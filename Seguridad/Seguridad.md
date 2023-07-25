# Seguridad

## Sanitizacion, jsx, headers en server

## Sanitización de Datos del Usuario: Para prevenir ataques de XSS, es fundamental asegurarse de que todos los datos ingresados por el usuario se saniticen adecuadamente antes de ser renderizados en la interfaz. Utiliza bibliotecas de sanitización como DOMPurify para limpiar cualquier contenido HTML peligroso antes de mostrarlo.

## Uso de JSX para Evitar Inyecciones: En React y React Native, utiliza JSX para renderizar contenido dinámico en lugar de manipular directamente el DOM. JSX escapa automáticamente los datos y evita la inyección de código malicioso.

## Headers HTTP Seguros: Asegúrate de configurar correctamente las cabeceras HTTP en el servidor para prevenir ataques de CSRF. Utiliza el encabezado X-CSRF-Token o SameSite para controlar la política de same-origin.