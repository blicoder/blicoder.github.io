---
layout: post
title: Belajar OpenAPI Untuk Pemula
---

##Tipe Data

| type | format | comments |
| - | - | - |
| integer | int32 | signed 32 bits |
| integer | int64 | signed 64 bits (a.k.a long) |
| number | float |  |
| number | double |  |
| string |  |  |
| string | byte | base64 encoded characters |
| string | binary | any sequence of octets |
| boolean |  |  |
| string | date |  |
| string | date-time |  |
| string | password |   |

##Document

OpenAPI Object (Root Document Object)

| Field Name | Type | Description |
| - | - | - |
| openapi | string | REQUIRED |
| info | Info Object | REQUIRED |
| servers | Server Object |  |
| paths | Paths Object | REQUIRED |
| components | Components Object |  |
| security | Security Requirement Object |  |
| tags | Tag Object |  |
| externalDocs | External Documentation Object |  |

Example

```
{
  "openapi": "3.0.3",
  "info": {},
  "servers": [],
  "paths": {}
}
```

##Info

Info Object

| title | string | REQUIRED |
| description | string |  |
| termOfService | string |  |
| contact | Contact Object |  |
| license | License Object |  |
| version | string | REQUIRED |

Contact Object

| name | string |  |
| url | string |  |
| email | string |  |

License Object

| name | string |  |
| url | string |  |

##Server

Server Object

| url | string |  |
| description | string |  |
| variables | Map[string, Server Variable Object] |  |

##External Documentation

External Documentation Object

| description | string |  |
| url | string | REQUIRED |

##Path

Path Object

| /{path} | Path Item Object |  |

Path Item Object

| $ref | string |  |
| summary | string |  |
| description | string |  |
| servers | Server Object |  |
| parameters | Parameter Object / Reference Object |  |

Path Operation

| get | Operation Object |  |
| put | Operation Object |  |
| post | Operation Object |  |
| delete | Operation Object |  |
| options | Operation Object |  |
| head | Operation Object |  |
| patch | Operation Object |  |
| trace | Operation Object |  |

##Operation

Operation Object

| tags | [string] |  |
| summary | string |  |
| description | string |  |
| externalDocs | External Documentation Object |  |
| operationId | string |  |
| parameters | [Parameter Object / Reference Object] |  |
| requestBody | Request Body Object / Reference Object |  |
| responses | Responses Object | REQUIRED |
| callbacks | Map[string, Callback Object | Reference Object] |  |
| deprecated | boolean |  |
| security | [Security Requirement Object] |  |
| servers | [Server Object] |  |

##Parameter

Parameter Object

| name | string | REQUIRED |
| in | string | REQUIRED |
| description | string |  |
| required | boolean |  |
| deprecated | boolean |  |
| allowEmptyValue | boolean |  |

##Schema
Mendefinisikan struktur datanya, biasanya menggunakan JSON Schema
- JSON Schema Specification
- JSON Schema Validation

##Request Body
Memberitahu tentang schema request body yang harus dikirim ketika menggunakan RESTful API kita

Request Body Object

| description | string |  |
| content | Map[string, Media Type Object] | REQUIRED |
| required | boolean |  |

Media Type Object

| schema | Schema Object / Reference Object |  |
| example | Any |  |
| examples | Map[string, Example Object | Reference Object] |  |
| encoding | Map[string, Encoding Object] |  |

##Object Schema

##Array Schema

##Example

##Response Body

Response Body Object

| HTTP Status Code | Response Object / Reference Object |  |


##Tag

Tag merupakan fitur tambahan, dimana kita bisa grouping beberapa Path menjadi satu Tag yang sama


##Component

Component merupakan bagian dalam OpenAPI untuk menyimpan object yang bisa digunakan ulang

Ada banyak jenis component, ada schema, request, response, parameter, header, dan lain-lain

Component Object

| schemas | Map[string, Schema Object / Reference Object ] |  |
| responses | Map[string, Response Object / Reference Object] |  |
| parameters | Map[string, Parameter Object / Reference Object] |  |
| examples | Map[string, Example Object | Reference Object] |  |
| requestBodies | Map[string, Request Body Object / Reference Object] |  |
| headers | Map[string, Header Object / Reference Object] |  |
| securitySchemes | Map[string, Security Scheme Object / Reference Object] |  |
| links | Map[string, Link Object / Reference Object] |  |
| callbacks | Map[string, Callback Object / Reference Object] |  |

##Reference
OpenAPI memiliki fitur reference, dimana dengan reference kita bisa membuat reference ke data component yang sudah kita buat


#Security

Security Object

| type | string | Any |  |
| description | string | Any |  |
| name | string | apiKey | REQUIRED |
| in | string | apiKey | REQUIRED |
| scheme | string | http |  |
| bearerFormat | string | http ("bearer") |  |
| flows | OAuth, Flows, Object | oatuh2 |  |
| openIdConnectUrl | string | openIdConnect |  |