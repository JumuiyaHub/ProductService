# Product Service Microservice

A Spring Boot microservice for managing product catalog data with MongoDB integration, RESTful APIs and comprehensive documentation.

## 📋 Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Technologies](#technologies)
- [Project Structure](#project-structure)
- [Prerequisites](#prerequisites)
- [Installation & Setup](#installation--setup)
- [API Documentation](#api-documentation)
- [API Endpoints](#api-endpoints)
- [Configuration](#configuration)
- [Testing](#testing)
- [Docker Support](#docker-support)
- [Contributing](#contributing)
- [License](#license)
- [Support](#support)

## 🚀 Overview

The Product Service is a microservice built with Spring Boot that provides a comprehensive solution for managing product-related data in a distributed system architecture. It offers a RESTful API for creating, retrieving, and managing product information with MongoDB as the underlying database for efficient data persistence.

This service is designed to be:
- **Scalable**: Built with microservice architecture principles
- **Containerized**: Ready for Docker deployment
- **Well-documented**: Integrated with OpenAPI/Swagger for API documentation
- **Testable**: Comprehensive test suite with Testcontainers integration

## ✨ Features

- **Product Management**: Create and retrieve product information
- **RESTful API**: Clean, intuitive REST endpoints
- **MongoDB Integration**: NoSQL database for flexible data storage
- **API Documentation**: Interactive Swagger UI for API exploration
- **Containerization**: Docker and Docker Compose support
- **Testing**: Comprehensive test suite with integration testing
- **Production Ready**: Built with Spring Boot best practices

## 🛠 Technologies

| Technology | Version | Purpose |
|------------|---------|---------|
| **Java** | 21 | Programming language |
| **Spring Boot** | 3.5.0 | Application framework |
| **Spring Data MongoDB** | - | Database integration |
| **MongoDB** | Latest | NoSQL database |
| **Maven** | 3.6+ | Build automation |
| **Docker** | Latest | Containerization |
| **Lombok** | Latest | Reduces boilerplate code |
| **OpenAPI** | 2.8.9 | API documentation |
| **Rest-Assured** | 5.3.2 | API testing |
| **Testcontainers** | Latest | Integration testing |

## 📁 Project Structure

```
productservice/
├── docker-compose.yml                  # Docker services configuration
├── pom.xml                            # Maven dependencies and build
├── README.md                          # This file
├── LICENSE                            # Apache 2.0 License
├── HELP.md                            # Additional documentation
├── mvnw                               # Maven wrapper (Unix)
├── mvnw.cmd                           # Maven wrapper (Windows)
└── src/
    ├── main/
    │   ├── java/com/kiru/microservice/product/
    │   │   ├── ProductServiceApplication.java    # Main application
    │   │   ├── config/
    │   │   │   └── OpenAPIConfig.java           # Swagger configuration
    │   │   ├── controller/
    │   │   │   └── ProductController.java       # REST controllers
    │   │   ├── dto/
    │   │   │   ├── ProductRequest.java          # Request DTOs
    │   │   │   └── ProductResponse.java         # Response DTOs
    │   │   ├── model/
    │   │   │   └── Product.java                 # Data models
    │   │   ├── repository/
    │   │   │   └── ProductRepository.java       # Data access layer
    │   │   └── service/
    │   │       └── ProductService.java          # Business logic
    │   └── resources/
    │       ├── application.properties           # Configuration
    │       ├── static/                          # Static resources
    │       └── templates/                       # Templates
    └── test/
        └── java/com/kiru/microservice/product/
            ├── ProductServiceApplicationTests.java      # Main tests
            ├── TestcontainersConfiguration.java         # Test config
            └── TestProductserviceApplication.java       # Test application
```

## 📋 Prerequisites

Before running the application, ensure you have:

- **Java 21** or higher
- **Maven 3.6+**
- **Docker Desktop** (includes Docker Engine and Docker Compose)
- **Git** (for cloning the repository)

### Verify Prerequisites

```bash
# Check Java version
java -version

# Check Maven version
mvn -version

# Check Docker version
docker --version
docker-compose --version
```

## 🚀 Installation & Setup

### 1. Clone the Repository

```bash
git clone <repository_url>
cd productservice
```

### 2. Start MongoDB

The application requires MongoDB to be running. Use Docker Compose to start the database:

```bash
# Start MongoDB in detached mode
docker-compose up -d mongodb

# Verify MongoDB is running
docker ps
```

**MongoDB Connection Details:**
- **Host**: `localhost:27017`
- **Database**: `product-service`
- **Username**: `root`
- **Password**: `password`
- **Auth Source**: `admin`

### 3. Build the Application

```bash
# Build the project
./mvnw clean install

# On Windows
mvnw.cmd clean install
```

### 4. Run the Application

```bash
# Start the Spring Boot application
./mvnw spring-boot:run

# On Windows
mvnw.cmd spring-boot:run
```

The application will start on **http://localhost:8080**

### 5. Verify Installation

Once the application is running, you can verify it's working by:

1. **Health Check**: Visit `http://localhost:8080/actuator/health` (if actuator is configured)
2. **API Documentation**: Visit `http://localhost:8080/swagger-ui.html`
3. **Test API**: Make a GET request to `http://localhost:8080/api/product`

## 📚 API Documentation

### Swagger UI
Access the interactive API documentation at:
- **Swagger UI**: [http://localhost:8080/swagger-ui.html](http://localhost:8080/swagger-ui.html)
- **OpenAPI Spec**: [http://localhost:8080/v3/api-docs](http://localhost:8080/v3/api-docs)

The Swagger UI provides:
- Complete API endpoint documentation
- Request/response schemas
- Interactive testing capabilities
- Authentication details (if applicable)

## 🔌 API Endpoints

### Base URL
```
http://localhost:8080/api/product
```

### Endpoints

#### Create Product
- **Method**: `POST`
- **Path**: `/api/product`
- **Description**: Creates a new product in the catalog
- **Content-Type**: `application/json`

**Request Body:**
```json
{
    "name": "Smartphone X",
    "description": "A powerful smartphone with advanced features.",
    "skuCode": "SMARTPHONE-X-001",
    "price": 999.99
}
```

**Response (201 Created):**
```json
{
    "id": "60d0fe4f260384001c1c1c1c",
    "name": "Smartphone X",
    "description": "A powerful smartphone with advanced features.",
    "price": 999.99
}
```

#### Get All Products
- **Method**: `GET`
- **Path**: `/api/product`
- **Description**: Retrieves all products from the catalog

**Response (200 OK):**
```json
[
    {
        "id": "60d0fe4f260384001c1c1c1c",
        "name": "Smartphone X",
        "description": "A powerful smartphone with advanced features.",
        "price": 999.99
    },
    {
        "id": "60d0fe4f260384001d2d2d2d",
        "name": "Laptop Pro",
        "description": "High-performance laptop for professionals.",
        "price": 1499.00
    }
]
```

### Example API Calls

#### Using cURL

```bash
# Create a product
curl -X POST http://localhost:8080/api/product \
  -H "Content-Type: application/json" \
  -d '{
    "name": "Gaming Laptop",
    "description": "High-performance gaming laptop",
    "skuCode": "GAMING-LAPTOP-001",
    "price": 1299.99
  }'

# Get all products
curl -X GET http://localhost:8080/api/product
```

#### Using HTTPie

```bash
# Create a product
http POST localhost:8080/api/product \
  name="Gaming Laptop" \
  description="High-performance gaming laptop" \
  skuCode="GAMING-LAPTOP-001" \
  price:=1299.99

# Get all products
http GET localhost:8080/api/product
```

## ⚙️ Configuration

### Application Properties

The application is configured through `src/main/resources/application.properties`:

```properties
# MongoDB Configuration
spring.data.mongodb.uri=mongodb://root:password@localhost:27017/product-service?authSource=admin

# Swagger Configuration
springdoc.swagger-ui.path=/swagger-ui.html
springdoc.api-docs.path=/v3/api-docs

# Server Configuration
server.port=8080

# Logging Configuration
logging.level.com.kiru.microservice.product=DEBUG
```

### Environment Variables

You can override configuration using environment variables:

```bash
# MongoDB URI
export SPRING_DATA_MONGODB_URI=mongodb://username:password@host:port/database

# Server Port
export SERVER_PORT=8081
```

### Docker Environment

For Docker deployments, use environment variables in your `docker-compose.yml`:

```yaml
environment:
  - SPRING_DATA_MONGODB_URI=mongodb://root:password@mongodb:27017/product-service?authSource=admin
  - SERVER_PORT=8080
```

## 🧪 Testing

### Running Tests

```bash
# Run all tests
./mvnw test

# Run tests with coverage
./mvnw test jacoco:report

# Run specific test class
./mvnw test -Dtest=ProductServiceApplicationTests
```

### Test Categories

- **Unit Tests**: Fast, isolated tests for individual components
- **Integration Tests**: End-to-end tests using Testcontainers
- **API Tests**: REST API testing with Rest-Assured

### Testcontainers Integration

The project uses Testcontainers for integration testing, which provides:
- Real MongoDB instances for testing
- Isolated test environments
- Reliable, reproducible tests

## 🐳 Docker Support

### Docker Compose

The project includes a `docker-compose.yml` for easy development setup:

```yaml
version: '3.8'
services:
  mongodb:
    image: mongo:latest
    container_name: mongodb
    restart: always
    ports:
      - "27017:27017"
    environment:
      MONGO_INITDB_ROOT_USERNAME: root
      MONGO_INITDB_ROOT_PASSWORD: password
    volumes:
      - mongodb_data:/data/db

volumes:
  mongodb_data:
```

### Running with Docker

```bash
# Start all services
docker-compose up -d

# View logs
docker-compose logs -f

# Stop services
docker-compose down

# Clean up (removes volumes)
docker-compose down -v
```

### Building Docker Image

```bash
# Build application image
docker build -t product-service:latest .

# Run the application
docker run -p 8080:8080 product-service:latest
```

## 🤝 Contributing

Please follow these steps:

1. **Fork the repository**
2. **Create a feature branch**: `git checkout -b feature/amazing-feature`
3. **Commit your changes**: `git commit -m 'Add amazing feature'`
4. **Push to the branch**: `git push origin feature/amazing-feature`
5. **Open a Pull Request**

### Development Guidelines

- Follow Java coding conventions
- Write tests for new features
- Update documentation as needed
- Ensure all tests pass before submitting PR

### Code Style

- Use consistent indentation (4 spaces)
- Follow Spring Boot best practices
- Use meaningful variable and method names
- Add appropriate comments and documentation

## 📄 License

This project is licensed under the **Apache License 2.0**. See the [LICENSE](LICENSE) file for details.

## 🆘 Support

### Getting Help

- **Documentation**: Check the [HELP.md](HELP.md) file
- **Issues**: Open an issue on the GitHub repository
- **Discussions**: Use GitHub Discussions for questions

### Common Issues

#### MongoDB Connection Issues
```bash
# Check if MongoDB is running
docker ps

# Restart MongoDB
docker-compose restart mongodb

# Check MongoDB logs
docker-compose logs mongodb
```

#### Port Already in Use
```bash
# Find process using port 8080
lsof -i :8080

# Kill the process
kill -9 <PID>

# Or use a different port
./mvnw spring-boot:run -Dspring-boot.run.arguments=--server.port=8081
```

### Troubleshooting

1. **Build Issues**: Ensure Java 21 and Maven 3.6+ are installed
2. **Test Failures**: Check Docker is running for Testcontainers
3. **API Issues**: Verify MongoDB is accessible and running
4. **Documentation**: Ensure OpenAPI dependencies are correct