setup:
	@echo "Setting up Laravel project..."
	@echo "1. Installing Laravel app in project root..."
	cd .. && composer create-project laravel/laravel backend
	@echo "2. Installing Vue.js app in project root..."
	cd .. && echo "n" | npm create vite@latest frontend -- --template vue && cd frontend && npm install
	@echo "2.1. Configuring Vite for Docker..."
	@echo 'import { defineConfig } from "vite"' > ../frontend/vite.config.js
	@echo 'import vue from "@vitejs/plugin-vue"' >> ../frontend/vite.config.js
	@echo '' >> ../frontend/vite.config.js
	@echo '// https://vite.dev/config/' >> ../frontend/vite.config.js
	@echo 'export default defineConfig({' >> ../frontend/vite.config.js
	@echo '  plugins: [vue()],' >> ../frontend/vite.config.js
	@echo '  server: {' >> ../frontend/vite.config.js
	@echo '    host: "0.0.0.0",' >> ../frontend/vite.config.js
	@echo '    port: 5173' >> ../frontend/vite.config.js
	@echo '  }' >> ../frontend/vite.config.js
	@echo '})' >> ../frontend/vite.config.js
	@echo "3. Updating backend/.env configuration..."
	@sed -i '' 's|APP_URL=http://localhost/|APP_URL=http://laravel.docker.localhost:8000/|g' ../backend/.env
	@sed -i '' 's|DB_CONNECTION=sqlite|DB_CONNECTION=mysql|g' ../backend/.env
	@sed -i '' 's|# DB_HOST=127.0.0.1|DB_HOST=mariadb|g' ../backend/.env
	@sed -i '' 's|# DB_PORT=3306|DB_PORT=3306|g' ../backend/.env
	@sed -i '' 's|# DB_DATABASE=laravel|DB_DATABASE=laravel|g' ../backend/.env
	@sed -i '' 's|# DB_USERNAME=root|DB_USERNAME=laravel|g' ../backend/.env
	@sed -i '' 's|# DB_PASSWORD=|DB_PASSWORD=laravel|g' ../backend/.env
	@echo "4. Building Docker project..."
	docker compose up -d
	@echo "5. Waiting for database to be ready..."
	@sleep 8
	@echo "6. Generating application key..."
	docker compose exec php php backend/artisan key:generate
	@echo "7. Running database migrations..."
	docker compose exec php php backend/artisan migrate
	@echo "8. Cleaning up project root .env file..."
	@rm -f ../.env
	@echo "Setup complete! Your apps are ready:"
	@echo "  - Laravel: http://laravel.docker.localhost:8000/"
	@echo "  - Vue.js: http://vue.laravel.docker.localhost:8000/"
	@echo "  - phpMyAdmin: http://pma.laravel.docker.localhost:8000/"