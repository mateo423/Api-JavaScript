# User List Fetcher

Este script de JavaScript recupera una lista de usuarios de una API y los muestra en una página web.

## Descripción

El script realiza las siguientes acciones:

1. Selecciona un elemento del DOM con el id 'usersList'.
2. Hace una petición fetch a la API 'https://reqres.in/api/users?page=2'.
3. Procesa la respuesta JSON.
4. Para cada usuario en los datos recibidos, inserta HTML en el elemento 'usersList' que incluye:
   - Avatar del usuario
   - Nombre y apellido del usuario
   - Dirección de correo electrónico del usuario (con un enlace mailto)

## Código

```javascript
const usersList = document.querySelector('#usersList');
fetch('https://reqres.in/api/users?page=2')
  .then((response) => {
    return response.json();
  })
  .then((info) => {
    const users = info.data;
    for (const user of users) {
      usersList.insertAdjacentHTML(
        "beforeend",
        ` 
        <div>
          <img src="${user.avatar}" alt="" />
          <h3>${user.first_name} ${user.last_name}</h3>
          <a href="mailto:${user.email}">${user.email}</a>
          <hr/>
        </div>
      `
      );
    }
  })
  .catch((error) => {
    console.log(error);
  });
```

## Uso

1. Asegúrate de tener un elemento en tu HTML con el id 'usersList'. Por ejemplo:

   ```html
   <div id="usersList"></div>
   ```

2. Incluye el script en tu archivo HTML:

   ```html
   <script src="path/to/your/script.js"></script>
   ```

3. Cuando se cargue la página, el script se ejecutará automáticamente y poblará el elemento 'usersList' con la información de los usuarios.

## Dependencias

Este script no tiene dependencias externas. Utiliza las API fetch y Promises nativas de JavaScript, que están disponibles en la mayoría de los navegadores modernos.

## Notas

- Este script utiliza la API de reqres.in, que es un servicio de API REST de prueba. En un entorno de producción, deberías reemplazar la URL con la de tu propia API.
- El manejo de errores es básico (solo registra en la consola). En una aplicación real, considera implementar un manejo de errores más robusto.

