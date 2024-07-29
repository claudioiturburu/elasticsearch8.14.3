**ELASTICSEARCH 8.14.3** 


- [Iniciar contenedor con ElasticSearch y Kibana](#iniciar-contenedor-con-elasticsearch-y-kibana)
- [Verbos HTTP](#verbos-http)
  - [POST](#post)
    - [Crear un recurso](#crear-un-recurso)
  - [PUT](#put)
    - [Actualizar un recurso](#actualizar-un-recurso)
  - [DELETE](#delete)
    - [Eliminar un recurso](#eliminar-un-recurso)
    - [Eliminar un índice](#eliminar-un-índice)
  - [GET](#get)
    - [Solicita un recurso](#solicita-un-recurso)
    - [Solicitar un conjunto de recursos](#solicitar-un-conjunto-de-recursos)
    - [Listar índices](#listar-índices)

# Iniciar contenedor con ElasticSearch y Kibana

```console
docker compose up -d
```
ElasticSearch (motor de búsqueda) levantará el servicio en los puertos 9200 y 9300. Se podrá acceder a la api con http://localhost:9200
Kibana (gestiona ES) levantará el servicio en el puerto 5601, pudiendo acceder al mismo en http://localhost:5601


# Verbos HTTP
Los elementos en letra italic los determina el usuario. Las llaves con puntos suspensivos indican un JSON.

## POST
### Crear un recurso
POST /*indice*/_doc*{...}* 
Ejemplo:
POST /movimiento/_doc
{
    "id_movimiento_expediente": "d55e20bc-5d6a-48e3-aacf-796896925bac",
    "numero_movimiento": "VI-2024-I-0004",
    "descripcion": "Resolución del STJ",
    "fecha_publicacion": "2024-02-02T13:42:00.00011Z"
}

## PUT
### Actualizar un recurso
PUT /*indice*/_doc/*<ID>**{...}* 
Ejemplo:
PUT /movimiento/_doc/d55e20bc-5d6a-48e3-aacf-796896925bac
{
    "id_movimiento_expediente": "d55e20bc-5d6a-48e3-aacf-796896925bac",
    "numero_movimiento": "VI-2024-I-0004",
    "descripcion": "Resolución del STJ protocolizada",
    "fecha_publicacion": "2024-02-02T13:42:00.00011Z"
}


## DELETE
### Eliminar un recurso
DELETE /*indice*/_doc/*<ID>* 
Ejemplo:
DELETE /movimiento/_doc/d55e20bc-5d6a-48e3-aacf-796896925bac
### Eliminar un índice
DELETE /*<indice>*
Ejemplo:
DELETE /movimiento

## GET
### Solicita un recurso
GET /*indice*/_doc/*<ID>* 
Ejemplo:
GET /movimiento/_doc/d55e20bc-5d6a-48e3-aacf-796896925bac
### Solicitar un conjunto de recursos
GET /*<indice>*/_search/*{...}*
Ejemplo para obtener todos los documentos:
GET /*<indice>*/_search/
{
    "query": {
        "match_all": {}
    }
}
### Listar índices
GET /_cat/indices





