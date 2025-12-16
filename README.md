# OpenTelemetry Spring Boot Assignment

A Spring Boot REST application instrumented with OpenTelemetry to demonstrate tracing, metrics, and log correlation.

## 📋 Overview

This project showcases the integration of OpenTelemetry with a Spring Boot application, enabling comprehensive observability through automatic instrumentation. The application exposes REST endpoints and validates trace and span generation using the OpenTelemetry Java Agent.

## 🛠️ Tech Stack

- **Java**: 21
- **Spring Boot**: 3.2
- **Build Tool**: Maven
- **Observability**: OpenTelemetry Java Agent
- **Logging**: SLF4J + Logback
- **Testing**: Postman

## 📁 Project Structure
```
src/main/java/com/example/opentelemetry/assignment
├── controller
│   ├── HealthController.java
│   └── OrderController.java
├── dto
│   ├── ErrorResponse.java
│   ├── HealthResponse.java
│   ├── OrderRequest.java
│   └── OrderResponse.java
├── entity
│   └── Order.java
├── exception
│   └── GlobalExceptionHandler.java
├── mapper
│   └── OrderMapper.java
├── repository
│   └── OrderRepository.java
├── service
│   └── OrderService.java
├── simulation
│   ├── FailureSimulationAspect.java
│   └── SimulateFailure.java
└── Application.java
```

## 🚀 Getting Started

### Prerequisites

- Java 21 or higher
- Maven 3.6+
- OpenTelemetry Java Agent (configured in `pom.xml`)

### Run the Application
```bash
mvn spring-boot:run
```

The OpenTelemetry Java Agent is automatically attached via Maven configuration with the following properties:
- `otel.service.name=opentelemetry-assignment`
- `otel.traces.exporter=logging`
- `otel.metrics.exporter=logging`
- `otel.logs.exporter=logging`

## 🔌 API Endpoints

### Health Check
```http
GET /health
```
Returns the health status of the application.

**Response Example:**
```json
{
    "status": "ok"
}
```

### Create Order
```http
POST /orders
Content-Type: application/json

{
  "item": "visionPro",
  "price": 200000.00
}

```

**Response Example:**
```json
{
    "id": 3,
    "item": "visionPro",
    "price": 200000.00
}
```

## 📊 Observability Features

### Tracing
- ✅ Automatic trace and span creation for HTTP requests
- ✅ HTTP method, status code, and URL captured in spans
- ✅ Parent-child span relationships maintained

### Metrics
- ✅ JVM metrics (memory, CPU, threads)
- ✅ HTTP server metrics (request count, duration)
- ✅ Resource attributes configured with service name

### Logging
- ✅ Structured logging with SLF4J
- ✅ Automatic injection of `trace_id` and `span_id` via MDC
- ✅ Log-trace correlation enabled

### Failure Simulation
- ✅ Aspect-oriented failure simulation
- ✅ `@SimulateFailure` annotation for controlled error scenarios
- ✅ Trace validation during error conditions

### Log Format Example
```
2025-12-16 12:01:00 [http-nio-8080-exec-9] INFO 
                [trace_id=42e5c5f93fcc4183796843f0d325d0eb span_id=a098f8238569e52f]
                c.e.o.a.c.OrderController - GET /api/v1/orders called
```

## ✅ Validation

The following validations have been performed:

1. **API Functionality**
   - Health endpoint returns 200 OK
   - Order creation endpoint processes requests successfully

2. **Tracing Verification**
   - Trace IDs generated for each request
   - Span hierarchy correctly established
   - Span attributes contain relevant metadata

3. **Log Correlation**
   - `trace_id` and `span_id` present in application logs
   - Logs can be correlated with traces

4. **Metrics Collection**
   - JVM metrics exported (heap memory, CPU usage, thread count)


## 🔧 Configuration

### Application Properties
```properties
# Server Configuration
server.port=8080

# Application Name
spring.application.name=opentelemetry-assignment

# Logging Configuration
logging.level.root=INFO
logging.level.com.example.opentelemetry.assignment=INFO
```

### OpenTelemetry Maven Configuration
The OpenTelemetry Java Agent is configured in `pom.xml` using the `spring-boot-maven-plugin` with agent parameters. This allows automatic instrumentation without manual agent attachment.

## 📈 Future Enhancements

- [ ] Integration with Jaeger or Zipkin for trace visualization
- [ ] Prometheus metrics export
- [ ] Custom span attributes and events
- [ ] Database query tracing
- [ ] Integration tests with trace validation

## 📝 Notes

- The application uses the OpenTelemetry Java Agent for automatic instrumentation
- Agent is configured via Maven plugin for seamless development experience
- No manual agent attachment required - just run `mvn spring-boot:run`
- Logging exporter is used for development; switch to OTLP for production
