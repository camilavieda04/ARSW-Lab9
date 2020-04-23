### Escuela Colombiana de Ingeniería
### Arquitecturas de Software - ARSW

## Escalamiento en Azure con Maquinas Virtuales, Sacale Sets y Service Plans

### Dependencias
* Cree una cuenta gratuita dentro de Azure. Para hacerlo puede guiarse de esta [documentación](https://azure.microsoft.com/en-us/free/search/?&ef_id=Cj0KCQiA2ITuBRDkARIsAMK9Q7MuvuTqIfK15LWfaM7bLL_QsBbC5XhJJezUbcfx-qAnfPjH568chTMaAkAsEALw_wcB:G:s&OCID=AID2000068_SEM_alOkB9ZE&MarinID=alOkB9ZE_368060503322_%2Bazure_b_c__79187603991_kwd-23159435208&lnkd=Google_Azure_Brand&dclid=CjgKEAiA2ITuBRDchty8lqPlzS4SJAC3x4k1mAxU7XNhWdOSESfffUnMNjLWcAIuikQnj3C4U8xRG_D_BwE). Al hacerlo usted contará con $200 USD para gastar durante 1 mes.

### Parte 0 - Entendiendo el escenario de calidad

Adjunto a este laboratorio usted podrá encontrar una aplicación totalmente desarrollada que tiene como objetivo calcular el enésimo valor de la secuencia de Fibonnaci.

**Escalabilidad**
Cuando un conjunto de usuarios consulta un enésimo número (superior a 1000000) de la secuencia de Fibonacci de forma concurrente y el sistema se encuentra bajo condiciones normales de operación, todas las peticiones deben ser respondidas y el consumo de CPU del sistema no puede superar el 70%.

### Escalabilidad Serverless (Functions)

1. Cree una Function App tal cual como se muestra en las  imagenes.

![](images/part3/part3-function-config.png)

![](images/part3/part3-function-configii.png)

2. Instale la extensión de **Azure Functions** para Visual Studio Code.

![](images/part3/part3-install-extension.png)

3. Despliegue la Function de Fibonacci a Azure usando Visual Studio Code. La primera vez que lo haga se le va a pedir autenticarse, siga las instrucciones.

![](images/part3/part3-deploy-function-1.png)

![](images/part3/part3-deploy-function-2.png)

4. Dirijase al portal de Azure y pruebe la function.

![](images/part3/part3-test-function.png)

   - Verificamos que la función se ejecute correctamente:
      ![image](https://user-images.githubusercontent.com/44879884/80004128-91376700-8487-11ea-8157-c24af1db891e.png)
      ![image](https://user-images.githubusercontent.com/44879884/80004141-95638480-8487-11ea-8aca-1dcaf6327d9e.png)

5. Modifique la coleción de POSTMAN con NEWMAN de tal forma que pueda enviar 10 peticiones concurrentes. Verifique los resultados y presente un informe.

   - Se crea la colección de POSTMAN
   
      ![image](https://user-images.githubusercontent.com/44879884/80011977-38210080-8492-11ea-9750-2968fbc636a0.png)
      
   - Se verifica la información de la función en azure
   
      ![image](https://user-images.githubusercontent.com/44879884/80011749-e7110c80-8491-11ea-8d5d-17ac65658450.png)
   
   - Se ejecuta newman con 10 peticiones
   
      ![image](https://user-images.githubusercontent.com/44879884/80012218-95b54d00-8492-11ea-9304-d3721fc5c281.png)

6. Cree una nueva Function que resuleva el problema de Fibonacci pero esta vez utilice un enfoque recursivo con memoization. Pruebe la función varias veces, después no haga nada por al menos 5 minutos. Pruebe la función de nuevo con los valores anteriores. ¿Cuál es el comportamiento?.

**Preguntas**

* ¿Qué es un Azure Function?
  Es un servicio de cómputo sin servidor que le permite ejecutar código activado por eventos sin     tener que aprovisionar o administrar explícitamente la infraestructura.  
* ¿Qué es serverless?
   Es un modelo de ejecución de computación en la nube en el que el proveedor de la nube ejecuta el    servidor y administra dinámicamente la asignación de recursos de la máquina. 
* ¿Qué es el runtime y que implica seleccionarlo al momento de crear el Function App?
   Ofrece una nueva forma de aprovechar la simplicidad y flexibilidad del modelo de programación de    Azure Functions en las instalaciones. Se implementa localmente para proporcionar una experiencia    de desarrollo casi idéntica a la del servicio en la nube. 
   El runtime le proporciona una forma de experimentar Azure Functions antes de comprometerse con      la nube. De esta manera, los activos de código que construye se pueden llevar con usted a la        nube cuando migra. 
* ¿Por qué es necesario crear un Storage Account de la mano de un Function App?
   Contiene todos sus objetos de datos de Azure Storage: blobs, archivos, colas, tablas y discos.      Proporciona un espacio de nombre único para sus datos de Azure Storage al que se puede acceder      desde cualquier lugar del mundo a través de HTTP o HTTPS. Los datos de la cuenta son duraderos y    altamente disponibles, seguros, escalables de forma masiva. 
* ¿Cuáles son los tipos de planes para un Function App?, ¿En qué se diferencias?, mencione ventajas y desventajas de cada uno de ellos.
   - Plan de consumo: Azure proporciona todos los recursos computacionales necesarios. No tiene que      preocuparse por la administración de recursos y solo paga por el tiempo que se ejecuta su          código. 
   - Plan premium: Especifica una cantidad de instancias precalentadas que siempre están en línea y      listas para responder de inmediato. Cuando se ejecuta su función, Azure proporciona los            recursos computacionales adicionales que se necesitan. Paga por las instancias precalentadas        que se ejecutan continuamnete y cualquier instancia adicional que se use como Azure escala su      aplicación dentro y fuera. 
   

* ¿Por qué la memoization falla o no funciona de forma correcta?
* ¿Cómo funciona el sistema de facturación de las Function App?
* Informe
