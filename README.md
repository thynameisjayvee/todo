# todo

## Laravel Installation
- navigate to src folder
```
cd src
```
- Install laravel dependencies
```
composer install
```
- Setup laravel environment configuration
```
cp .env.example .env
```
- Modify environment configuration based on your needs(eg. database name, ports etc.)
- Install required laravel keys and migrate database
```
php artisan key:generate
php artisan jwt:secret
php artisan migrate
```
- Install node modules 
```
npm install or yarn install
```
- Build assets or watch
```
npm run watch or yarn run watch --to watch files during development
npm run prod or yarn run prod --for production server
```
