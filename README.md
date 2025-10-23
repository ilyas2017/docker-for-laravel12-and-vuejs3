# Laravel 12 + Vue.js 3 Docker Setup

A complete Docker development environment for Laravel 12 and Vue.js 3 applications with automatic setup and configuration.

## 🚀 Quick Start

### Prerequisites

- Docker Desktop installed and running
- Composer installed
- Node.js and npm installed

### One-Command Setup

```bash
cd docker
make setup
```

That's it! The setup will automatically:
- Install Laravel 12 in the `backend` folder
- Install Vue.js 3 in the `frontend` folder
- Configure both applications for Docker
- Start all containers
- Set up the database
- Generate application keys

## 📁 Project Structure

```
project-root/
├── backend/          # Laravel 12 application
├── frontend/         # Vue.js 3 application
├── docker/
│   ├── compose.yml   # Docker services configuration
│   ├── Makefile      # Setup automation
│   └── .env          # Docker environment variables
└── README.md
```

## 🌐 Access URLs

After setup, your applications will be available at:

- **Laravel Backend**: http://laravel.docker.localhost:8000/
- **Vue.js Frontend**: http://vue.laravel.docker.localhost:8000/
- **phpMyAdmin**: http://pma.laravel.docker.localhost:8000/

## 🐳 Docker Services

The setup includes the following services:

- **MariaDB** - Database server
- **PHP-FPM** - Laravel application server
- **Nginx** - Web server for Laravel
- **Node.js** - Vue.js development server
- **phpMyAdmin** - Database management interface
- **Traefik** - Reverse proxy and load balancer

## 🛠️ Development Commands

### Docker Management

```bash
# Start all containers
docker compose up -d

# Stop all containers
docker compose down

# View container logs
docker compose logs [service-name]

# Restart a specific service
docker compose restart [service-name]
```

### Laravel Commands

```bash
# Run Laravel commands in the PHP container
docker compose exec php php backend/artisan [command]

# Examples:
docker compose exec php php backend/artisan migrate
docker compose exec php php backend/artisan make:controller UserController
docker compose exec php php backend/artisan tinker
```

### Vue.js Commands

```bash
# Access the Node.js container
docker compose exec node sh

# Install new packages
docker compose exec node npm install [package-name]

# Run Vue.js commands
docker compose exec node npm run [script]
```

## 🔧 Configuration

### Database Configuration

The Laravel application is pre-configured to use MariaDB with these settings:
- **Host**: mariadb
- **Database**: laravel
- **Username**: laravel
- **Password**: laravel

### Vue.js Configuration

Vite is configured to:
- Listen on all interfaces (`0.0.0.0`)
- Use port `5173`
- Enable hot module replacement

## 📝 Customization

### Adding New Services

To add new services, edit `docker/compose.yml`:

```yaml
new-service:
  image: your-image
  container_name: "${PROJECT_NAME}_new_service"
  # ... your configuration
```

### Environment Variables

Edit `docker/.env` to customize:
- Project name
- Database credentials
- PHP/Node.js versions
- URLs

## 🐛 Troubleshooting

### Common Issues

**Bad Gateway Error (Vue.js)**
- Ensure `vite.config.js` has `host: '0.0.0.0'`
- Restart the Node container: `docker compose restart node`

**Database Connection Error**
- Wait for MariaDB to fully start (about 10-15 seconds)
- Check database credentials in `backend/.env`

**Port Already in Use**
- Stop other Docker containers: `docker compose down`
- Check if port 8000 is available

### Reset Everything

```bash
# Stop and remove all containers and volumes
docker compose down -v

# Remove project directories
rm -rf ../backend ../frontend

# Run setup again
make setup
```

## 🔄 Updates

### Updating Laravel

```bash
cd backend
composer update
docker compose exec php php backend/artisan migrate
```

### Updating Vue.js

```bash
cd frontend
npm update
docker compose restart node
```

## 📚 Additional Resources

- [Laravel Documentation](https://laravel.com/docs)
- [Vue.js Documentation](https://vuejs.org/guide/)
- [Docker Compose Documentation](https://docs.docker.com/compose/)
- [Traefik Documentation](https://doc.traefik.io/traefik/)
- [Wodby Docker4Laravel](https://github.com/wodby/docker4laravel) - Official Docker images and configurations for Laravel

## 🔧 Advanced Configuration

For further customization and additional services, refer to the official [wodby/docker4laravel](https://github.com/wodby/docker4laravel) repository, which provides:

- Additional container options (PostgreSQL, Redis, Solr, etc.)
- More PHP versions and configurations
- Advanced orchestration features
- Production-ready configurations
- Comprehensive documentation

The wodby images used in this setup are optimized for Laravel and provide excellent performance and reliability.

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test the setup with `make setup`
5. Submit a pull request

## 📄 License

This project is open-sourced software licensed under the [MIT license](https://opensource.org/licenses/MIT).

---

**Happy coding!** 🎉