FROM python:3.13-slim

WORKDIR /app

# Install git for ucp-sdk dependency
RUN apt-get update && apt-get install -y git && rm -rf /var/lib/apt/lists/*

# Install uv
COPY --from=ghcr.io/astral-sh/uv:latest /uv /bin/uv

# Copy project files
COPY . .

# Install dependencies
RUN uv sync

# Expose port
EXPOSE 10999

# Run command
CMD ["uv", "run", "business_agent", "--host", "0.0.0.0", "--port", "10999"]
