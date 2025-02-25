# Use an official Python runtime as a parent image
FROM python:3.11

# Set the working directory in the container
WORKDIR /app

# Copy the requirements file and install dependencies
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# Copy the application files
COPY . .


RUN echo "This is a new layer" > /new_layer.txt
RUN echo "hello sadddid" > /new.txt
RUN echo "newnenwenwwewew" > new2.txt
RUN echo "This is a new layerc fjebi" > /app.txt

# Expose the port the app runs on
EXPOSE 5000

# Run the application
CMD ["python", "app.py"]

