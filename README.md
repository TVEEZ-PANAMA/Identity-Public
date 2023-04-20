# Validación Biométrica del Tribunal Electoral

Este es un servicio de validación biométrica del Tribunal Electoral de Panamá. Para poder hacer uso de este servicio, se deben seguir los siguientes pasos:

## Obtener Token de Autorización

Para poder hacer uso del servicio de validación, se debe obtener un token de autorización mediante una solicitud POST a la siguiente dirección:

POST: https://XXXXXXXXXXXXX/auth/login


La solicitud debe incluir un cuerpo JSON con las siguientes propiedades:


```
{
    "username": "XXXXXXX@xxxxxxxx.com",
    "email" : "XXXXXXXX@xxxxxxxx.com",
    "password" : "XXXXXXXX"
}
```

- Como Respuesta obtendrá detalles de su cuenta incluido el campo token.

```
{
    "code": 0,
    "data": {
        "user": {
            "companyRaw": {
                "logoImage": "xxxxxxxxxxxxxxxxxxxxxxxx",
                "deviceUUID": "xxxxxxxxxxxxxxxxxxxxxxx",
                "keys": "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
                "encryptionKey": "xxxxxxxxxxxxxxxxxxxxxxx",
                "ExternalDatabaseRefID": "xxxxxxxxxxxxxxxx",
                "maxAttempt": x
            }
        },
        "token": "xxxxxxxxx"
    }
}
```

## Realizar Consulta de Validación

Una vez obtenido el token de autorización, se debe realizar una solicitud POST a la siguiente dirección:

POST: https://XXXXXXXXXXXXX/user/makeRequest


La solicitud debe incluir un objeto JSON con las siguientes propiedades:


```
{
    "cedula": "X-XXXX-XXX",
    "photo": "XXXXXXXXX"
}
```

- La propiedad "cedula" debe contener el número de cédula del ciudadano que se quiere validar
- La propiedad "photo" debe contener la foto del ciudadano en formato BASE64.

## Respuesta del Servicio

- Luego de enviada la solicitud, se obtendrá una respuesta en formato JSON que contendrá la información de validación del ciudadano. 
- Dependiendo del resultado de la validación, se retornará un objeto JSON con los siguientes campos:

### Usuario Validado

Si el ciudadano es válido, se retornará un objeto JSON con el siguiente formato:

```
{
    "code": 0,
    "data": {
        "Resultado": true,
        "info": {
            "codigo": 0,
            "message": "OK",
            "IdTransaccion": 63184
        }
    }
}
```


### Usuario NO Validado

Si el ciudadano no es válido, se retornará un objeto JSON con el siguiente formato:

```
{
    "code": 605,
    "data": {
        "Resultado": false,
        "info": {
            "codigo": 605,
            "message": "",
            "IdTransaccion": 63189
        }
    }
}
```

El objeto "info" contendrá la información de validación del ciudadano, incluyendo el código de validación, el mensaje y el ID de la transacción.

