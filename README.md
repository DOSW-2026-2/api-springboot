# LABORATORIO 7: SPRINGBOOT - API REST

**Escuela Colombiana de Ingeniería Julio Garavito**  
**Curso:** Desarrollo y Operaciones de Software - DOSW  
**Caso de estudio:** **TechCup**

El presente laboratorio tiene como objetivo iniciar la definición del API REST para el proyecto **Oficio Ya** usando el framework Spring Boot.
El laboratorio se desarrollará en equipos correspondientes al SQUAD definido para el proyecto y consistirá en las siguientes partes:

---

## 1. Objetivo

Iniciar la definición de **API REST** para el caso de uso **Oficio Ya** usando el framework Spring Boot.
El laboratorio se desarrollará en los equipos correspondientes al **SQUAD** definido para el proyecto.

---

## PARTE 1: Estructuración del proyecto backend usando Spring Boot

Desarrolle los siguientes pasos para estructurar el backend del proyecto:

1. Usando Spring Initializr (https://start.spring.io/) creen el proyecto para el backend. Tener en cuenta:
   * Es un proyecto Maven.
   * Seleccionen la versión 4.0.3 (o la más reciente estable) de Spring Boot.
   * Defina la metadata adecuada para el proyecto (ej. `edu.eci.dosw.oficioya`). 
   * Verifique que la versión de Java sea la 17.

   Deben obtener una estructura similar a la siguiente:

   ```text
   src
   ├── main
   │   ├── java
   │   │   └── edu.eci.dosw.oficioya
   │   │       └── OficioYaApplication.java
   │   └── resources
   │       └── application.properties
   └── test
       └── java
           └── edu.eci.dosw.oficioya
               └── OficioYaApplicationTests.java
   ```

3. Adicione al pom.xml las siguientes dependencias:
   * JUnit
   * JaCoCo
   * Sonarqube
  
4. Complementen la estructura anterior con las siguiente estructura de carpetas:

```text
project/
├── src/
│   ├── main/
│   │   ├── java/
│   │   │   └── edu/eci/dosw/oficioya/
│   │   │       ├── OficioYaApplication.java 
│   │   │       ├── config/         # Configuración (Security, Web, etc.)
│   │   │       ├── controller/     # REST controllers (@RestController)
│   │   │       ├── service/        # Lógica de negocio (@Service)
│   │   │       ├── repository/     # Acceso a datos (@Repository / JPA)
│   │   │       ├── entity/         # Entidades JPA (Base de datos)
│   │   │       ├── model/          # Entidades centrales del negocio
│   │   │       ├── dto/            # Objetos de transferencia
│   │   │       └── exception/      # Manejo de excepciones (@ControllerAdvice)
│   │   └── resources/
│   │       ├── application.properties
│   │       └── docs/
│   │           ├── uml/
│   │           ├── images/
│   │           └── requirements/
│   └── test/
│       └── java/                   # Tests (misma estructura de paquetes)
├── pom.xml                         # Configuración Maven
└── README.md
```

3. Cree la rama `feature/scafolding`.
4. Realice un PR desde la rama `feature/scafolding` a `develop`.
5. El PR debe ser revisado y aprobado por alguno de los integrantes del equipo, diferente a quien lo generó.

---

# PARTE 2 - Preguntas

En el archivo `README.md`, dé respuesta a las siguientes preguntas:

1. ¿Para qué sirve el paquete `Controller` en la estructura Spring Boot?
2. ¿Para qué sirve el paquete `Service` en la estructura Spring Boot?
3. ¿Para qué sirve el paquete `Model` en la estructura Spring Boot?
4. ¿Para qué sirve el paquete `Repository` en la estructura Spring Boot?
5. ¿Para qué sirve el paquete `Entity` en la estructura Spring Boot?
6. ¿Para qué sirve el paquete `DTO` en la estructura Spring Boot?
7. ¿Para qué sirve el paquete `Exception` en la estructura Spring Boot?

Adicione la bibliografía en normas APA.

7. Realice un PR desde la rama `feature/springboot-questions` a develop.
8. El PR debe ser revisado y aprobado por un integrante diferente.

---

# PARTE 3 - DIAGRAMA DE CLASES A IMPLEMENTACIÓN

1. Diseñe la primera versión del Diagrama de Clases (solo atributos, sin métodos) del proyecto **Oficio Ya**. El diagrama debe estar en estándar UML.
2. Identifique las clases que permiten cumplir los requerimientos asociados con:
   * **Trabajadores (CRUD)**.
   * **Autenticación**

3. Adicione imagen del Diagrama de Clases al archivo `README.md`.
4. Adicione el Diagrama de Clases a la carpeta `/docs`.
5. En GitHub, Cree las clases identificadas en el paquete correspondiente dentro del proyecto.
6. Compile el proyecto y verifique que no existen errores.
7. Realice un PR desde la rama `feature/first-cycle` a develop.
8. El PR debe ser revisado y aprobado por alguno de los integrantes del equipo, diferente a quien lo generó.

---
# PARTE 4 - API PARA EL PRIMER CICLO

Para los requerimientos: Trabajadores (CRUD) realice:

1. Defina los controladores necesarios para definir los endpoints requeridos. Recuerden las siguientes reglas:

   **Trabajadores:**
   * Los trabajadores se crean por defecto con estado Activo.
   * Los campos `Nombre`, `correo`, `teléfono`, `oficio principal` y `contraseña` son obligatorios.
   * Los trabajadores no se pueden eliminar, solamente se puede inactivar. (Es decir, no existe operación DELETE para un trabajador).
   * La información de los trabajadores se puede modificar si su estado no es Inactivo.
   * Pueden existir solicitantes que sean contratantes también.
   * Pueden existir contratantes que sean trabajadores también.
  
  **Autenticación:**
  * El método usado será POST comparando el correo y la contraseña.
  
2. Para cada controlador no olvide adicionar las anotaciones: `@RestController` y `@RequestMapping`. Ejemplo:

   ```text
   @RestController
   @RequestMapping("/api/trabajadores")
   public class TrabajadorController {
     // ...
   }
   ```

3. En cada controlador, defina las operaciones necesarias. No olvide adicionar la anotación correspondiente dependiendo la operación y si reciben parámetros. Ejemplo:

   ```text
   @GetMapping("/{id}")
   public ResponseEntity<Trabajador> get(@PathVariable Long id) {
    // ...
   }
   ```
   **Importante:** No olvide retornar el código HTTP adecuado. Ejemplo: `ResponseEntity.status(HttpStatus.UNAUTHORIZED)`.
   
4. Defina los servicios necesarios para dar respuesta a los endpoints definidos anteriormente. **Nota:** No olvide el uso de la anotación `@Service`. Teniendo en cuenta que no tenemos persistencia implementada en este momento, realice:

  * Métodos GET: Cree objetos dummy del modelo que desea consultar. Ejemplo:

    ```text
    @Service
    public class UserService {
        private final List<User> users = new ArrayList<>();
        private final AtomicLong idGenerator = new AtomicLong(1);
    
        public UserService() {
            // Datos iniciales simulados
            users.add(new User(1L, "Usuario Demo", "demo@ejemplo.com"));
        }
    
        public List<User> findAll() {
            return new ArrayList<>(users);
        }
    }
    ```
 * Métodos POST: Retorne un nuevo objeto del modelo para simular que fue creado. Ejemplo:

   ```text
   public Worker create(Worker worker) {
     worker.setId(idGenerator.getAndIncrement());
     workers.add(worker);
     return worker;
   }
   ```

 *  Métodos PUT: Realice la simulación con alguno de los objetos creados en el constructor del modelo correspondiente. Ejemplo:

   ```text
   public Optional<Worker> update(Long id, Worker worker) {
    for (int i = 0; i < workers.size(); i++) {
        if (worker.get(i).getId().equals(id)) {
            worker.setId(id);
            worker.set(i, worker);
            return Optional.of(worker);
        }
    }
    return Optional.empty();
   }
   ```
 * Métodos DELETE: Realice la simulación con alguno de los objetos creados en el constructor del modelo correspondiente. Ejemplo:

   ```text
   public boolean delete(Long id) {
    return workers.removeIf(u -> u.getId().equals(id));
   }
   ```
5. Realice un PR desde la rama `feature/api-rest-first-cycle` a develop.
6. El PR debe ser revisado y aprobado por alguno de los integrantes del equipo, diferente a quien lo generó.

---
# PARTE 5 - SWAGGER - DOCUMENTAR API

Documentar el API construido anteriormente realizando:

1. En el `pom.xml`, agregar la dependencia de `sprindoc-openapi`:

   ```text
   <dependency>
      <groupId>org.springdoc</groupId>
      <artifactId>springdoc-openapi-starter-webmvc-ui</artifactId>
      <version>2.6.0</version>
    </dependency>
   ```
2. Anotar los controladores, permitiendo describir mejor los endpoints implementados. Ejemplo:
  
   ```text
    import org.springframework.web.bind.annotation.*;
    import io.swagger.v3.oas.annotations.Operation;
    import io.swagger.v3.oas.annotations.tags.Tag;
    
    @RestController
    @RequestMapping("/workers")
    @Tag(name = "Workers", description = "Operaciones relacionadas con trabajadores")
    public class WorkerController {
    
        @GetMapping("/{id}")
        @Operation(summary = "Obtener trabajador por ID", description = "Devuelve un trabajador")
        public Worker getWorkerById(@PathVariable Long id) {
            return new User(id, "Andres Cantor", "andres@example.com");
        }
    
        @PostMapping
        @Operation(summary = "Crear un nuevo trabajador", description = "Registra un trabajador")
        public User createUser(@RequestBody Worker worker) {
            worker.setId(100L);
            return worker;
        }
    }
   ```
   
3. Personalizar la información general de la API creando una clase de configuración para definir título y versión. Ejemplo:

   ```text
    import io.swagger.v3.oas.models.OpenAPI;
    import io.swagger.v3.oas.models.info.Info;
    import org.springframework.context.annotation.Bean;
    import org.springframework.context.annotation.Configuration;
    
    @Configuration
    public class SwaggerConfig {
        @Bean
        public OpenAPI customOpenAPI() {
            return new OpenAPI()
                    .info(new Info()
                    .title("API de Ejemplo")
                    .version("1.0.0")
                    .description("Documentación interactiva con Swagger UI"));
        }
    }
   ```
4. Probar en el navegador: Iniciar la aplicación con mvn spring-boot:run o ejecutando directamente la clase main y abrir el navegador: http://localhost:8080/swagger-ui.html
5. Tomen una captura de pantalla del Swagger generado y adiciónela en el `Readme.md`.
6. Realice un PR desde la rama `feature/swagger-first-cycle` a `develop`.
7. El PR debe ser revisado y aprobado por alguno de los integrantes del equipo, diferente a quien lo generó.

---
# PARTE 6 - LOGGER
Para los servicios implementados anteriormente, incluya el registro de acciones y errores usando SLF4J.

1. Incluya en las clases a nivel de servicio el framework de logs SLF4J. Ejemplo:

    ```text
    import org.slf4j.Logger;
    import org.slf4j.LoggerFactory;
    import org.springframework.stereotype.Service;
    
    @Service
    public class WorkerService {
        private static final Logger log = LoggerFactory.getLogger(WorkerService.class);
    
        public Worker findById(Long id) {
            log.debug("Buscando trabajador con id: {}", id);
            // ... lógica
            log.info("trabajador encontrado: {}", id);
            return worker;
        }
    }
    ```
2. Configure en el archivo `application.properties` un nombre adecuado para el archivo de logs. Ejemplo:
3. Realice un PR desde la rama `feature/logs-first-cycle` a develop.
4. El PR debe ser revisado y aprobado por alguno de los integrantes del equipo, diferente a quien lo generó.


