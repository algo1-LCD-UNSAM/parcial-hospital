# Parcial Hospital
En un hospital se está diseñando un nuevo sistema el cual gestionará la carga de recetas y su
procesamiento. En principio, el sistema incorporará profesionales de la salud (médicxs) con cierta
especialidad, pero por el momento no diferenciaremos. Un profesional siempre tendrá una matrícula
propia y única dentro del sistema y un nombre. Al momento de incorporar un profesional se debe
verificar si ya existe registrado contemplando su matrícula. Lxs profesionales pueden recetar estudios a
pacientes del hospital.  
Lxs pacientes tienen un número de dni que lxs identifica y un un nombre. Para inscribir al paciente al
hospital, se debe verificar que no exista previamente en el mismo (considerando el dni).  
Las recetas se componen de un identificador numérico único en todo el sistema del hospital. Al
momento de recetar, un profesional puede incluir varios estudios que deberá realizarse al paciente. Una
receta sólo puede estar dirigida a un paciente específico y cuando se carga inicialmente queda
pendiente de procesamiento, es decir, está disponible para procesar. Esta operación de procesar una
receta representa el momento en que el paciente se dirige a realizar los estudios de la misma. Se recibe
la receta, se valida que no haya sido procesada previamente y se efectúan los estudios
correspondientes. Una vez procesada, una receta no puede volver a procesarse.  
Los estudios se dividen en distintas categorías, por ejemplo estudio de imagen, laboratorio, etc. Todos
los estudios tienen un nombre, una descripción y un estado para saber si fueron realizados. Se
simplifican los tipos de estudios a dos: Uno de rayos X (RX), el cual tiene también definida una zona que
describe sobre qué parte del cuerpo se realiza (tórax, abdomen, cráneo, etc). El otro es un estudio de
laboratorio que tiene definida una cantidad de items que serán analizados. Contemplar la posibilidad de
agregar otros tipos de estudios en el futuro.  
Cuando se realiza un estudio, a partir del procesamiento de la receta, se envía el resultado al médico y
al paciente. A efectos prácticos, se pide que estos “envíos” sea una simple impresión en consola
notificando que se realiza.  
Se solicita realizar lo siguiente:  
a) Implementar todas las clases necesarias que se describen en el enunciado, incluyendo los
métodos necesarios para resolver las funcionalidades solicitadas.  
b) Implementar el siguiente escenario (ver Anexo 1):  
  1) Crear un nuevo hospital llamado Pura Salud.
  2) Registrar 3 profesionales.
  3) Registrar 3 pacientes.
  4) Cargar 5 recetas utilizando profesionales y pacientes de los puntos previos.
  5) Procesar las primeras 4 recetas del punto previo.
  6) Mostrar las recetas del sistema.
  7) Mostrar sólo las recetas procesadas del sistema.
  8) Mostrar pacientes con al menos 3 estudios realizados

