# Cosmos http
Include para realizar peticiones http en formato Json basada en la librería de Microsoft *Msxml*.
Para versiones iguales o superiores a Cosmos 6.0 (es necesaria la clase Json)

## Clase principal y uso

* La clase ``cRequest`` es la responsable de hacer las peticiones.
* Es necesario inicializar el objeto con el método ``reset`` antes usarlo.
* Se pueden pasar parámetros en la query
* Se pueden añadir cabeceras
* Permite los cuatro métodos principales ``GET``, ``POST``, ``UPDATE``,``DELETE``
* El resultado se almacena en la propiedad ``Response`` en formato Json.
* Calcula con precisión de milésimas de segundos el tiempo en resolver la petición

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

