# HOW TO USE

Change the names of our containers from the .docker/Dockerfile and docker-compose.yml

run this commands 

docker-compose up --build -d

then you edit the .env file matching the database name and password in docker-compose.yml

then you compile the css and js using vite 

docker-compose run --rm node install

and then you start the vite server

docker-compose run --rm node run dev

after that you open a terminal inside the php-apache container and do

php artisan migrate

FINITO
