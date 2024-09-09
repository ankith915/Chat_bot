# Use the Python 3.11.8 base image
FROM python:3.11.8

# Set the working directory inside the container
WORKDIR /code

# Copy the requirements file from the common directory into the container
COPY common/requirements.txt requirements.txt

# Update and upgrade system packages
RUN apt-get update && apt-get upgrade -y

# Install Python dependencies
RUN pip install -r requirements.txt

# Copy application code and necessary directories into the container
COPY copilot/app /code/app
COPY common /code/common
COPY configs /code/configs  

# Set environment variables
ENV LLM_CONFIG="/code/configs/llm_config.json"
ENV DB_CONFIG="/code/configs/db_config.json"
ENV MILVUS_CONFIG="/code/configs/milvus_config.json"
ENV SMITH_CONFIG="/code/configs/smith_config.json"
ENV LOGLEVEL="INFO"

# Expose port 8000 for the application
EXPOSE 8000

# Define the command to run the application using uvicorn
CMD ["uvicorn", "app.main:app", "--host", "0.0.0.0", "--port", "8000"]
