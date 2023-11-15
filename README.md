    path('favoritos_listar/', views.favoritos, name="favoritos_listar"),
    path('favoritos_form/', views.favoritos_form, name="favoritos_form"),
    path('favoritos_crear/', views.favoritos_crear, name="favoritos_crear"),
    path('favoritos_actualizar/', views.favoritos_actualizar, name="favoritos_actualizar"),
    path('favoritos_eliminar/<int:id>/', views.favoritos_eliminar, name="favoritos_eliminar"),
    path('favoritos_formulario_editar/<int:id>/', views.favoritos_formulario_editar, name="favoritos_formulario_editar"),

    
    path('hotel_comodidad_listar/', views.hotel_comodidad, name="hotel_comodidad_listar"),
    path(hotel_comodidad'_form/', views.hotel_comodidad_form, name="hotel_comodidad_form"),
    path('hotel_comodidad_crear/', views.hotel_comodidad_crear, name="hotel_comodidad_crear"),
    path('hotel_comodidad_actualizar/', views.hotel_comodidad_actualizar, name="hotel_comodidad_actualizar"),
    path('hotel_comodidad_eliminar/<int:id>/', views.hotel_comodidad_eliminar, name="hotel_comodidad_eliminar"),
    path('hotel_comodidad_formulario_editar/<int:id>/', views.hotel_comodidad_formulario_editar,   name="hotel_comodidad_formulario_editar"),


def favoritos(request):
    consulta = Favorito.objects.all()
    context = {'data': consulta}
    return render(request, 'planning_travel/favoritos/favoritos.html', context)

def favoritos_form(request):
    return render(request, 'planning_travel/favoritos/favoritos_form.html')

def favoritos_crear(request):
    if request.method == 'POST':
        id_hotel = request.POST.get('id_hotel')
        id_usuario = request.POST.get('id_usuario')
        fecha_agregado = request.POST.get('fecha_agregado')

        try:
            q = Favorito(
                id_hotel=id_hotel,
                id_usuario=id_usuario,
                fecha_agregado=fecha_agregado,
            )
            q.save()
            messages.success(request, "Fue agregado correctamente")
        except Exception as e:
            messages.error(request,f'Error: {e}')

        return redirect('favoritos_listar')
    else:
        messages.warning(request,'No se enviaron datos')
        return redirect('favoritos_listar')

def favoritos_eliminar(request, id):
    try:
        q = Favorito.objects.get(pk = id)
        q.delete()
        messages.success(request, 'Hotel favorito eliminado correctamente!!')
    except Exception as e:
        messages.error(request,f'Error: {e}')

    return redirect('favoritos_listar')

def favoritos_formulario_editar(request, id):

    q = Favorito.objects.get(pk = id)
    contexto = {'data': q}

    return render(request, 'planning_travel/favoritos/favoritos_formulario_editar.html', contexto)

def favoritos_actualizar(request):
    if request.method == 'POST':
        id_hotel = request.POST.get('id_hotel')
        id_usuario=request.POST.get('id_usuario')
        fecha_agregado = request.POST.get('fecha_agregado')

        try:
            q = Favorito.objects.get(pk = id)
            q.id_hotel= id_hotel
            q.id_usuario = id_usuario
            q.fecha_agregado=fecha_agregado
            q.save()
            messages.success(request, "Fue actualizado correctamente")
        except Exception as e:
            messages.error(request,f'Error: {e}')
    else:
        messages.warning(request,'No se enviaron datos')
        
    return redirect('favoritos_listar')




def hotel_comodidad(request):
    consulta = Hotel_comodidad.objects.all()
    context = {'data': consulta}
    return render(request, 'planning_travel/hotel_comodidad/hotel_comodidad.html', context)

def hotel_comodidad_form(request):
    return render(request, 'planning_travel/hotel_comodidad/hotel_comodidad_form.html')

def hotel_comodidad_crear(request):
    if request.method == 'POST':
        id_hotel = request.POST.get('id_hotel')
        id_comodidad = request.POST.get('id_comodidad')
        dispone = request.POST.get('dispone')

        try:
            q = Hotel_comodidad(
                id_hotel=id_hotel,
                id_comodidad=id_comodidad,
                dispone=dispone,
            )
            q.save()
            messages.success(request, "Fue agregado correctamente")
        except Exception as e:
            messages.error(request,f'Error: {e}')

        return redirect('hotel_comodidad_listar')
    else:
        messages.warning(request,'No se enviaron datos')
        return redirect('hotel_comodidad_listar')

def hotel_comodidad_eliminar(request, id):
    try:
        q = Hotel_comodidad.objects.get(pk = id)
        q.delete()
        messages.success(request, 'Comodidad eliminada correctamente!!')
    except Exception as e:
        messages.error(request,f'Error: {e}')

    return redirect('hotel_comodidad_listar')

