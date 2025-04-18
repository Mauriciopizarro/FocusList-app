FocusList-app
-

https://task-app-api-backend.onrender.com/

# Introducción

Este repositorio contiene una aplicación en Python, usando el framework Fast Api para el desarrollo de los endpoints y Mongodb como base de datos principal.<br>
En esta app un usuario puede registrarse, iniciar o cerrar sesión, restablecer su password, etc.
<br>
Una vez que el usuario inicia sesión, puede crear tareas, listarlas y finalizar las mismas.

# Tecnologías utilizadas

- Docker
- MongoDB
- FastAPI
- Inyeccion de dependencias
- JWT
- Oauth2
- Pydantic
- Jinja2 templates
- Bootstrap
- HTML
- Pytest
- GitHub / GitHub Actions


# Instalación

1) Clonar el repositorio

            git clone https://github.com/Mauriciopizarro/kenwin-challenge.git

2) Crear el archivo env en el raiz del proyecto y configurar las siguientes variables de entorno <br> <br>
  **_FAST_API_PORT_**=<br>
  **_DATABASE_URL_**= <br>
  **_ACCESS_TOKEN_EXPIRES_IN_**= <br>
  **_JWT_ALGORITHM_**= <br>
 **_JWT_PRIVATE_KEY_**= <br>
 **_JWT_PUBLIC_KEY_**= <br>
<br>
3) Buildear del docker compose

       docker-compose build
4) Iniciar contenedores

       docker-compose up

5) Listo, la app ya está levantada en el puerto 5000 (o el puerto que hayas colocado en el env)

<br>


# Endpoints
                                                

## Login

En primer lugar se debe registrar un usuario (enviar en el body '**email**', '**username**' y '**password**')

`http://localhost:5000/api/v1/register`

    curl --location --request POST 'http://localhost:5000/api/v1/register' \
    --header 'Content-Type: application/json' \
    --data-raw '{
        "email": "example@mail.com",
        "username": "Name",
        "password": "Password"
    }

**Constraints**

- El email debe ser una dirección de mail válida.
- La contraseña debe contener entre 8 y 14 caracteres.


Una vez registrado, se debe iniciar con las credenciales colocadas en el register

`http://localhost:5000/api/v1/login`

    curl --location --request POST 'http://localhost:5000/api/v1/login' \
    --header 'Content-Type: application/json' \
    --data-raw '{
        "email": "your_email",
        "password": "your_password"
    }'

Al iniciar sesión, se creara un access_token, este será seteado en las cookies de las request, por lo que no será necesario colocarlo manualmente. Los demás endpoints van a requerir de estar autenticado.
<br>
El usuario puede cerrar sesión a través del siguiente endpoint

`http://localhost:5000/api/v1/logout`

<br>

Estando logueado, el usuario puede cambiar su contraseña

`http://localhost:5000/api/v1/reset_password`
<br>

    curl --location --request POST 'http://localhost:5000/api/v1/reset_password' \
    --header 'Content-Type: application/json' \
    --data-raw '{
        "new_password": "new_pass",
        "repeat_new_password": "repeat_new_pass"
    }'

<br>

## Tareas

El usuario puede crear sus propias tareas, las mismas tendrán descripción dificultad, fecha de inicio y fecha de fin, etc.

Para crear una tarea debemos estar autenticados. <br>

`http://localhost:5000/api/v1/create_task`

    curl --location --request POST 'http://localhost:5000/api/v1/create_task' \
    --header 'Content-Type: application/json' \
    --data-raw '{
        "description": "Alguna descripción",
        "difficult": 3
    }'

**Constraints**
- La dificultad debe ser un valor numérico entre 1 y 10, siendo 1 una tarea fácil o 10 muy difícil.
<br>
<br>

Para visualizar todas nuestras tareas, debe hacer GET al siguiente endpoint

`http://localhost:5000/api/v1/tasks`

    curl --location --request GET 'http://localhost:5000/api/v1/tasks'
<br>
<br>
Para finalizar una tarea se debe enviar por parámetro el id de la tarea, este se puede obtener haciendo un GET en el anterior endpoint.
`http://localhost:5000/api/v1/finish_task/{task_id}`

    curl --location --request POST 'http://localhost:5000/api/v1/finish_task/{task_id}'


# Front-end

SignUp:
![image](https://github.com/user-attachments/assets/e56c22db-3135-4932-99c1-fd7ee8a41dde)

Login:
![image](https://github.com/user-attachments/assets/b8bc4b8d-f9f1-4aee-92f7-8ee8c190dc9b)

Home:
![image](https://github.com/user-attachments/assets/5c4499fb-60dc-426a-acda-98cf0fd1a3de)

Create new task:
![image](https://github.com/user-attachments/assets/72d46008-fb0c-408d-8c39-870ec9cc6d4c)

Filter your tasks:
![image](https://github.com/user-attachments/assets/9f9e6733-fb8a-4614-90d8-b7cde6508cc8)

Task details:
![image](https://github.com/user-attachments/assets/bcc092aa-cad6-431a-a627-37bbb90dc227)

Tasks in progress filter:
![image](https://github.com/user-attachments/assets/9d1d9e87-d397-4fbc-bc9e-ba182e9fe773)



<br>
<br>
<br>
<br>

## Desarrollo

Esta app ha sido desarrollada por Mauricio Pizarro con el proposito de ser enviada como prueba tecnica. <br>
Email: pizarromauricio031096@gmail.com
