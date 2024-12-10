# NestJS Basics

## What is NestJS?

NestJS is a **progressive Node.js framework** for building efficient, reliable, and scalable server-side applications. It is built on **TypeScript** (but supports JavaScript) and uses **Express.js** or **Fastify** as a backend framework. Inspired by Angular, NestJS provides a structured way of building applications using **decorators**, **dependency injection**, and **modular architecture**.

---

## Why Use NestJS?

1. **Modular Architecture**:

   - Promotes reusable and maintainable code.
   - Applications are divided into **modules**, making the codebase easier to understand.

2. **TypeScript Support**:

   - TypeScript ensures type safety, making code more predictable and less error-prone.

3. **Dependency Injection**:

   - Handles relationships between classes, improving code scalability and testability.

4. **Built-in Features**:

   - Comes with features like **validation**, **middleware**, **guards**, and **pipes**, reducing the need for additional libraries.

5. **Flexibility**:

   - Supports various databases (SQL and NoSQL), microservices, WebSocket, and GraphQL.

6. **Integration**:
   - Works seamlessly with modern tools like **Swagger**, **TypeORM**, **Mongoose**, etc.

---

## Basic Concepts in NestJS

1. **Modules**:

   - A module is a class annotated with the `@Module()` decorator.
     ```typescript
     @Module({
       imports: [],
       controllers: [AppController],
       providers: [AppService],
     })
     export class AppModule {}
     ```

2. **Controllers**:

   - Handle HTTP requests and responses.
     ```typescript
     @Controller("users")
     export class UserController {
       @Get()
       findAll(): string {
         return "This action returns all users";
       }
     }
     ```

3. **Providers**:

   - Providers are used for dependency injection and implementing business logic.
     ```typescript
     @Injectable()
     export class UserService {
       findAll(): string[] {
         return ["user1", "user2"];
       }
     }
     ```

4. **Decorators**:

   - Special annotations like `@Controller()`, `@Get()`, and `@Injectable()` add metadata to classes and methods.

5. **Middleware**:

   - Functions executed before the route handlers.
     ```typescript
     export function logger(req, res, next) {
       console.log(`Request...`);
       next();
     }
     ```

6. **Pipes and Guards**:
   - **Pipes**: For data validation and transformation.
   - **Guards**: For handling authentication and authorization.

---

## Prerequisites for NestJS

1. **Install Node.js**:

   - Download and install Node.js from [Node.js Official Website](https://nodejs.org/).
   - Verify the installation:
     ```bash
     node -v
     npm -v
     ```

2. **Install NestJS CLI**:

   - Install the NestJS CLI globally:
     ```bash
     npm i -g @nestjs/cli
     ```

3. **Code Editor**:
   - Use **Visual Studio Code** or any editor that supports TypeScript.

---

## Setting Up a Basic NestJS Application

1. **Create a New Project**:
   ```bash
   nest new project-name
   ```
2. **Navigate to the project directory**:
   ```bash
   cd project-name
   ```
3. **Directory Structure**
   After the project is created, the directory structure looks like this:

   ```bash
   src/
     app.controller.ts  # Handles HTTP requests
     app.service.ts     # Contains business logic
     app.module.ts      # Root application module
     main.ts            # Entry point for the application
   ```

4. **Start the Application**
   Run the application in development mode:

   ```bash
   npm run start:dev
   ```

   By default, the application runs at `http://localhost:3000`.

---

## Basic Program: Hello World in NestJS

**main.ts**

The entry point of the application:

```bash
import { NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';

async function bootstrap() {
    const app = await NestFactory.create(AppModule);
    await app.listen(3000);
}
bootstrap();
```

**app.module.ts**

Defines the root module of the application:

```bash
import { Module } from '@nestjs/common';
import { AppController } from './app.controller';
import { AppService } from './app.service';

@Module({
    imports: [],
    controllers: [AppController],
    providers: [AppService],
})
export class AppModule {}
```

**app.controller.ts**

Handles the HTTP request for the root route:

```bash
import { Controller, Get } from '@nestjs/common';
import { AppService } from './app.service';

@Controller()
export class AppController {
  constructor(private readonly appService: AppService) {}

  @Get()
  getHello(): string {
    return this.appService.getHello();
  }
}
```

**app.service.ts**

Contains the business logic for returning the "Hello World" message:

```bash
import { Injectable } from '@nestjs/common';

@Injectable()
export class AppService {
  getHello(): string {
    return 'Hello World!';
  }
}
```
