# Tarea

## Instrucciones
Cuando uds compran instrumentos financieros en mercados regulados, como acciones, papel de deuda guber, divisas, metales, futuros, commodities, etc 
  la instrucción que giran ustedes a su institución financiera se conoce como "postura de compra". Para que su compra se de, alguien tiene que poner 
  una postura de venta con las características suficientemente similares para poder hacerle MATCH.

El mercado es como un tanque gigante de posturas de compra y posturas de venta y un motor de matching que siempre está buscando el mejor match para una postura cualquiera.

Una vez que hay un match, entonces esa orden pasa a ejecución, pero no pasa inmediatamente. Si pasara inmediatamente, tendríamos algo como esto:

### pseudocódigo
start transaction;  
ejecutar orden mercado capitales de Julieta;  
commit;  
start transaction;  
ejecutar orden mercado divisas de Javier;  
commit;  
start transaction;  
ejecutar orden mercado deuda de Sebas 1;  
commit;  
start transaction;  
ejecutar orden mercado deuda de Sebas 2;  
commit;  
Y sabemos que esto no es muy eficiente.  

Es más eficiente tener:

start transaction;  
ejecutar orden mercado capitales 1;  
ejecutar orden mercado capitales 2;  
ejecutar orden mercado capitales 3;  
commit;  
start transaction;  
ejecutar orden mercado deuda 1;  
ejecutar orden mercado deuda 2;  
ejecutar orden mercado deuda 3;  
ejecutar orden mercado deuda 4;  
commit;  
start transaction;  
ejecutar orden mercado divisas 1;  
ejecutar orden mercado divisas 2;  
commit;  

Aún cuando dicha ejecución de ordenes esté fuera de nuestra BD

No solamente eso, sino que toda transacción de instrumentos financieros debe ir acompañado de cash. Tu institución financiera entrega 
  tus títulos o tus CETES, y tu institución financiera debe recibir de la institución financiera contraparte una suma de cash. 
  Solo que este cash viene de Banxico, por lo que es otro sistema externo con el que es difícil coordinar transacciones.

Suponiendo que tenemos los siguientes instrumentos:

capitales
deuda
divisas
Y suponiendo que los 3 mercados los tenemos en diferentes sistemas, y que para cada sistema tenemos los siguientes verbos/funciones:

transferir_capitales(origen, destino, monto)  
transferir_deuda(origan, destino, monto)  
transferir_divisas(origen, destino, monto)  
transferir_efectivo(origen, destino, monto)  

Y que como control de flujo de nuestro programa, podemos usar las siguientes funciones de pseudocódigo:

if error then para verificar errores  
if success then para verificar éxito  

Y que el único que NO SOPORTA TRANSACCIONES es el de Banxico, donde se liquida la parte de cash de todas las transacciones.

Y suponiendo que en caso de error de cualquiera de estas funciones, se hace rollback de la transacción, ¿qué secuencia de funciones 
  hipotéticas, de control, start transaction, commit y rollback se necesitan para asegurar la ejecución all or nothing de los siguientes escenarios?

Ulises con cuenta en GBM compra a Julieta con cuenta en Santander 400 títulos de AMZ (Amazon) a 66048.20 MXM pagaderos con cash.

Sebas Dulong con cuenta en Citi vende a Javier Orcazas 1200 títulos de GME (GameStop) a 3714.88 pagaderos 100 títulos de deuda gubernamental 
  con valor de 2998.12 y el restante con cash.
  
DJ Delgado con cuenta en Scotia vende 20000 USD a un exchange rate de 25.2 MXN y 300 títulos de deuda corporativa a un precio de 40032.71 a Frida Kaori 
  con cuenta en Inbursa pagaderos enteramente con cash.  
  
## Solución

Puedes usar:

transferir_capitales(origen, destino, monto)  
transferir_deuda(origan, destino, monto)  
transferir_divisas(origen, destino, monto)  
transferir_efectivo(origen, destino, monto)  

if error then para verificar errores  
if success then para verificar éxito  

1. Ulises con cuenta en GBM compra a Julieta con cuenta en Santander 400 títulos de AMZ (Amazon) a 66048.20 MXM pagaderos con cash.


  
  
  
  
  
  
