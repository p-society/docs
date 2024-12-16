### **Tree Structure of the Repository**

```
.
├── .env
├── .eslintrc.js
├── .gitignore
├── .prettierrc
├── LICENSE
├── README.md
├── nest-cli.json
├── package.json
├── package-lock.json
├── tsconfig.build.json
├── tsconfig.json
├── yarn.lock
├── env/
│   ├── Dockerfile
│   ├── env.development.txt
│   ├── env.production.txt
│   └── index.js
├── generate/
│   ├── controller.js
│   ├── controller.spec.js
│   ├── createFileWithContent.js
│   ├── dto.js
│   ├── index.js
│   ├── module.js
│   ├── schema.js
│   ├── service.js
│   └── service.spec.js
├── src/
│   ├── app.controller.ts
│   ├── app.controller.spec.ts
│   ├── app.module.ts
│   ├── app.service.ts
│   ├── common/
│   │   ├── EnsureObjectId.ts
│   │   ├── featherify.ts
│   │   ├── generate-random-number.ts
│   │   ├── get-class-properties.ts
│   │   ├── global-service.ts
│   │   ├── mailer.ts
│   │   ├── options.ts
│   │   ├── query.utils.ts
│   │   └── soft-delete-schema.ts
│   ├── constants/
│   │   └── roles-enum.ts
│   ├── decorators/
│   │   └── ModifyBody.decorator.ts
│   ├── filters/
│   │   ├── global-exception.filter.ts
│   │   └── mongo-error.filter.ts
│   ├── main.ts
│   ├── services/
│   │   ├── apis/
│   │   │   ├── auth/
│   │   │   ├── mailer/
│   │   │   ├── otp/
│   │   │   ├── redis/
│   │   │   ├── sendOtp/
│   │   │   └── users/
│   │   └── gateways/
│   │       └── presence/
│   ├── types/
│       ├── PaginatedResponse.d.ts
│       ├── QueryOptions.d.ts
│       ├── SocketClient.d.ts
│       └── SocketIOMiddleware.d.ts
└── test/
    ├── app.e2e-spec.ts
    └── jest-e2e.json
```

---

### **Documentation of Folders and Files**

#### **Root Files**

- **`.env`**: Contains environment variable configurations.
- **`.eslintrc.js`**: ESLint configuration file for enforcing code style and linting rules.
- **`.gitignore`**: Specifies files and directories to be ignored by Git.
- **`.prettierrc`**: Configuration file for Prettier, a code formatting tool.
- **`LICENSE`**: Specifies the license under which the project is distributed.
- **`README.md`**: Provides an overview of the project, setup instructions, and usage details.
- **`nest-cli.json`**: Configuration for NestJS CLI tools.
- **`package.json`** and **`yarn.lock`**: Manage project dependencies and scripts.
- **`tsconfig.json`** and **`tsconfig.build.json`**: TypeScript configurations for development and production builds.

---

#### **`env/`**

Contains environment-specific configurations:

- **`Dockerfile`**: Used to containerize the application.
- **`env.development.txt`** and **`env.production.txt`**: Store environment-specific variables.
- **`index.js`**: A utility script for loading environment configurations.

---
#### **`generate/`**

The `generate` folder automates the creation of CRUD APIs in a NestJS project. By running a simple command like:

```bash
yarn generate studentsApi
```

developers can quickly generate essential components such as controllers, services, modules, DTOs, and schemas. This speeds up development, ensures consistency, and reduces boilerplate code, allowing developers to focus on business logic rather than repetitive setup tasks.

**Warning:** Currently, the `generate` script cannot generate gateways or custom APIs.

- **`controller.js`**: Script to generate a new controller file.
- **`controller.spec.js`**: Script to generate test files for controllers.
- **`createFileWithContent.js`**: Helper to create a file with pre-defined content.
- **`dto.js`**: Script to generate a Data Transfer Object (DTO).
- **`index.js`**: Entry point for the generator scripts.
- **`module.js`**: Script to generate a new module file.
- **`schema.js`**: Script to generate schema definitions.
- **`service.js`**: Script to generate service files.
- **`service.spec.js`**: Script to generate test files for services.



---

#### **`src/`**

The main source code directory for the application:

- **`app.controller.ts`**: Handles HTTP requests for the root application route.
- **`app.module.ts`**: Root module of the application.
- **`app.service.ts`**: Core application logic.
- **`main.ts`**: Entry point for the NestJS application.

##### **Subfolders in `src/`**

1. **`common/`**:
    
    - Utility functions, reusable components, and shared services (e.g., `mailer.ts` for sending emails, `soft-delete-schema.ts` for handling soft deletes).
2. **`constants/`**:
    
    - **`roles-enum.ts`**: Enum definitions for user roles.
3. **`decorators/`**:
    
    - **`ModifyBody.decorator.ts`**: Custom decorators for request body modification.
4. **`filters/`**:
    
    - Exception and error-handling filters like `global-exception.filter.ts`.
5. **`services/`**:
    
    - **`apis/`**:
        - `auth/`: Handles authentication logic.
        - `mailer/`: Email-sending services.
        - `otp/`: OTP generation and verification logic.
        - `redis/`: Redis adapter services.
        - `sendOtp/`: Dedicated OTP sending service.
        - `users/`: User management, including schemas, decorators, and guards.
    - **`gateways/`**:
        - `presence/`: Manages WebSocket-based presence events.
6. **`types/`**:
    
    - TypeScript type definitions (e.g., `SocketClient.d.ts`, `QueryOptions.d.ts`).

---

#### **`test/`**

- **`app.e2e-spec.ts`**: End-to-end test for the application.
- **`jest-e2e.json`**: Jest configuration for E2E tests.