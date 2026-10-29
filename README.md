# mk96-qa-postman-collections

Colecciones de [Postman](https://www.postman.com) para probar a mano las APIs de las pruebas técnicas del repositorio [`mk96-qa-technical-tests`](https://github.com/mk96-qa/mk96-qa-technical-tests).

Todas las peticiones apuntan a `localhost`, así que primero hay que arrancar el servicio correspondiente. No usan claves, variables ni cabeceras de autorización.

## Qué hay

| Colección | Archivo | Peticiones | Servicio que prueba |
|---|---|---|---|
| **PricesDb** | `prices-db.postman_collection.json` | 6 | `prices-db`, en el puerto `8090` |
| **Similar products** | `similar-products.postman_collection.json` | 3 | `similar-products-app` (puerto `5000`) y `similar-products-mock` (puerto `3001`) |

### PricesDb

Todas son `POST http://localhost:8090/Neoris/Inditex/PricesDB/getOperatingProductRate`, con un cuerpo JSON `{ "productId", "brandId", "applicationDate" }`:

| Petición | Qué comprueba |
|---|---|
| `GetPrices1410_1_35455` | Producto 35455, marca 1, el 14 de junio de 2020 a las 10:00 |
| `GetPrices1416_1_35455` | Igual, el 14 de junio de 2020 a las 16:00 |
| `GetPrices1421_1_35455` | Igual, el 14 de junio de 2020 a las 21:00 |
| `GetPrices1510_1_35455` | Igual, el 15 de junio de 2020 a las 10:00 |
| `GetPrices1621_1_35455` | Igual, el 16 de junio de 2020 a las 21:00 |
| `GetPricesError` | Producto 1000, marca 1, el 16 de junio de 2020 a las 21:00. Pensada para probar el caso de error |

### Similar products

| Petición | Método y URL |
|---|---|
| `getSimilarProduct` | `GET http://localhost:5000/product/1/similar` |
| `getSimilaridsMock` | `GET http://localhost:3001/product/1/similarids` |
| `getProductMock` | `GET http://localhost:3001/product/1` |

La primera llama a la API real. Las otras dos llaman directamente al servicio simulado (mock) del que depende.

## Cómo usarlas

1. Arranca el servicio que quieras probar siguiendo el README de su carpeta en [`mk96-qa-technical-tests`](https://github.com/mk96-qa/mk96-qa-technical-tests).
2. En Postman, pulsa **Import** y elige el archivo `.postman_collection.json`.
3. Lanza las peticiones desde la colección importada.

Si tu servicio escucha en otro puerto, cambia la dirección en cada petición, porque las colecciones no usan variables.

## Estructura del repositorio

```
.
├── README.md
├── prices-db.postman_collection.json
└── similar-products.postman_collection.json
```
