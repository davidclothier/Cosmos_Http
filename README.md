[<img src="http://www.base100.com/images/productos/cosmos/cosmos_v60.jpg" alt="Cosmos" width="96"/>]()

# Cosmos http include
Include con una clase *adapter* para realizar peticiones http en formato Json basada en la interfaz COM de Microsoft [*Msxml2.XMLHTTP*](https://es.wikipedia.org/wiki/XMLHttpRequest).

Para versiones iguales o superiores a [Cosmos 6.0](http://www.base100.com/es/productos/cosmos01.html) (es necesaria la clase Json)

## Uso

* La clase ``cRequest`` es la responsable de hacer las peticiones.
* Es necesario inicializar el objeto con el método ``reset`` antes usarlo.
* Se pueden pasar parámetros en la query
* Se pueden añadir cabeceras
* Permite los cuatro métodos principales ``GET``, ``POST``, ``UPDATE``,``DELETE``
* El resultado se almacena en la propiedad ``Response`` en formato Json.
* Calcula con precisión de milésimas de segundos el tiempo en resolver la petición. Se obtiene con el método ```getTimeElapsed```
* La petición es síncrona

## Ejemplos

### Un ejemplo con paso de parámetros en la query

```
private testQueryParameter
objects
begin
    Request         as cRequest
end
begin
    Request.reset();
    
    Request.Url = "http://uinames.com/api/";
    Request.Method = HttpTypes.GET_METHOD;
    Request.addQueryParameter( "region", "spain" );
    Request.addQueryParameter( "ext", "" );
    Request.send();

    Request.Response.Trace();
end
```

### Un ejemplo con uso de cabeceras
> Ejemplo no operativo por uso de `api-key`
```
private testHeaders
objects
begin
    Request         as cRequest    
end
begin
    Request.reset();

    Request.Url = "https://api.sendinblue.com/v3/senders";
    Request.Method = HttpTypes.GET_METHOD;
    Request.addHeader( "api-key", "abcdefg");
    Request.send();

    Request.Response.Trace();
end
```

### Un ejemplo con paso de parámetros en el body
> Ejemplo no operativo por uso de `api-key`
```
private testBodyParameter
objects
begin
    Request         as cRequest
    jsnMain         as Json
    jsnAttributes   as Json
    jsnListIds      as Json
end
begin
    jsnAttributes.Set( "NAME", "DAVID" );
    jsnAttributes.Set( "SURNAME", "CLOTHIER" );
    jsnAttributes.Set( "M123_LUGAR", "OFFICE" );
    
    jsnListIds.SetAsArray();
    jsnListIds.AddArrayElement( 2 );
    jsnListIds.AddArrayElement( 3 );
    
    jsnMain.Set( "attributes", jsnAttributes );
    jsnMain.Set( "listIds", jsnListIds );
    jsnMain.Set( "emailBlacklisted", true );
    jsnMain.Set( "smsBlacklisted", false );
    
    Request.reset();
    Request.Url = "https://api.sendinblue.com/v3/contacts/david.ropero@actionsdata.com";
    Request.Method = HttpTypes.PUT_METHOD;
    Request.addHeader( "api-key" , "abcdefg" );
    Request.addHeader( "Content-Type", "application/json" );
    Request.Body = jsnMain;
    Request.send();
    
    Request.StatusResponse.Trace;
end
```

## Mejoras futuras

* Envoltorio para métodos de autenticación como Basic Auth, Digest, OAuth 2.0, etc.
* Invocación asíncrona con callback

## Desarrollado por

* David Ropero Alcázar - david.ropero@gmail.com

[<img src="https://image.freepik.com/iconos-gratis/boton-del-logotipo-de-twitter_318-85053.jpg" alt="Twitter" width="48"/>](https://twitter.com/clothierdroid)
[<img src="http://www.iconsdb.com/icons/preview/black/linkedin-4-xxl.png" alt="Linkedin" width="48"/>](http://www.linkedin.com/in/davidropero)

## Licencia

GNU Public License v3.0

