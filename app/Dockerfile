# Use an official Python runtime as a parent image
FROM python:3.9-slim

# Set working directory
WORKDIR /app

# Copy requirements first to leverage Docker cache
COPY requirements.txt .

# Install dependencies without cache to keep image lean
RUN pip install --no-cache-dir -r requirements.txt

# Copy app source code
COPY . .

# Expose port (adjust if needed)
EXPOSE 5000

# Command to run your Flask app (adjust if your entrypoint is different)
CMD ["python", "app.py"]