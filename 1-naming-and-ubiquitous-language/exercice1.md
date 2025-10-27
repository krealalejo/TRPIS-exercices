# ParcelFlow — Ejercicios

## Contexto

![Logo de Parcel](../assets/parcel-flow-logo.webp)

_ParcelFlow_ es un producto SaaS para la orquestación de última milla (_conjunto de procesos, decisiones y sistemas que coordinan todo lo necesario para que un paquete llegue desde el último punto logístico hasta el cliente_)

El producto tendrá operaciones para: gestión de pickups, asignación de carriers y drivers, seguimiento por escaneos, manejo de errores en el proceso y prueba de entrega (POD).

Este documento contiene un pequeño contexto funcional de la empresa, algunos términos de su lenguaje ubicuo y los ejercicios para practicar en clase.

## Ubiquitous Language

- **Parcel**: cada uno de los elementos que se transportan.
- **Shipment**: un conjunto de uno o más parcels que se transportan bajo un mismo tracking number.
- **TrackingNumber**: identificador único de un Shipment visible para cliente y carrier.
- **PickupRequest**: la petición de recogida que hace un cliente para que un carrier recoja un Shipment en una dirección y ventana horaria.
- **DeliveryWindow**: intervalo de tiempo (start, end) en que se solicita la entrega o recogida.
- **Carrier**: la empresa responsable de mover Shipments.
- **Distpacher**: persona de operaciones que revisa y coordina los procesos de última milla.
- **Driver**: la persona asignada por un Carrier para recoger o entregar Shipments.
- **ScanEvent** (o **Scan**): evento registrado cuando un paquete es escaneado (picked up, arrived at hub, out for delivery, delivered).
- **Hub**: instalación física donde se clasifican Shipments.
- **Stop**: un punto en RouteSegment donde el Driver se espera que pare o ejecute una o mas acciones (pickup, delivery, drop-off, hub transit).
- **RouteSegment**: parte de la ruta de un Driver (secuencia entre hubs/stops).
- **Exception**: condición inesperada que requiere intervención humana.
- **ProofOfDelivery (POD)**: firma o foto que confirma la entrega.
- **ETA**: tiempo estimado de llegada para un Shipment en un stop.

## Ejercicios

### 1 — Naming: variables & funciones

**User Story:**
_Como despachador, quiero crear una solicitud de recogida para un cliente, de modo que un transportista pueda recoger su envío dentro del plazo de entrega solicitado por el cliente._

**Tarea:** A continuación se muestra una lista de 20 nombres de variables/funciones que como developer podríamos utilizar al implementar esta US. Algunos nombres son ambiguos/demasiado genéricos, otros hacen un uso incorrecto del lenguaje ubicuo y otros están bien definidos. Indica para cada nombre **si está bien definido o no** y explica brevemente por qué.

**Lista de nombres:**

```text
1. data
2. pickupReq
3. createPickupRequest(customerId, window)
4. shipmentId
5. request
6. createShipmentRequest()
7. delivery_time
8. deliveryWindowStart
9. createPickup
10. addr
11. customer
12. assignDriverToShipment(shipmentRef)
13. carrier_id
14. validate()
15. validatePickupRequest(pickupRequest)
16. create
17. pickupWindow
18. trackingNum
19. notifyCarrierOfPickup(pickupRequest)
20. status
```

## Resultado
```text
mal demasiado genérico
No tendría que tener una abreviatura, pickupRequest
Tendría que tener el parametro deliveryWindow en vez de window
Bien / ¿y el trackingNumber?
Mal demasiado genérico
Bien
deliveryWindow
Bien
Tendría que ser el mismo que en el 3
Super mal
Bien pero no está definido
Mal, tendría que ser en vez de shipmentRef - shipmentId (el mismo que en el 4)
Bien pero está mal escrito. CarrierId
Súper genérico
Bien
Demasiado genérico
Mal, usaríamos deliveryWindow
Mal porque tiene una abreviatura, tendría que ser trackingNumber
Bien
Mal, genérico
```

### 2 — Mensajes de commit

**Tarea:** A continuación hay 20 mensajes de commit. Se deben marcar cuáles utilizan un lenguaje ubicuo y/o describen el cambio, y cuáles no, explicando el porqué

**Lista de commits:**

```text
1. fix pickup orders not showing its status when completed
2. Add pickup request validation for overlapping delivery windows
3. minor typo fixes
4. Record ScanEvent with UTC timestamp when driver scans a shipment
5. temp changes for testing
6. Rename parcel.id to trackingNumber
7. refactor parcel.id
8. Reject pickup requests outside carrier service area
9. Added second factor auth for drivers
10. Add CI config
11. Notify carrier when pickup is scheduled
12. update README
13. Handle exception when address lookup fails during pickup creation
14. changes to UI
15. Ensure motorist assignment does not exceed route capacity
16. fix bug
17. Improve error message for unavailable carriers
18. WIP new tracking
19. Add proof of delivery photo upload
20. merge branch
```

## Resultado
```text
Fix:  canviar orders por request
ok
Mal, muy genérico
quitamos utc? demasiado detalle?
Mal, no se entiende bien
? to discuss
entre el 6 y el 7 este mejor
bien
cambiar added por Add
bien
bien
bien
mal, canviar creation por request
Mal, falta especificar más
Canviar motorist por driver y ¿¿route capacity??
mal
bien
no commitear cosas wip
bien
especificar la branch
```
