# Informe sobre Logging

Aquest document inclou informació detallada sobre la implementació i comparació de sistemes de logging.

## Exercici 3: Maneres de fer logs

| Mètode                                   | Exemple                                                                                       | Avantatges                                                                                         | Desavantatges                                                                                         |
|------------------------------------------|-----------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------|
| **Fent servir la configuració per defecte del mòdul logging** | ```python\nimport logging\nlogging.basicConfig(level=logging.INFO)\nlogging.info("Missatge de log")\n``` | - Ràpid i fàcil d'implementar.<br>- Útil per a petits projectes.                                  | - Poc flexible.<br>- Dificultat per escalar en projectes grans.<br>- Configuració estàtica.         |
| **Instanciant un objecte logger i parametritzant-lo des de programa** | ```python\nimport logging\nlogger = logging.getLogger("app_logger")\nhandler = logging.StreamHandler()\nformatter = logging.Formatter("%(asctime)s - %(levelname)s - %(message)s")\nhandler.setFormatter(formatter)\nlogger.addHandler(handler)\nlogger.setLevel(logging.DEBUG)\nlogger.info("Missatge de log")\n``` | - Permet configuracions més avançades.<br>- Flexibilitat en formats i sortides (fitxer, consola, etc.). | - Requereix més codi.<br>- Pot ser més difícil de mantenir per a projectes grans.                   |
| **Instanciant un objecte logger a partir d’una configuració emmagatzemada a fitxer** | Configuració al fitxer `logging.conf`:\n```ini\n[loggers]\nkeys=root\n[handlers]\nkeys=fileHandler\n[formatters]\nkeys=defaultFormatter\n[logger_root]\nlevel=DEBUG\nhandlers=fileHandler\n[handler_fileHandler]\nclass=FileHandler\nlevel=DEBUG\nformatter=defaultFormatter\nargs=("app.log", "w")\n[formatter_defaultFormatter]\nformat=%(asctime)s - %(levelname)s - %(message)s\n``` Codi Python: ```python\nimport logging\nimp...

--- 

## Exercici 4: Llibreries de logs en altres llenguatges

| **Característica**                     | **Llenguatge 1: Java**                         | **Llenguatge 2: JavaScript** (Node.js)            |
|----------------------------------------|-----------------------------------------------|--------------------------------------------------|
| **Nom de la llibreria**                | Log4j                                          | Winston                                          |
| **És nativa del llenguatge?**          | No                                             | No                                               |
| **URL per descarregar-se la llibreria**| [Log4j](https://logging.apache.org/log4j/2.x/) | [Winston](https://github.com/winstonjs/winston) |
| **Inicialització de l’objecte logger** | ```java\nLogger logger = LogManager.getLogger(Main.class);\n``` | ```javascript\nconst { createLogger, transports, format } = require('winston');\nconst logger = createLogger({\n  level: 'info',\n  transports: [new transports.Console()] });\n``` |
| **Nivells de log disponibles**         | TRACE, DEBUG, INFO, WARN, ERROR, FATAL         | error, warn, info, http, verbose, debug, silly   |
| **Mètode per fer log**                 | ```java\nlogger.info("Missatge de log");\n```  | ```javascript\nlogger.info("Missatge de log");\n``` |
| **Tipus de manegadors (pantalla, fitxer, etc.)** | Consola (`ConsoleAppender`), Fitxer (`FileAppender`), Base de dades | Consola (`Console`), Fitxer (`File`), HTTP       |
| **Identificar els seus noms a l’API**  | `ConsoleAppender`, `FileAppender`, `RollingFileAppender` | `Console`, `File`, `Http`, `Stream`             |
| **Opcions de format**                  | Personalitzable amb patrons (`PatternLayout`), JSON | Formats predefinits (`format.simple()`, `format.json()`) i personalitzats. |
