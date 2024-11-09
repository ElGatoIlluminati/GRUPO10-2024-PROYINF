REQUERIMIENTOS PARA QUE CORRA LA PÁGINA:
*tener instalado Python y PostgreSQL.

Descargar el archivo del GitHub, descomprimirlo y abrir la carpeta, en dicha carpeta abrir apretando botón derecho abrir la power Shell (de no aparecer buscarla para abrirla) y:
-crear entorno virtual así: python -m venv nombre_del_entorno
-activar así: nombre_del_entorno\Scripts .\actívate
	**de haber error con este paso hacer:
		Set-ExecutionPolicy RemoteSigned y colocar S
		luego volver a realizar .\activate

-volver a la carpeta VIGIFIA (para retroceder ponemos cd ..)		
-ejecutar: pip install -r requirements.txt
-abrir la carpeta base Vigifia (la que contiene todos los archivos) en visual studio code, ir a la carpeta vigifia e ir a setting.py y cambiar la contraseña de database por la propia de postgressql.
-abrir pgadmin4 y crear una nueva base llamada postgres que esté vacía (solo en caso de que no esté creada y en caso de que esté creada verificar que esté vacía).
-dirigirse donde se encuentra el archivo tester en la powershell (carpeta vigifia) pg_restore -U postgres (name en database settings) -h localhost -p 5432 -d postgres tester.dump  (borrar el "(name en database setting)") y posteriormente colocar la contraseña que ocupamos en postresql.
-ya con todo lo anterior listo colocar: python manage.py runserver y dirigirse a la dirección que se muestra por consola.


Observaciones:
**si no funciona la conexión con la base de datos hay que ir al path y colocar postgres.bin**
Si en algún momento cerramos el entorno en la poweshell, este tiene que volverse a abrir para que todos los pasos puedan salir correctamente.