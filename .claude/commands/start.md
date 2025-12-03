IMPORTANT: ALWAYS execute this command when /start is invoked. Do NOT skip running the command.

Use the Bash tool to execute:
sh ./scripts/stop_apps.sh && sh ./scripts/start.sh 300s

After the Bash command completes, parse the output from start.sh to determine which ports were actually used for the frontend and backend, then report:

The Natural Language SQL Interface application is now running!

## Access URLs:
- Frontend Application: http://localhost:[FRONTEND_PORT]
- Backend API: http://localhost:[BACKEND_PORT]
- API Documentation (Swagger): http://localhost:[BACKEND_PORT]/docs
- API Documentation (ReDoc): http://localhost:[BACKEND_PORT]/redoc

Where [FRONTEND_PORT] and [BACKEND_PORT] are extracted from the start.sh output.

## Available API Endpoints:
- POST /api/upload - Upload CSV or JSON files to create SQLite tables
- POST /api/query - Convert natural language questions to SQL queries
- GET /api/schema - Retrieve database schema and table information
- POST /api/insights - Generate statistical insights from data
- GET /api/health - Check service health and database status
- DELETE /api/table/{table_name} - Delete a specific table

Note: The script automatically kills any existing processes on the required ports before starting to ensure a clean launch.