## Anexo 1: Ejemplo de Main
Se puede utilizar el siguiente método main para probar el ejercicio, donde ya hay un escenario armado
para verificar la funcionalidad. 
```
Hospital hospital = new Hospital("Pura Salud");
// Profesionales de salud
Profesional juana = hospital.registrarProfesional("Juana", 12345);
Profesional ana = hospital.registrarProfesional("Ana", 11234);
Profesional maria = hospital.registrarProfesional("Maria", 54321);
// Pacientes
Paciente pedro = hospital.registrarPaciente("Pedro", 35234111);
Paciente tomas = hospital.registrarPaciente("Tomas", 34942999);
Paciente juan = hospital.registrarPaciente("Juan", 32912000);
// Recetas
Receta receta1 = hospital.cargarReceta(juana, pedro, new Estudio[] {
new EstudioRX("columna"),
new EstudioRX("torax")
});
Receta receta2 = hospital.cargarReceta(juana, tomas, new Estudio[] {
new EstudioRX("abdomen"),
new EstudioRX("torax")
});
Receta receta3 = hospital.cargarReceta(ana, juan, new Estudio[] {
new EstudioRX("abdomen"),
new EstudioLaboratorio(5)
});
Receta receta4 = hospital.cargarReceta(ana, pedro, new Estudio[] {
new EstudioLaboratorio(15)
});
Receta receta5 = hospital.cargarReceta(maria, juan, new Estudio[] {
new EstudioRX("columna"),
new EstudioRX("abdomen"),
new EstudioLaboratorio(10)
});
// Procesamiento
hospital.procesar(receta1);
hospital.procesar(receta2);
hospital.procesar(receta3);
hospital.procesar(receta4);
// Mostrar recetas
hospital.mostrarRecetas();
// Mostrar recetas procesadas
hospital.mostrarRecetasProcesadas();
// Mostrar pacientes con al menos 2 estudios realizados
hospital.mostrarPacientesConEstudios(3);
```
## Anexo 2: Ejemplo de salida de consola
Dado el ejemplo del main previo, se podría obtener una salida similar a la siguiente. No es necesario se
cumpla con el formato propuesto, simplemente se adjunta para verificar los datos del ejemplo. 
### Salida de procesar recetas
```
Notificando a paciente Pedro [35234111] sobre RX: Estudio de imagen RX de columna (REALIZADO)
Notificando a profesional Juana [12345] sobre RX: Estudio de imagen RX de columna (REALIZADO)
Notificando a paciente Pedro [35234111] sobre RX: Estudio de imagen RX de torax (REALIZADO)
Notificando a profesional Juana [12345] sobre RX: Estudio de imagen RX de torax (REALIZADO)
Notificando a paciente Tomas [34942999] sobre RX: Estudio de imagen RX de abdomen (REALIZADO)
Notificando a profesional Juana [12345] sobre RX: Estudio de imagen RX de abdomen (REALIZADO)
Notificando a paciente Tomas [34942999] sobre RX: Estudio de imagen RX de torax (REALIZADO)
Notificando a profesional Juana [12345] sobre RX: Estudio de imagen RX de torax (REALIZADO)
Notificando a paciente Juan [32912000] sobre RX: Estudio de imagen RX de abdomen (REALIZADO)
Notificando a profesional Ana [11234] sobre RX: Estudio de imagen RX de abdomen (REALIZADO)
Notificando a paciente Juan [32912000] sobre Laboratorio: Estudio de laboratorio (REALIZADO)
Notificando a profesional Ana [11234] sobre Laboratorio: Estudio de laboratorio (REALIZADO)
Notificando a paciente Pedro [35234111] sobre Laboratorio: Estudio de laboratorio (REALIZADO)
Notificando a profesional Ana [11234] sobre Laboratorio: Estudio de laboratorio (REALIZADO)
```
### Salida de recetas del sistema
```
Recetas de Pura Salud:
Receta 1:
- Profesional: Juana [12345]
- Paciente: Pedro [35234111]
- Estado: PROCESADA
- Estudios:
- RX: Estudio de imagen RX de columna (REALIZADO)
- RX: Estudio de imagen RX de torax (REALIZADO)
Receta 2:
- Profesional: Juana [12345]
- Paciente: Tomas [34942999]
- Estado: PROCESADA
- Estudios:
- RX: Estudio de imagen RX de abdomen (REALIZADO)
- RX: Estudio de imagen RX de torax (REALIZADO)
Receta 3:
- Profesional: Ana [11234]
- Paciente: Juan [32912000]
- Estado: PROCESADA
- Estudios:
- RX: Estudio de imagen RX de abdomen (REALIZADO)
- Laboratorio: Estudio de laboratorio (REALIZADO)
Receta 4:
- Profesional: Ana [11234]
- Paciente: Pedro [35234111]
- Estado: PROCESADA
- Estudios:
- Laboratorio: Estudio de laboratorio (REALIZADO)
Receta 5:
- Profesional: Maria [54321]
- Paciente: Juan [32912000]
- Estado: CARGADA
- Estudios:
- RX: Estudio de imagen RX de columna (PENDIENTE)
- RX: Estudio de imagen RX de abdomen (PENDIENTE)
- Laboratorio: Estudio de laboratorio (PENDIENTE)
```
### Salida de recetas procesadas del sistema
```
Recetas procesadas de Pura Salud:
Receta 1:
- Profesional: Juana [12345]
- Paciente: Pedro [35234111]
- Estado: PROCESADA
- Estudios:
- RX: Estudio de imagen RX de columna (REALIZADO)
- RX: Estudio de imagen RX de torax (REALIZADO)
Receta 2:
- Profesional: Juana [12345]
- Paciente: Tomas [34942999]
- Estado: PROCESADA
- Estudios:
- RX: Estudio de imagen RX de abdomen (REALIZADO)
- RX: Estudio de imagen RX de torax (REALIZADO)
Receta 3:
- Profesional: Ana [11234]
- Paciente: Juan [32912000]
- Estado: PROCESADA
- Estudios:
- RX: Estudio de imagen RX de abdomen (REALIZADO)
- Laboratorio: Estudio de laboratorio (REALIZADO)
Receta 4:
- Profesional: Ana [11234]
- Paciente: Pedro [35234111]
- Estado: PROCESADA
- Estudios:
- Laboratorio: Estudio de laboratorio (REALIZADO)
```
### Salida de pacientes con al menos 3 estudios
```
Pacientes con al menos 3 estudios realizados en Pura Salud:
Pedro [35234111]
```

