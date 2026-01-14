
FROM python:3.11-slim

WORKDIR /app

# Install git (required for UCP SDK git dependency)
RUN apt-get update && apt-get install -y git && rm -rf /var/lib/apt/lists/*

# Install uv for fast package management
RUN pip install uv

# Copy dependency files first for caching
COPY pyproject.toml uv.lock ./

# Install dependencies including the project itself
RUN uv sync --frozen

# Copy the rest of the application code
COPY . .

# Expose the application port
EXPOSE 8000

# Run the server
# Note: Host is hardcoded to 0.0.0.0 in server.py, which is correct for containers
CMD ["uv", "run", "server.py", "--products_db_path=ucp_data/products.db", "--transactions_db_path=ucp_data/transactions.db", "--port=8000"]
