# CodePilot Android — prototipo 0.1.1

Aplicación Android nativa en Kotlin + Jetpack Compose para empezar a construir un asistente de programación desde el teléfono.

## Incluido
- Interfaz oscura en español: Chat, Archivos, Terminal y Ajustes.
- Selector de carpeta mediante el selector de documentos de Android.
- Explorador de archivos de texto, editor y guardado con confirmación antes de sobrescribir.
- Chat con endpoint compatible con OpenAI Chat Completions configurable (URL base, modelo y clave API).
- Terminal restringida a `pwd`, `ls`, `find` y `cat` dentro del espacio privado de la app; no es una terminal general.
- Dependencia `DocumentFile` incluida para que el explorador de carpetas compile.

## Importante: estado real
Este ZIP contiene **código fuente**, no un APK compilado. En este entorno no se verificó una compilación Android ni se probó la app en un teléfono físico. No voy a afirmar que existe un APK listo hasta que se genere y se compruebe.

La app no trae un modelo de IA ni incluye cuota de API. Para usar el chat hay que configurar un proveedor compatible y, normalmente, una clave API con facturación propia. No pegues una clave en capturas ni compartas el proyecto con la clave guardada. En este prototipo la clave se guarda en preferencias privadas de la app, pero no está cifrada; no es adecuada para guardar secretos de alto valor.

## Compilar desde Android, sin PC
1. Descarga y descomprime este ZIP en el teléfono.
2. Instala un entorno Android de compilación compatible, por ejemplo AndroidIDE, desde una fuente oficial/verificable. La disponibilidad y compatibilidad pueden variar según la versión de Android del teléfono.
3. Abre la carpeta `CodePilotAndroid` como proyecto Gradle.
4. Configura JDK 17 y Android SDK Platform 35, si el entorno permite instalarlos.
5. Sincroniza Gradle y ejecuta la tarea `:app:assembleDebug`. La primera vez necesita Internet para descargar Gradle y dependencias y puede consumir bastante almacenamiento.
6. Si termina correctamente, el APK de depuración suele quedar en `app/build/outputs/apk/debug/app-debug.apk`. Confirma que el archivo exista antes de intentar instalarlo.
7. Al instalar, Android puede pedir permiso para instalar apps desde esa fuente. Concede el permiso solo al gestor de archivos/entorno que estés usando y revócalo después si ya no hace falta.

Si AndroidIDE no es compatible con tu teléfono o no puede instalar SDK/dependencias, la alternativa es un servicio de compilación en la nube; no hace falta inventar ni descargar un APK de origen desconocido.

## Configurar el chat
- URL base: la URL del proveedor, sin `/chat/completions` al final (la app agrega esa ruta).
- Modelo: el identificador exacto aceptado por el proveedor.
- Clave: la clave del proveedor si es requerida.
- Para un servidor local en otro equipo de la misma red, usa su IP de red, no `localhost`. En esta primera versión, un endpoint HTTP local puede funcionar, pero no uses HTTP para enviar una clave real por redes no confiables.

## Limitaciones de esta versión
- No aplica automáticamente los parches sugeridos por el chat.
- Git, ejecución de pruebas y compilación de APK desde la propia app aún no están implementados.
- La terminal es de solo lectura y limitada; no ejecuta Gradle ni scripts de usuario.
- El endpoint local solo conecta con un servidor existente; no instala ni ejecuta por sí solo un modelo local.
- El código todavía necesita pruebas funcionales y una revisión de seguridad antes de uso diario.

## Entorno de referencia
- JDK 17
- Android SDK Platform 35
- Android Gradle Plugin 8.7.3
- Kotlin 2.0.21
