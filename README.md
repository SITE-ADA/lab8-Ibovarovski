[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/Qr3lBpHw)

# University Management System

Spring Boot microservice project for managing students, courses, and course enrollments.

## Technologies

- Java 21
- Spring Boot 3.3.5
- Spring Data JPA
- Spring Web
- Spring Validation
- Spring Cloud OpenFeign
- PostgreSQL
- Docker Compose
- Swagger/OpenAPI
- Gradle

## Services

- student-service: runs on port 9090
- course-service: runs on port 8081
- student PostgreSQL database: port 5432
- course PostgreSQL database: port 5433

## Run With Docker

```bash
docker compose up --build
```

## Run Tests

```bash
bash ./gradlew :student-service:test
bash ./gradlew :course-service:test
```

## Swagger URLs

- Student Service: http://localhost:9090/swagger-ui/index.html
- Course Service: http://localhost:8081/swagger-ui/index.html

## Example Requests

Create student:

```bash
curl -X POST http://localhost:9090/api/v1/students \
  -H "Content-Type: application/json" \
  -d '{"firstName":"Nicat","lastName":"Aliyev","email":"nicat@example.com","age":20}'
```

Create course without prerequisite:

```bash
curl -X POST http://localhost:8081/api/v1/courses \
  -H "Content-Type: application/json" \
  -d '{"title":"Programming Basics","code":"CS101","credits":4,"prerequisiteCourseId":null}'
```

Create course with prerequisite:

```bash
curl -X POST http://localhost:8081/api/v1/courses \
  -H "Content-Type: application/json" \
  -d '{"title":"Data Structures","code":"CS201","credits":4,"prerequisiteCourseId":1}'
```

Enroll student:

```bash
curl -X POST http://localhost:8081/api/v1/courses/1/students/1
```

Get students in a course:

```bash
curl http://localhost:8081/api/v1/courses/1/students
```

Search students by name:

```bash
curl "http://localhost:9090/api/v1/students/search?name=Nicat"
```

Get courses by student name:

```bash
curl "http://localhost:8081/api/v1/courses/by-student-name?name=Nicat"
```

## Notes

- Enrollment date is stored when a student is enrolled into a course.
- Courses may have an optional prerequisite course ID.
- If a course has a prerequisite, the student must already be enrolled in that prerequisite course.
- Swagger documentation is written in Azerbaijani.
