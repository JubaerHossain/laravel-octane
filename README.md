# Laravel Benchmark

This project is a benchmarking setup for Laravel applications, leveraging modern performance-boosting technologies like Octane and FrankenPHP. The environment is fully containerized using Docker for ease of setup and consistent testing.

---

## Prerequisites

Before proceeding, ensure you have the following installed:

- Docker
- Docker Compose
- `make` utility (optional, but recommended for ease of use)

---

## Installation

### Step 1: Clone the Repository

```bash
# Clone this repository to your local machine
git clone https://github.com/JubaerHossain/laravel-octane.git
cd laravel-benchmark
```

### Step 2: Start the Environment

The environment is fully configured using Docker. Use the `make` command to start the containers:

```bash
make up
```

This command will:

- Build and start the Docker containers for Laravel Octane and FrankenPHP.
- Expose necessary ports for benchmarking.

### Step 3: Install Dependencies

Access the `app` container and install Laravel dependencies:

```bash
docker exec -it app bash
composer install
```

### Step 4: Configure Laravel

Set up Laravel's `.env` file:

```bash
cp .env.example .env
```

Generate the application key:

```bash
php artisan key:generate
```

---

## Benchmarking

The project includes pre-configured services like Laravel Octane and FrankenPHP. You can benchmark the application using tools like `wrk` or `ab`.

### Running Benchmarks

#### Health Check Endpoint

```bash
wrk -t16 -c100 -d30s --latency http://127.0.0.1:9801/api/health-check
```

---

## Docker Containers

The following containers are included in the setup:

- **FrankenPHP**
- **Whoami** (for debugging and endpoint validation)

---

## Ports

| Service                     | Port |
| --------------------------- | ---- |
| FrankenPHP                  | 9804 |
| Whoami                      | 9801 |

---

## Stopping the Environment

To stop all containers:

```bash
make down
```

---

## Troubleshooting

### Common Errors

1. **Command ****`wrk`**** not found:**

   - Install `wrk` using a package manager, e.g., `brew install wrk` on macOS or `sudo apt install wrk` on Ubuntu.

2. **Containers not starting:**

   - Check Docker logs using:
     ```bash
     docker logs <container_name>
     ```

3. **Timeout errors during fetch:**

   - Ensure your services are reachable at the specified ports.
   - Verify network connectivity using:
     ```bash
     docker network inspect <network_name>
     ```

---

## License

This project is open-source and available under the [MIT License](LICENSE).

---

Happy coding!

