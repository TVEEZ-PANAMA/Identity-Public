# Identity
Es un novedoso sistema de identificación biométrica diseñado para reconocer, verificar y dar prueba de vida de un usuario, sin mantener contacto personal.
### Identificación Biométrica
### Sistema de prueba de vida
### Software de prevención de falsificación de documentos
### Software de verificación de identidad
### Evitar robo de identidad

## Versiones
## v1.3.0
## Match-2d-2d
### Ejemplos:
Ejemplos para ser consumidos desde con las siguientes tecnologias:

1 Javascript Fetch
``
var myHeaders = new Headers();
myHeaders.append("Content-Type", "application/json");

var raw = JSON.stringify({
  "username": "sdk@capsa.com",
  "email": "sdk@capsa.com",
  "password": "jDmfRockZO"
});

var requestOptions = {
  method: 'POST',
  headers: myHeaders,
  body: raw,
  redirect: 'follow'
};

fetch("https://facetec.getxplor.com:8443/auth/login-sdk", requestOptions)
  .then(response => response.text())
  .then(result => console.log(result))
  .catch(error => console.log('error', error));
``

