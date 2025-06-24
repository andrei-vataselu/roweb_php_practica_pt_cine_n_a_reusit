# Laravel Blog Tutorial

## 1. Cloneaza proiectul

Deschide terminalul si scrie:

```
 git clone <adresa-ta-de-git>
cd practica2025
```

---

## 2. Seteaza fisierele de environment

Intra in folderul `laravel-blog/` si asigura-te ca ai fisierul `.env`. Daca nu exista, copiaza-l din `.env.example`:

```
cd laravel-blog
cp .env.example .env
cd ..
```

Verifica sa ai aceleasi date de conectare la baza de date ca in `docker-compose.yml` ( DB_HOST=db, DB_DATABASE=laravel_blog, DB_USERNAME=laravel_user, DB_PASSWORD=user_password).

---

## 3. Porneste containerele

Din folderul principal (unde ai `docker-compose.yml`):

```
docker compose up -d --build
```

Asta porneste tot ce trebuie: PHP, Nginx, MySQL, phpMyAdmin.

---

## 4. Instaleaza dependencies + baza de date

Toate comenzile de mai jos se ruleaza din containerul ( COMENZIILE SE DAU IN FOLDERU CU DOCKER COMPOSE U )

```
docker compose exec app composer install

docker compose exec app composer require livewire/livewire

docker compose exec app php artisan key:generate

docker compose exec app php artisan migrate

docker compose exec app php artisan db:seed

docker compose exec app php artisan optimize:clear

docker compose exec app npm install

docker compose exec app npm run build
```

---

## 5. Acceseaza aplicatia

- Site-ul: http://localhost:8000
- phpMyAdmin: http://localhost:8080 (user: laravel_user, parola: user_password, host: db)

## 6. Probleme frecvente

- Daca ai eroare de port, schimba porturile in `docker-compose.yml`.
- Daca ai probleme cu permisiunile pe Linux/Mac: `sudo chown -R $USER:$USER .`
- Daca nu se vad modificarile, ruleaza din nou `docker compose exec app npm run build` si/sau `php artisan optimize:clear`.
- Daca nu merge conexiunea la baza de date, verifica `.env` si `docker-compose.yml` sa fie la fel.

---

## 69. Gata!

Daca ai urmat pasii de mai sus, ar trebui sa vezi aplicatia cu Livewire si tot ce trebuie. Daca ai intrebari sau ceva nu merge, lasa un issue sau scrie-mi.
