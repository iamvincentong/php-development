# Docker PHP Development Environment

This project sets up a PHP development environment using Docker Compose with the following services:

- **nginx**: Web server to serve your PHP application
- **php**: PHP-FPM to process PHP files
- **mysql**: Database server

You can extend this setup to include additional services like Redis, Mailhog, etc.

## Getting Started

Follow these steps to get your development environment up and running:

### Prerequisites

Ensure you have Docker and Docker Compose installed on your machine.

### Installation

1. **Clone the repository:**

   ```sh
   git clone https://github.com/your-username/your-repo.git
   ```

2. Copy your PHP project files into the `./app/public` directory.

### Running the Environment

1. Navigate to the project directory:

   ```sh
   cd php-development
   ```

2. Build and start the Docker Compose services:

   ```sh
   docker compose up --build
   ```

3. Open your web browser and visit `http://127.0.0.1/` to see your project up and running!

## Extending the Environment

You can easily extend this setup to include other services as needed. For example, to add Redis and Mailhog:

1. Update docker-compose.yml:

   ```yaml
   version: "3.8"

   services:
   nginx:
     image: nginx:latest
     ports:
       - "80:80"
     volumes:
       - ./app/public:/var/www/html
       - ./config/nginx:/etc/nginx/conf.d

   php:
     image: php:fpm
     volumes:
       - ./app/public:/var/www/html

   mysql:
     image: mysql:5.7
     environment:
     MYSQL_ROOT_PASSWORD: root
     MYSQL_DATABASE: mydatabase
     MYSQL_USER: user
     MYSQL_PASSWORD: password
     ports:
       - "3306:3306"
     volumes:
       - db_data:/var/lib/mysql

   redis:
     image: redis:latest
     ports:
       - "6379:6379"

   mailhog:
     image: mailhog/mailhog
     ports:
       - "1025:1025"
       - "8025:8025"

   volumes:
   db_data:
   ```

2. Rebuild and restart the services:

   ```sh
   docker compose up --build
   ```

## Acknowledgements

Based on the tutorial from:
https://www.sitepoint.com/docker-php-development-environment/
