# Use Node.js as the base image
FROM node:18-alpine AS build

# Set the working directory inside the container
WORKDIR /app


RUN echo "This is a new layer" > /new_layer.txt
RUN echo "This is a new layerc fjebi" > /app.txt

RUN echo "helmeo"

RUN echo "hello" > /new.txt

# Copy package.json and package-lock.json before installing dependencies
COPY package*.json ./

# Install dependencies
RUN npm install --frozen-lockfile

# Copy the rest of the application files
COPY . .

# Build the application
RUN npm run build

# Use a lightweight web server for serving the static files
FROM nginx:alpine

# Copy the built files from the previous stage to the Nginx public directory
COPY --from=build /app/dist /usr/share/nginx/html

# Expose port 80
EXPOSE 80

# Start Nginx
CMD ["nginx", "-g", "daemon off;"]

