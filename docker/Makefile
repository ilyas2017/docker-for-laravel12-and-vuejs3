setup:
	@echo "Setting up Laravel project..."
	@echo "1. Installing Laravel app in project root..."
	cd .. && composer create-project laravel/laravel backend
	@echo "2. Updating backend/.env configuration..."
	@sed -i '' 's|APP_URL=http://localhost/|APP_URL=http://laravel.docker.localhost:8000/|g' ../backend/.env
	@sed -i '' 's|DB_CONNECTION=sqlite|DB_CONNECTION=mysql|g' ../backend/.env
	@sed -i '' 's|# DB_HOST=127.0.0.1|DB_HOST=mariadb|g' ../backend/.env
	@sed -i '' 's|# DB_PORT=3306|DB_PORT=3306|g' ../backend/.env
	@sed -i '' 's|# DB_DATABASE=laravel|DB_DATABASE=laravel|g' ../backend/.env
	@sed -i '' 's|# DB_USERNAME=root|DB_USERNAME=laravel|g' ../backend/.env
	@sed -i '' 's|# DB_PASSWORD=|DB_PASSWORD=laravel|g' ../backend/.env
	@echo "3. Building Docker project..."
	docker compose up -d
	@echo "4. Waiting for database to be ready..."
	@sleep 15
	@echo "5. Generating application key..."
	docker compose exec php php backend/artisan key:generate
	@echo "6. Running database migrations..."
	docker compose exec php php backend/artisan migrate
	@echo "Setup complete! Your Laravel app is ready at http://laravel.docker.localhost:8000/"