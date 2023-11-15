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




def favoritos(request):
    # select * from favoritos
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







    
     
    
