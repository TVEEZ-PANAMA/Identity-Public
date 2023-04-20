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

### Códigos de Respuesta SIB

A continuación se detallan los diferentes códigos de respuesta que puede retornar el servicio:

Código | Descripción | Resultado
--- | --- | ---
0 | Usuario Validado | TRUE
603 | Ciudadano difunto | FALSE
604 | Ciudadano mayor de edad cuya inscripción de Nacimiento (Nacional) esté cancelada | FALSE
602 | Ciudadano menor de 12 años | FALSE
601 | Cédula no existe en la base de datos | FALSE
606 | Cédula en blanco | FALSE
601 | Cédula con formato inválido | FALSE
605 | Ciudadano no reconocido | FALSE

También se describen los siguientes casos especiales:

- Ciudadano difunto: retorna FALSE con el código de error 603.
- Ciudadano mayor de edad cuya inscripción de Nacimiento (Nacional) esté cancelada: retorna FALSE con el código de error 604.
- Ciudadano menor de 12 años: retorna FALSE con el código de error
- Cédula no existe en la base de datos: retorna FALSE con el código de error 601.
- Cédula en blanco: retorna FALSE con el código de error 606.
- Cédula con formato inválido: actualmente no está contemplado en el servicio, por lo que retorna el código de error 601.
- Ciudadano sin foto registrada: retorna FALSE con el código de error 605.
- El rostro no coincide con los registros: retorna FALSE con el código de error 605.
