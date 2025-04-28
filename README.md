# 📚 BookCatalog - API de Gestion de Livres

Une API RESTful développée avec **Spring Boot** pour gérer un catalogue de livres, avec monitoring, documentation automatique et métriques customisées.

## 🚀 Fonctionnalités
- **CRUD complet** pour les livres (Create, Read, Update, Delete).
- **Validation** des données avec `@Valid`.
- **Monitoring** via Spring Boot Actuator.
- **Métriques personnalisées** (Micrometer) pour suivre les créations/suppressions de livres.
- **Documentation interactive** avec Swagger UI.
- **Sécurité** (optionnelle) pour Actuator et Swagger.

## 📦 Dépendances Clés
- Spring Boot 3.x
- Spring Data JPA (Base de données)
- Lombok (Réduction de code boilerplate)
- Micrometer (Métriques)
- SpringDoc OpenAPI (Swagger UI)
- Prometheus (Optionnel)
- Sleuth/Zipkin (Optionnel)

## 🔧 Installation
1. **Cloner le projet** :
   ```bash
   git clone https://github.com/votre-repo/book-catalog.git
   cd book-catalog
   ```

2. **Configurer la base de données** (ex: H2 ou PostgreSQL) :
   ```properties
   # application.properties
   spring.datasource.url=jdbc:h2:mem:bookdb
   spring.datasource.username=sa
   spring.datasource.password=
   ```

3. **Lancer l'application** :
   ```bash
   ./mvnw spring-boot:run
   ```

## 🌐 Endpoints
| Méthode | Endpoint          | Description                |
|---------|-------------------|----------------------------|
| GET     | `/api/books`      | Liste tous les livres      |
| GET     | `/api/books/{id}` | Récupère un livre par ID   |
| POST    | `/api/books`      | Crée un nouveau livre      |
| PUT     | `/api/books/{id}` | Met à jour un livre        |
| DELETE  | `/api/books/{id}` | Supprime un livre          |

## 📊 Monitoring & Métriques
### Actuator Endpoints
- `/actuator/health` : Santé de l'application.
- `/actuator/metrics` : Métriques système et custom (`books.created`, `books.deleted`).
- `/actuator/prometheus` : Export des métriques pour Prometheus.

**Exemple de métrique custom** :
```java
// Compteur de livres créés
Counter.builder("books.created")
    .description("Nombre total de livres créés")
    .register(registry);
```

### Swagger UI
Accédez à la documentation interactive :  
🔗 http://localhost:8080/swagger-ui.html

## 🛠️ Configuration Avancée
### Sécuriser Actuator
```properties
# application.properties
management.endpoints.web.exposure.include=health,info,metrics
management.endpoint.health.roles=ACTUATOR_ADMIN
```

### Activer Prometheus
```properties
management.endpoints.web.exposure.include=*
management.metrics.export.prometheus.enabled=true
```

## 🐳 Docker (Optionnel)
```bash
docker build -t book-catalog .
docker run -p 8080:8080 book-catalog
```

## 📈 Dashboard Grafana
Importez le dashboard JSON pour visualiser les métriques :  
Exemple de Dashboard: https://grafana.com/grafana/dashboards/15665

## 📝 Licence
MIT License - Voir LICENSE.