def hotel_comodidad_formulario_editar(request, id):

    q = Hotel_comodidad.objects.get(pk = id)
    contexto = {'data': q}

    return render(request, 'planning_travel/hotel_comodidad/hotel_comodidad_formulario_editar.html', contexto)

def hotel_comodidad_actualizar(request):
    if request.method == 'POST':
        id_hotel = request.POST.get('id_hotel')
        id_comodidad = request.POST.get('id_comodidad')
        dispone = request.POST.get('dispone')

        try:
            q = Hotel_comodidad.objects.get(pk = id)
            q.id_hotel= id_hotel
            q.id_comodidad = id_comodidad
            q.dispone=dispone
            q.save()
            messages.success(request, "Fue actualizado correctamente")
        except Exception as e:
            messages.error(request,f'Error: {e}')
    else:
        messages.warning(request,'No se enviaron datos')
        
    return redirect('hotel_comodidad_listar')



Favoritos.html

{% extends 'planning_travel/base.html' %} 
{% load static %} 
{% block titulo %}Favoritos{% endblock %}
{% block contenedor %}
    <h1>Favoritos</h1>
    <a class="btn btn-success" href="{% url 'favoritos_form' %}">Agregar a favoritos</a>

    <table class="table">
        <thead>
            <th>ID</th>
            <th>Id hotel</th>
            <th>Id usuario</th>
            <th>Fecha agregado</th>
            <th>Acciones</th>
        </thead>
        <tbody>
            {% for r in data %}
            <tr>
                <td>{{ r.id }}</td>
                <td>{{ r.id_hotel }}</td>
                <td>{{ r.id_usuario }}</td>
                <td>{{ r.fecha_agregado }}</td>
                <td>
                    <button
                        type="button"
                        class="btn btn-info"
                        data-bs-toggle="modal"
                        data-bs-target="#modalVer-1"
                    >
                        <i class="bi bi-eye-fill"></i>
                    </button>
                    <a
                        class="btn btn-warning"
                        href="{% url 'favoritos_formulario_editar' r.id %}"
                        ><i class="bi bi-pencil"></i
                    ></a>
                    <a
                        href="javascript:eliminar('{% url 'favoritos_eliminar' r.id %}')"
                        class="btn btn-danger"
                        ><i class="bi bi-x-lg"></i
                    ></a>
                </td>
            </tr>
            {% endfor %}
        </tbody>
    </table>
    <nav aria-label="Page navigation example">
        <ul class="pagination">
            <li class="page-item"><a class="page-link" href="#">Anterior</a></li>
            <li class="page-item"><a class="page-link" href="#">1</a></li>
            <li class="page-item"><a class="page-link" href="#">2</a></li>
            <li class="page-item"><a class="page-link" href="#">3</a></li>
            <li class="page-item"><a class="page-link" href="#">Siguiente</a></li>
        </ul>
    </nav>
{% endblock %}



Hotel como

{% extends 'planning_travel/base.html' %} 
{% load static %} 
{% block titulo %}Hotel_comodidad{% endblock %}
{% block contenedor %}
    <h1>Hotel comodidad</h1>
    <a class="btn btn-success" href="{% url 'favoritos_form' %}">Agregar comodidad</a>

    <table class="table">
        <thead>
            <th>ID</th>
            <th>Id hotel</th>
            <th>Id comodidad</th>
            <th>Dispone</th>
            <th>Acciones</th>
        </thead>
        <tbody>
            {% for r in data %}
            <tr>
                <td>{{ r.id }}</td>
                <td>{{ r.id_hotel }}</td>
                <td>{{ r.id_comodidad }}</td>
                <td>{{ r.dispone }}</td>
                <td>
                    <button
                        type="button"
                        class="btn btn-info"
                        data-bs-toggle="modal"
                        data-bs-target="#modalVer-1"
                    >
                        <i class="bi bi-eye-fill"></i>
                    </button>
                    <a
                        class="btn btn-warning"
                        href="{% url 'hotel_comodidad_formulario_editar' r.id %}"
                        ><i class="bi bi-pencil"></i
                    ></a>
                    <a
                        href="javascript:eliminar('{% url 'hotel_comodidad_eliminar' r.id %}')"
                        class="btn btn-danger"
                        ><i class="bi bi-x-lg"></i
                    ></a>
                </td>
            </tr>
            {% endfor %}
        </tbody>
    </table>
    <nav aria-label="Page navigation example">
        <ul class="pagination">
            <li class="page-item"><a class="page-link" href="#">Anterior</a></li>
            <li class="page-item"><a class="page-link" href="#">1</a></li>
            <li class="page-item"><a class="page-link" href="#">2</a></li>
            <li class="page-item"><a class="page-link" href="#">3</a></li>
            <li class="page-item"><a class="page-link" href="#">Siguiente</a></li>
        </ul>
    </nav>
{% endblock %}










Form favoritos

{% extends 'planning_travel/base.html' %}
{% load static %}

{% block titulo %}Formulario Favoritos{% endblock %}

