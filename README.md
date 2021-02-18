# Desafío de Donaciones Fullstack JS

El desafío consiste en lo siguiente:

-	Existe un servicio REST que llamaremos Organizaciones sin fines de lucro OSL.
	-	El servicio responde a la consulta un listado de organizaciones sin fines de lucro. Cada uno de estos registros contiene datos de la organización como el nombre, una descripción, sus datos bancarios, los montos que reciben como donación, los días que pueden recibir donación y el medio por el cúal reciben las donaciones.
	-	Cada organización puede recibir donaciones en las fechas que indica su registro junto con todas las fechas de las organizaciones listadas anteriormente.

Este es un ejemplo de la respuesta que entrega este servicio:
```json
[
  {
    "name": "Facebook INC",
    "description": "Facebook es una red social sin fines de lucro que ayuda a conectar personas alrededor del mundo",
    "founded": "2004",
    "owner": "Mark Zuckerberg",
    "contact": "contact@facebook.com",
    "bank_data": {
      "name": "Bank of China",
      "account": "000345654640"
    },
    "donation_type": [
      "bank transfer",
      "credit card",
      "debit card"
    ],
    "donation_amounts": [
      "1000",
      "5000",
      "10000"
    ],
    "donation_dates": [
      "1",
      "13",
      "17",
      "21",
      "30"
    ]
  },
  {
    "name": "Apple INC",
    "description": "Apple es una empresa de innovación dedicada a brindar objetos tecnológicos a empresas de pocos recursos",
    "founded": "1976",
    "owner": "Tim Cook",
    "contact": "contacto@apple.com",
    "bank_data": {
      "name": "Deutsche Bank",
      "account": "00052252123"
    },
    "donation_type": [
      "credit card",
      "debit card"
    ],
    "donation_amounts": [
      "2000",
      "3000",
      "7000"
    ],
    "donation_dates": [
      "5",
      "12",
      "19",
      "23",
      "31"
    ]
  },
  {
    "name": "Microsoft INC",
    "description": "Microsoft es una empresa de tecnología que apunta a desarrollar talentos de personas en situación de riesgo económico",
    "founded": "1975",
    "owner": "Bill Gates",
    "contact": "contacto@microsoft.com",
    "bank_data": {
      "name": "Banco Santander",
      "account": "000122323431"
    },
    "donation_type": [
      "bank transfer"
    ],
    "donation_amounts": [
      "5000",
      "10000",
      "15000"
    ],
    "donation_dates": [
      "2",
      "6",
      "8",
      "10"
    ]
  }
]
```

Acá se puede apreciar que el servicio generó 3 organizaciones con sus respectivos datos (Facebook, Apple y Microsoft) cada uno con sus montos para recibir. Los números en donation dates son los dias del mes en que la institución puede recibir donaciones. Recordamos que estos son acumulativos a través de las organizaciones, es decir:

Facebook INC: 1, 13, 17, 21, 30
Apple INC: 1, 13, 17, 21, 30 + 5, 12, 19, 23, 31
Microsft INC: 1, 13, 17, 21, 30 + 5, 12, 19, 23, 31 + 2, 6, 8, 10


Una versión del OSL se encuentra en :
http://desafio.helpnet.cl/osl

## EJERCICIO :

Se deberá generar una interfaz que con los datos del servicio permita lo siguiente:
- Seleccionar Organización a la cuál se le desea donar
- Ingresar los datos de la persona que esta donando (RUT, Nombre, Apellidos, Dirección, Email, Teléfono, Región y País). Estos datos son obligatorios y deben ser validados
- Según la organización seleccionada la persona deberá elegir el tipo de canal de donación segun los tipos disponibles. Una vez seleccionado el tipo de canal apareceran distintos formaularios. 

  Transferencia: La persona deberá ingresar los datos de su banco: Nombre Banco, Tipo de cuenta, N° Cuenta, Clave Bancaria
  
  Tarjeta de credito: La persona deberá ingresar los datos de su tarjeta: N° de Tarjera ( Se debe identificar si es Visa o Mastercard), Fecha de vencimiento, CVC
  
  Tarjeta de Débito: La persona debería ingresar los datos de su tarjeta: Banco que emite, N° Tarjeta, Clave Bancaria, Clave de Transferencia
  
Una vez seleccionado el tipo de transacción y esten completados los datos de esta la persona, esta deberá ingresar el monto, en caso que el monto no coincida con los permitidos se deberá calcular si es un múltiplo de alguno de estos y mencionarle que se realizaran N transacciones del valor aceptado para lograr la cantidad que desea donar. En caso contrario la donación no debe ser permitida y los montos permitidos se mostraran a la persona.

Cada una de las transacciones debera ser guardada en una base de datos Mysql almacenando los datos de la persona, la donación con su respectivo detalle y la organización a la que va esta (nombre y contacto) junto con los respectivos datos bancarios debido a que estos podrían cambiar en la API.


NOTAS:

- Las organizaciones desplegadas en el servicio podrían cambiar
- Puede que una organización no permita donaciones
- En caso de que la persona ingrese sus datos personales ( al menos el RUT ) y no complete la donación, se deberá guardar como una transacción abandonada capturando la mayor cantidad de datos personales de la persona.
- En caso de que la persona sea un donador recurrente se deberán traer sus datos personales según la última donación realizada una vez ingresado el RUT

REQUISITOS:

-	Se deben implementar la solucione en Angular 8, NodeJS con Express y base de datos MySQL.
-	La solución debe ser enviada vía un pull request a este repositorio.
-	La solución debe contener un README.md con las instrucciones para compilar e instalar.
-	Si  puedes utilizar Dockers para entregar la solución sumaras puntos pero no es un requisito.


ACLARACIÓN:
Todos los pull request serán rechazados, esto no quiere decir que ha sido rechazada la solución, sino que es una forma de que otros postulantes no copien tu código.
