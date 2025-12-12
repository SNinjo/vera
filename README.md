# Vera

A full-stack web system for convenient cloud services.

## Service

1. [Site](https://github.com/SNinjo/vera-site) - Web interface for interacting with all services.
2. [Identity](https://github.com/SNinjo/vera-identity-service) - Handles user authentication and identity management.
3. [Drive](https://github.com/SNinjo/vera-drive-service) - Provides storage for user data.

## Usage

1. Clone the repository with all submodules

    ```shell
    git clone --recurse-submodules git@github.com:SNinjo/vera.git
    ```

2. Set up environment variables

    ```shell
    cp .env.example .env
    cp vera-site/.env.example vera-site/.env
    cp vera-identity-service/.env.example vera-identity-service/.env
    cp vera-drive-service/.env.example vera-drive-service/.env
    ```

3. Start the database

    ```shell
    docker-compose up -d db
    ```

4. Migrate the database schemas

    ```shell
    cd ./vera-identity-service && make migrate-up
    cd ../vera-drive-service && make migrate-up
    cd ..
    ```

5. Add your first user to the whitelist

    ```shell
    export EMAIL=<your-email>
    psql "postgres://user:pass@localhost:5432/vera?sslmode=disable" \
        -c "INSERT INTO users (email, created_at, updated_at) VALUES ('$EMAIL', NOW(), NOW());"
    ```

6. Start all services

    ```shell
    docker-compose up -d
    ```

7. Open the [website](http://localhost:8080) and log in with Gmail
