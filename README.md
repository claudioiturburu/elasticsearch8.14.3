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
- [Operaciones masivas](#operaciones-masivas)
  - [Bulk](#bulk)
  - [Multi GET](#multi-get)
- [Mappings](#mappings)
  - [Tipos de Datos](#tipos-de-datos)
    - [Cadenas](#cadenas)
    - [Numéricos](#numéricos)
    - [Fecha](#fecha)
    - [Booleanos](#booleanos)
    - [Binarios](#binarios)
    - [Geográficos](#geográficos)
    - [Complejos](#complejos)
    - [Otros](#otros)

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
POST /*indice*/_doc
*{...}* 

Ejemplo:

```console
POST /movimiento/_doc
{
    "id_movimiento_expediente": "d55e20bc-5d6a-48e3-aacf-796896925bac",
    "numero_movimiento": "VI-2024-I-0004",
    "descripcion": "Resolución del STJ",
    "fecha_publicacion": "2024-02-02T13:42:00.00011Z"
}
```
## PUT
### Actualizar un recurso
PUT /*indice*/_doc/*ID*
*{...}* 

Ejemplo:

```console
PUT /movimiento/_doc/d55e20bc-5d6a-48e3-aacf-796896925bac
{
    "id_movimiento_expediente": "d55e20bc-5d6a-48e3-aacf-796896925bac",
    "numero_movimiento": "VI-2024-I-0004",
    "descripcion": "Resolución del STJ protocolizada",
    "fecha_publicacion": "2024-02-02T13:42:00.00011Z"
}
```

## DELETE
### Eliminar un recurso
DELETE /*indice*/_doc/*ID* 

Ejemplo:

```console
DELETE /movimiento/_doc/d55e20bc-5d6a-48e3-aacf-796896925bac
```
### Eliminar un índice
DELETE /*indice*

Ejemplo:

```console
DELETE /movimiento
```
## GET
### Solicita un recurso
GET /*indice*/_doc/*ID* 

Ejemplo:

```console
GET /movimiento/_doc/d55e20bc-5d6a-48e3-aacf-796896925bac
```
### Solicitar un conjunto de recursos
GET /*indice*/_search/*{...}*

Ejemplo para obtener todos los documentos:

```console
GET /movimiento/_search/
{
    "query": {
        "match_all": {}
    }
}
```
### Listar índices
```console
GET /_cat/indices
```
# Operaciones masivas
Permite reducir el overhead e incrementar la velocidad de indexación haciendo uso del formato ndjson (consiste en realizar varios json separado por /n)
## Bulk
Permite realizar operaciones de ABM en una única solicitud
POST /_bulk

POST /*indice*/_bulk

Ejemplo:
```console

```


## Multi GET

GET /_mget

GET /*indice*/_mget

Ejemplo:
```console
GET /_mget
{
    "docs": [
        {
            "_index": "movimiento",
            "_id": "d55e20bc-5d6a-48e3-aacf-796896925bac"
        },
        {
            "_index": "movimiento",
            "_id": "a776de96-30e7-4813-9146-1bf713e6f9c8"
        }
    ]
}
```

# Mappings

## Tipos de Datos
### Cadenas
- `text`: un tipo de dato que se indexa en elasticsearch de manera que se pueda realizar búsquedas de texto completo.
- `keyword`: un tipo de dato que se indexa como una cadena plana, sin realizar ningún tipo de análisis.
### Numéricos
long
integer
short
byte
double
half_float
scaled_float
### Fecha

### Booleanos


### Binarios


### Geográficos


### Complejos


### Otros
