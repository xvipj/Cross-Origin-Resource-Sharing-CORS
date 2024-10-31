# Cross-Origin Resource Sharing (CORS)

## Configurando CORS en Django para permitir solicitudes de un dominio específico

### ¿Qué es CORS?

CORS (Cross-Origin Resource Sharing) es un mecanismo de seguridad que los navegadores web utilizan para restringir las solicitudes HTTP que una página web puede realizar a un servidor de un dominio diferente. Esto ayuda a prevenir ataques de scripting entre sitios (XSS).

### ¿Por qué es necesario configurar CORS?

Cuando una aplicación frontend (como una aplicación Angular) intenta hacer una solicitud a un backend (como un API Django), el navegador verifica si el servidor backend permite solicitudes desde ese origen. Si el servidor no está configurado correctamente, se produce un error CORS.

### Configuración de CORS en Django

**1. Instalar la aplicación `django-cors-headers`:**

```bash
pip install django-cors-headers
```

**2. Configurar el archivo `settings.py`:**

* **Agregar la aplicación al archivo `INSTALLED_APPS`:**

  ```python
  INSTALLED_APPS = [
      # ... otras aplicaciones
      'corsheaders',
  ]
  ```

* **Agregar el middleware `CorsMiddleware` al archivo `MIDDLEWARE`:**

  ```python
  MIDDLEWARE = [
      # ... otros middlewares
      'corsheaders.middleware.CorsMiddleware',
      'django.middleware.common.CommonMiddleware',
  ]
  ```

* **Definir los orígenes permitidos en `CORS_ORIGIN_WHITELIST`:**

  ```python
  CORS_ORIGIN_WHITELIST = [
      'http://localhost:4200',  # Reemplaza con el dominio de tu aplicación
  ]
  ```

**3. Aplicar los cambios:**

* Ejecutar las migraciones:

  ```bash
  python manage.py migrate
  ```

* Reiniciar el servidor Django.

### Opciones de configuración adicionales

* **Múltiples orígenes:**

  ```python
  CORS_ORIGIN_WHITELIST = [
      'http://localhost:4200',
      'https://mi-aplicacion.com'
  ]
  ```

* **Métodos HTTP permitidos:**

  ```python
  CORS_ALLOWED_METHODS = [
      'GET',
      'POST',
      'PUT',
      'DELETE'
  ]
  ```

* **Encabezados permitidos:**

  ```python
  CORS_ALLOW_HEADERS = [
      'Content-Type',
      'Authorization'
  ]
  ```

### Consideraciones adicionales

* **Seguridad:** Evita permitir el acceso desde cualquier origen (`*`). Configura los orígenes permitidos de forma específica.
* **Desarrollo vs. Producción:** Ajusta los orígenes permitidos según el entorno de desarrollo o producción.

* **Documentación:** Consulta la documentación oficial de `django-cors-headers` para obtener más opciones de configuración: [https://pypi.org/project/django-cors-headers/](https://pypi.org/project/django-cors-headers/)

### Conclusión

Configurar CORS en Django es esencial para permitir que tu aplicación frontend se comunique de forma segura con tu backend. Siguiendo estos pasos, podrás evitar errores CORS y garantizar una correcta interacción entre tus aplicaciones.

