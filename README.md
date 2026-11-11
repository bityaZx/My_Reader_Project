# Reader
Reader is an impressive full stack web application crafted with Node.js, designed to provide a delightful experience for food enthusiasts and cooking aficionados. With its intuitive user interface, extensive collection of recipes, and interactive features, Reader takes you on a culinary journey, allowing you to explore, discover, and share your passion for food.

## Technologies

### Client
1. NEXT.JS
2. React Query
3. SCSS
4. Bulma

### Server
1. Nest.js
2. Prisma
3. PostgreSQL




https://github.com/atenadadkhah/reader/assets/91287064/c2118870-1755-455c-84d0-dd95259ecf2a

## Run with Docker Compose

From the project root, run:

```powershell
docker compose up --build
```

Open the frontend at [http://localhost:3001](http://localhost:3001). The backend is available at [http://localhost:3000](http://localhost:3000).

PostgreSQL data is stored in the `postgres_data` named volume and remains after stopping or removing the containers. Do not run `docker compose down -v` unless you intend to delete that data. The database is on an internal network and is not published to the host; only the backend can access it.


## Setup
### Docker

1. Copy `.env.example` to `.env` and set a local database password and matching `DATABASE_URL`.
2. If your network uses TLS inspection, set `PRISMA_CA_FILE` in `.env` to the path of its trusted CA certificate bundle. Do not disable TLS verification.
3. From the project root, run `docker compose up --build -d`.
4. Open the app at `http://localhost:3001`. The API is available at `http://localhost:3000`.

The Dockerfiles use multi-stage builds and run the Node.js services as the unprivileged `node` user. Stop the services with `docker compose down`.

### Manual development

1. Restore the PostgreSQL backup in `reader_db_backup`.
2. Configure `DATABASE_URL` in `server/.env`.
3. Start the server from `server` with `npm install` and `npm run start:dev`.
4. Configure `NEXT_PUBLIC_API_URL` in `client/.env.local`.
5. Start the client from `client` with `npm install` and `npm run dev`.