{% block contenedor %}
    <div class="container my-5 w-25">
        <h1 class="text-center">Registrar Favoritos</h1>
        <form action="{% url 'favoritos_crear' %}" method="post">
            {% csrf_token %}
            <div class="form-floating mb-3">
                <input type="text" class="form-control" id="id_hotel" placeholder="Id_hotel" name="id_hotel">
                <label for="id_hotel">Id hotel</label>
            </div>
            <div class="form-floating mb-3">
                <input type="text" class="form-control" id="id_usuario" placeholder="Id_usuario" name="id_usuario">
                <label for="id_usuario">Id usuario</label>
            </div>
<div class="form-floating mb-3">
                <input type="text" class="form-control" id="fecha_agregado" placeholder="Fecha_agregado" name="fecha_agregado">
                <label for="fecha_agregado">Fecha agregado</label> faltaaa
            </div>
            <div class="row my-2">
                <button type="submit" class="btn btn-primary">Registrar</button>
            </div>
        </form>
    </div>
{% endblock %}


Form hotel

{% extends 'planning_travel/base.html' %}
{% load static %}

{% block titulo %}Formulario Comodidad Hotel{% endblock %}

{% block contenedor %}
    <div class="container my-5 w-25">
        <h1 class="text-center">Registrar Comodidad Hotel</h1>
        <form action="{% url 'comodidad_hotel_crear' %}" method="post">
            {% csrf_token %}
            <div class="form-floating mb-3">
                <input type="text" class="form-control" id="id_hotel" placeholder="Id_hotel" name="id_hotel">
                <label for="id_hotel">Id hotel</label>
            </div>
            <div class="form-floating mb-3">
                <input type="text" class="form-control" id="id_comodidad" placeholder="Id_comodidad" name="id_comodidad">
                <label for="id_comodidad">Id comodidad</label>
            </div>
<div class="form-floating mb-3">
                <input type="text" class="form-control" id="dispone" placeholder="Dispone" name="dispone">
                <label checkboss for="dispone">Dispone</label> faltaaa
            </div>
            <div class="row my-2">
                <button type="submit" class="btn btn-primary">Registrar</button>
            </div>
        </form>
    </div>
{% endblock %}






Favoritosformedit
{% extends 'planning_travel/base.html' %}
{% load static %}

{% block titulo %}Formulario Favoritos{% endblock %}

{% block contenedor %}
    <div class="container my-5 w-25">
        <h1 class="text-center">Actualizar Favoritos</h1>
        <form action="{% url 'favoritos_actualizar' %}" method="post">
            {% csrf_token %}
            <input hidden type="text" name="id" value="{{ data.id }}">
            <div class="form-floating mb-3">
                <input type="text" class="form-control" id="id_hotel" placeholder="Id_hotel" name="id_hotel" value="{{ data.id_hotel }}”>
                <label for="id_hotel">Id hotel</label>
            </div>
            <div class="form-floating mb-3">
                <input type="text" class="form-control" id="id_usuario" placeholder="Id_usuario" name="id_usuario" value="{{ data.id_usuario }}”>
                <label for="id_usuario">Id usuario</label>
            </div>
<div class="form-floating mb-3">
                <input type="text" class="form-control" id="fecha_agregado" placeholder="Fecha_agregado" name="fecha_agregado" value="fecha_agregado”>
                <label for="fecha_agregado">Fecha agregado</label> faltaaa
            </div>
            <div class="row my-2">
                <button type="submit" class="btn btn-primary">Actualizar</button>
            </div>
        </form>
    </div>
{% endblock %}




Formhotel

Favoritosformedit
{% extends 'planning_travel/base.html' %}
{% load static %}

{% block titulo %}Formulario Favoritos{% endblock %}

{% block contenedor %}
    <div class="container my-5 w-25">
        <h1 class="text-center">Actualizar Favoritos</h1>
        <form action="{% url 'favoritos_actualizar' %}" method="post">
            {% csrf_token %}
            <input hidden type="text" name="id" value="{{ data.id }}">
            <div class="form-floating mb-3">
                <input type="text" class="form-control" id="id_hotel" placeholder="Id_hotel" name="id_hotel" value="{{ data.id_hotel }}”>
                <label for="id_hotel">Id hotel</label>
            </div>
            <div class="form-floating mb-3">
                <input type="text" class="form-control" id="id_comodidad" placeholder="Id_comodidad" name="id_comodidad" value="{{ data.id_comodidad }}”>
                <label for="id_comodidad">Id comodidad</label>
            </div>
<div class="form-floating mb-3">
                <input type="text" class="form-control" id="dispone" placeholder="Dispone" name="dispone" value="{{ data.dispone }}”>
                <label checkboss for="dispone">Dispone</label> faltaaa
            </div>
            <div class="row my-2">
                <button type="submit" class="btn btn-primary">Actualizar</button>
            </div>
        </form>
    </div>
{% endblock %}





