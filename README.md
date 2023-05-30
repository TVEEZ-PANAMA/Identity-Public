# Identity
Es un novedoso sistema de identificación biométrica diseñado para reconocer, verificar y dar prueba de vida de un usuario, sin mantener contacto personal.

## Versiones
## v1.3.0

### Login SDK
### Ejemplos:
Ejemplos para consumir el **/auth/login-sdk** desde las siguientes plataformas:
- **Javascript Fetch**
```
var myHeaders = new Headers();
myHeaders.append("Content-Type", "application/json");

var raw = JSON.stringify({
  "username": "xxxxxxxxxxxx@domain.com",
  "email": "xxxxxxxxxxxx@domain.com",
  "password": "x*x*x*x*x*x*x*x"
});

var requestOptions = {
  method: 'POST',
  headers: myHeaders,
  body: raw,
  redirect: 'follow'
};

fetch("https://xxxxxxxx/auth/login-sdk", requestOptions)
  .then(response => response.text())
  .then(result => console.log(result))
  .catch(error => console.log('error', error));
```

- **Node Js Axios**
```
const axios = require('axios');
let data = JSON.stringify({
  "username": "xxxxxxxxxxxx@domain.com",
  "email": "xxxxxxxxxxxx@domain.com",
  "password": "x*x*x*x*x*x*x*x"
});

let config = {
  method: 'post',
  maxBodyLength: Infinity,
  url: 'https://xxxxxxxx/auth/login-sdk',
  headers: { 
    'Content-Type': 'application/json'
  },
  data : data
};

axios.request(config)
.then((response) => {
  console.log(JSON.stringify(response.data));
})
.catch((error) => {
  console.log(error);
});
```

- **C# HttpClient**
```
var client = new HttpClient();
var request = new HttpRequestMessage(HttpMethod.Post, "https://xxxxxxxx/auth/login-sdk");
var content = new StringContent("{\r\n    \"username\": \"xxxxxxxxxxxx@domain.com\",\r\n    \"email\": \"xxxxxxxxxxxx@domain.com\",\r\n    \"password\": \"x*x*x*x*x*x*x*x\"\r\n}", null, "application/json");
request.Content = content;
var response = await client.SendAsync(request);
response.EnsureSuccessStatusCode();
Console.WriteLine(await response.Content.ReadAsStringAsync());
```

### Match-2d-2d
### Ejemplos:
Ejemplos para consumir el **/user/f/match-2d-2d** desde las siguientes plataformas:
- **Javascript Fetch**
```
var myHeaders = new Headers();
myHeaders.append("x-device-key", "ESTE VALOR SE OBTIENE DEL LOGIN EN LA VARIABLE data.user.companyRaw.deviceUUID");
myHeaders.append("Authorization", "TOKEN-GENERADO-EN-EL-LOGIN");
myHeaders.append("x-user-agent", "identity");
myHeaders.append("Content-Type", "application/json");

var raw = JSON.stringify({
  "image0": "base64",
  "image1": "base64",
  "minMatchLevel": 4
});

var requestOptions = {
  method: 'POST',
  headers: myHeaders,
  body: raw,
  redirect: 'follow'
};

fetch("https://xxxxxxxxx/user/f/match-2d-2d", requestOptions)
  .then(response => response.text())
  .then(result => console.log(result))
  .catch(error => console.log('error', error));
```

- **Node Js Axios**
```
const axios = require('axios');
let data = JSON.stringify({
  "image0": "base64",
  "image1": "base64",
  "minMatchLevel": 4
});

let config = {
  method: 'post',
  maxBodyLength: Infinity,
  url: 'https://xxxxxxxxxxxxxxxx/user/f/match-2d-2d',
  headers: { 
    'x-device-key': 'ESTE VALOR SE OBTIENE DEL LOGIN EN LA VARIABLE data.user.companyRaw.deviceUUID', 
    'Authorization': 'TOKEN-GENERADO-EN-EL-LOGIN', 
    'x-user-agent': 'identity', 
    'Content-Type': 'application/json'
  },
  data : data
};

axios.request(config)
.then((response) => {
  console.log(JSON.stringify(response.data));
})
.catch((error) => {
  console.log(error);
});
```

- **C# HttpClient**
```
var client = new HttpClient();
var request = new HttpRequestMessage(HttpMethod.Post, "https://xxxxxxxxxxxxxxxx/user/f/match-2d-2d");
request.Headers.Add("x-device-key", "ESTE VALOR SE OBTIENE DEL LOGIN EN LA VARIABLE data.user.companyRaw.deviceUUID");
request.Headers.Add("Authorization", "TOKEN-GENERADO-EN-EL-LOGIN");
request.Headers.Add("x-user-agent", "identity");
var content = new StringContent("{\r\n    \"image0\": \"base64\",\r\n    \"image1\": \"base64\",\r\n    \"minMatchLevel\": 4\r\n}", null, "application/json");
request.Content = content;
var response = await client.SendAsync(request);
response.EnsureSuccessStatusCode();
Console.WriteLine(await response.Content.ReadAsStringAsync());
```


