flowchart TD

    %% Usuário e Frontend
    A[Usuário] --> B[CloudFront]
    B --> C[S3 (Frontend Next.js)]

    %% API e Backend
    C --> D[API Gateway]
    D --> E[Backend (EC2 / ECS - NestJS)]

    %% Banco de dados
    E --> F[RDS PostgreSQL]

    %% Cache e tempo real
    E --> G[ElastiCache (Redis)]
    G --> H[WebSocket / Tempo Real]
    H --> A

    %% IoT
    I[Sensores] --> J[IoT Core]
    J --> K[Lambda]
    K --> E

    %% AR e Assets
    L[S3 (Modelos 3D / Assets)] --> M[Módulo AR (Frontend)]
    M --> A
