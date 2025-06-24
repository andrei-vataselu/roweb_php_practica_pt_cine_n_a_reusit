# Laravel Blog Tutorial

Daca nu esti bot ar trebui sa poti urma tutorialul.

## 1. Cloneaza proiectul

Deschide terminalul si scrie:

```
git clone  https://github.com/andrei-vataselu/roweb_php_practica_pt_cine_n_a_reusit practica2025
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

## 420. Ouput

Cam asa tre sa iti arate output ul daca nu esti bot

```
C:\Users\andrewkarma\Desktop\jhfdg\laravel-blog>docker compose up -d --build
Compose now can delegate build to bake for better performances
Just set COMPOSE_BAKE=true
[+] Building 1.8s (17/17) FINISHED                                                                 docker:desktop-linux
 => [app internal] load build definition from Dockerfile                                                           0.3s
 => => transferring dockerfile: 1.03kB                                                                             0.0s
 => [app internal] load metadata for docker.io/library/composer:latest                                             0.0s
 => [app internal] load metadata for docker.io/library/php:8.3-fpm                                                 0.6s
 => [app internal] load .dockerignore                                                                              0.1s
 => => transferring context: 2B                                                                                    0.0s
 => [app internal] load build context                                                                              0.1s
 => => transferring context: 460.59kB                                                                              0.0s
 => [app] FROM docker.io/library/composer:latest                                                                   0.0s
 => [app stage-0 1/9] FROM docker.io/library/php:8.3-fpm@sha256:144245cdb5936b518d133bfce7c3df98880d040da864eb02f  0.0s
 => CACHED [app stage-0 2/9] WORKDIR /var/www/html/laravel-blog                                                    0.0s
 => CACHED [app stage-0 3/9] RUN apt-get update && apt-get install -y     git     curl     libpng-dev     libonig  0.0s
 => CACHED [app stage-0 4/9] RUN apt-get clean && rm -rf /var/lib/apt/lists/*                                      0.0s
 => CACHED [app stage-0 5/9] RUN docker-php-ext-install pdo_mysql mbstring exif pcntl bcmath gd zip                0.0s
 => CACHED [app stage-0 6/9] COPY --from=composer:latest /usr/bin/composer /usr/bin/composer                       0.0s
 => CACHED [app stage-0 7/9] RUN useradd -G www-data,root -u 1000 -d /home/laravel laravel                         0.0s
 => CACHED [app stage-0 8/9] RUN mkdir -p /home/laravel/.composer &&     chown -R laravel:laravel /home/laravel    0.0s
 => [app stage-0 9/9] COPY --chown=laravel:laravel laravel-blog/ /var/www/html/laravel-blog                        0.2s
 => [app] exporting to image                                                                                       0.2s
 => => exporting layers                                                                                            0.1s
 => => writing image sha256:15df49123ebe5171e7f5a1a932227b321050aba56180b1fa0f20c192a039d918                       0.0s
 => => naming to docker.io/library/jhfdg-app                                                                       0.0s
 => [app] resolving provenance for metadata file                                                                   0.0s
[+] Running 7/7
 ✔ app                                Built                                                                        0.0s
 ✔ Network jhfdg_laravel-blog         Created                                                                      0.1s
 ✔ Volume "jhfdg_dbdata"              Created                                                                      0.0s
 ✔ Container laravel-blog-db          Started                                                                      0.8s
 ✔ Container laravel-blog-app         Started                                                                      1.2s
 ✔ Container laravel-blog-phpmyadmin  Started                                                                      1.1s
 ✔ Container laravel-blog-webserver   Started                                                                      1.3s

C:\Users\andrewkarma\Desktop\jhfdg\laravel-blog>docker compose exec app composer install
Installing dependencies from lock file (including require-dev)
Verifying lock file contents can be installed on current platform.
Package operations: 111 installs, 0 updates, 0 removals
  - Downloading doctrine/inflector (2.0.10)
  - Downloading doctrine/lexer (3.0.1)
  - Downloading symfony/polyfill-ctype (v1.32.0)
  - Downloading webmozart/assert (1.11.0)
  - Downloading dragonmantank/cron-expression (v3.4.0)
  - Downloading symfony/deprecation-contracts (v3.6.0)
  - Downloading psr/container (2.0.2)
  - Downloading fakerphp/faker (v1.24.1)
  - Downloading symfony/polyfill-php83 (v1.32.0)
  - Downloading symfony/polyfill-mbstring (v1.32.0)
  - Downloading symfony/http-foundation (v7.3.0)
  - Downloading fruitcake/php-cors (v1.3.0)
  - Downloading psr/http-message (2.0)
  - Downloading psr/http-client (1.0.3)
  - Downloading ralouphie/getallheaders (3.0.3)
  - Downloading psr/http-factory (1.1.0)
  - Downloading guzzlehttp/psr7 (2.7.1)
  - Downloading guzzlehttp/promises (2.2.0)
  - Downloading guzzlehttp/guzzle (7.9.3)
  - Downloading symfony/polyfill-php80 (v1.32.0)
  - Downloading guzzlehttp/uri-template (v1.0.4)
  - Downloading symfony/polyfill-intl-normalizer (v1.32.0)
  - Downloading symfony/polyfill-intl-grapheme (v1.32.0)
  - Downloading symfony/string (v7.3.0)
  - Downloading symfony/service-contracts (v3.6.0)
  - Downloading symfony/console (v7.3.0)
  - Downloading nunomaduro/termwind (v2.3.1)
  - Downloading voku/portable-ascii (2.0.3)
  - Downloading phpoption/phpoption (1.9.3)
  - Downloading graham-campbell/result-type (v1.1.3)
  - Downloading vlucas/phpdotenv (v5.6.2)
  - Downloading symfony/css-selector (v7.3.0)
  - Downloading tijsverkoyen/css-to-inline-styles (v2.3.0)
  - Downloading symfony/var-dumper (v7.3.0)
  - Downloading symfony/polyfill-uuid (v1.32.0)
  - Downloading symfony/uid (v7.3.0)
  - Downloading symfony/routing (v7.3.0)
  - Downloading symfony/process (v7.3.0)
  - Downloading symfony/polyfill-intl-idn (v1.32.0)
  - Downloading symfony/mime (v7.3.0)
  - Downloading psr/event-dispatcher (1.0.0)
  - Downloading symfony/event-dispatcher-contracts (v3.6.0)
  - Downloading symfony/event-dispatcher (v7.3.0)
  - Downloading psr/log (3.0.2)
  - Downloading egulias/email-validator (4.0.4)
  - Downloading symfony/mailer (v7.3.0)
  - Downloading symfony/error-handler (v7.3.0)
  - Downloading symfony/http-kernel (v7.3.0)
  - Downloading symfony/finder (v7.3.0)
  - Downloading ramsey/collection (2.1.1)
  - Downloading brick/math (0.13.1)
  - Downloading ramsey/uuid (4.8.1)
  - Downloading psr/simple-cache (3.0.0)
  - Downloading symfony/translation-contracts (v3.6.0)
  - Downloading symfony/translation (v7.3.0)
  - Downloading psr/clock (1.0.0)
  - Downloading symfony/clock (v7.3.0)
  - Downloading carbonphp/carbon-doctrine-types (3.2.0)
  - Downloading nesbot/carbon (3.10.1)
  - Downloading monolog/monolog (3.9.0)
  - Downloading league/uri-interfaces (7.5.0)
  - Downloading league/uri (7.5.1)
  - Downloading league/mime-type-detection (1.16.0)
  - Downloading league/flysystem-local (3.29.0)
  - Downloading league/flysystem (3.29.1)
  - Downloading nette/utils (v4.0.7)
  - Downloading nette/schema (v1.3.2)
  - Downloading dflydev/dot-access-data (v3.0.3)
  - Downloading league/config (v1.2.0)
  - Downloading league/commonmark (2.7.0)
  - Downloading laravel/serializable-closure (v2.0.4)
  - Downloading laravel/prompts (v0.3.5)
  - Downloading laravel/framework (v12.19.3)
  - Downloading laravel/pail (v1.2.3)
  - Downloading laravel/pint (v1.22.1)
  - Downloading symfony/yaml (v7.3.0)
  - Downloading laravel/sail (v1.43.1)
  - Downloading nikic/php-parser (v5.5.0)
  - Downloading psy/psysh (v0.12.9)
  - Downloading laravel/tinker (v2.10.1)
  - Downloading livewire/livewire (v3.6.3)
  - Downloading hamcrest/hamcrest-php (v2.1.1)
  - Downloading mockery/mockery (1.6.12)
  - Downloading filp/whoops (2.18.3)
  - Downloading nunomaduro/collision (v8.8.1)
  - Downloading staabm/side-effects-detector (1.0.5)
  - Downloading sebastian/version (5.0.2)
  - Downloading sebastian/type (5.1.2)
  - Downloading sebastian/recursion-context (6.0.2)
  - Downloading sebastian/object-reflector (4.0.1)
  - Downloading sebastian/object-enumerator (6.0.1)
  - Downloading sebastian/global-state (7.0.2)
  - Downloading sebastian/exporter (6.3.0)
  - Downloading sebastian/environment (7.2.1)
  - Downloading sebastian/diff (6.0.2)
  - Downloading sebastian/comparator (6.3.1)
  - Downloading sebastian/code-unit (3.0.3)
  - Downloading sebastian/cli-parser (3.0.2)
  - Downloading phpunit/php-timer (7.0.1)
  - Downloading phpunit/php-text-template (4.0.1)
  - Downloading phpunit/php-invoker (5.0.1)
  - Downloading phpunit/php-file-iterator (5.1.0)
  - Downloading theseer/tokenizer (1.2.3)
  - Downloading sebastian/lines-of-code (3.0.1)
  - Downloading sebastian/complexity (4.0.1)
  - Downloading sebastian/code-unit-reverse-lookup (4.0.1)
  - Downloading phpunit/php-code-coverage (11.0.10)
  - Downloading phar-io/version (3.2.1)
  - Downloading phar-io/manifest (2.0.4)
  - Downloading myclabs/deep-copy (1.13.1)
  - Downloading phpunit/phpunit (11.5.24)
  - Installing doctrine/inflector (2.0.10): Extracting archive
  - Installing doctrine/lexer (3.0.1): Extracting archive
  - Installing symfony/polyfill-ctype (v1.32.0): Extracting archive
  - Installing webmozart/assert (1.11.0): Extracting archive
  - Installing dragonmantank/cron-expression (v3.4.0): Extracting archive
  - Installing symfony/deprecation-contracts (v3.6.0): Extracting archive
  - Installing psr/container (2.0.2): Extracting archive
  - Installing fakerphp/faker (v1.24.1): Extracting archive
  - Installing symfony/polyfill-php83 (v1.32.0): Extracting archive
  - Installing symfony/polyfill-mbstring (v1.32.0): Extracting archive
  - Installing symfony/http-foundation (v7.3.0): Extracting archive
  - Installing fruitcake/php-cors (v1.3.0): Extracting archive
  - Installing psr/http-message (2.0): Extracting archive
  - Installing psr/http-client (1.0.3): Extracting archive
  - Installing ralouphie/getallheaders (3.0.3): Extracting archive
  - Installing psr/http-factory (1.1.0): Extracting archive
  - Installing guzzlehttp/psr7 (2.7.1): Extracting archive
  - Installing guzzlehttp/promises (2.2.0): Extracting archive
  - Installing guzzlehttp/guzzle (7.9.3): Extracting archive
  - Installing symfony/polyfill-php80 (v1.32.0): Extracting archive
  - Installing guzzlehttp/uri-template (v1.0.4): Extracting archive
  - Installing symfony/polyfill-intl-normalizer (v1.32.0): Extracting archive
  - Installing symfony/polyfill-intl-grapheme (v1.32.0): Extracting archive
  - Installing symfony/string (v7.3.0): Extracting archive
  - Installing symfony/service-contracts (v3.6.0): Extracting archive
  - Installing symfony/console (v7.3.0): Extracting archive
  - Installing nunomaduro/termwind (v2.3.1): Extracting archive
  - Installing voku/portable-ascii (2.0.3): Extracting archive
  - Installing phpoption/phpoption (1.9.3): Extracting archive
  - Installing graham-campbell/result-type (v1.1.3): Extracting archive
  - Installing vlucas/phpdotenv (v5.6.2): Extracting archive
  - Installing symfony/css-selector (v7.3.0): Extracting archive
  - Installing tijsverkoyen/css-to-inline-styles (v2.3.0): Extracting archive
  - Installing symfony/var-dumper (v7.3.0): Extracting archive
  - Installing symfony/polyfill-uuid (v1.32.0): Extracting archive
  - Installing symfony/uid (v7.3.0): Extracting archive
  - Installing symfony/routing (v7.3.0): Extracting archive
  - Installing symfony/process (v7.3.0): Extracting archive
  - Installing symfony/polyfill-intl-idn (v1.32.0): Extracting archive
  - Installing symfony/mime (v7.3.0): Extracting archive
  - Installing psr/event-dispatcher (1.0.0): Extracting archive
  - Installing symfony/event-dispatcher-contracts (v3.6.0): Extracting archive
  - Installing symfony/event-dispatcher (v7.3.0): Extracting archive
  - Installing psr/log (3.0.2): Extracting archive
  - Installing egulias/email-validator (4.0.4): Extracting archive
  - Installing symfony/mailer (v7.3.0): Extracting archive
  - Installing symfony/error-handler (v7.3.0): Extracting archive
  - Installing symfony/http-kernel (v7.3.0): Extracting archive
  - Installing symfony/finder (v7.3.0): Extracting archive
  - Installing ramsey/collection (2.1.1): Extracting archive
  - Installing brick/math (0.13.1): Extracting archive
  - Installing ramsey/uuid (4.8.1): Extracting archive
  - Installing psr/simple-cache (3.0.0): Extracting archive
  - Installing symfony/translation-contracts (v3.6.0): Extracting archive
  - Installing symfony/translation (v7.3.0): Extracting archive
  - Installing psr/clock (1.0.0): Extracting archive
  - Installing symfony/clock (v7.3.0): Extracting archive
  - Installing carbonphp/carbon-doctrine-types (3.2.0): Extracting archive
  - Installing nesbot/carbon (3.10.1): Extracting archive
  - Installing monolog/monolog (3.9.0): Extracting archive
  - Installing league/uri-interfaces (7.5.0): Extracting archive
  - Installing league/uri (7.5.1): Extracting archive
  - Installing league/mime-type-detection (1.16.0): Extracting archive
  - Installing league/flysystem-local (3.29.0): Extracting archive
  - Installing league/flysystem (3.29.1): Extracting archive
  - Installing nette/utils (v4.0.7): Extracting archive
  - Installing nette/schema (v1.3.2): Extracting archive
  - Installing dflydev/dot-access-data (v3.0.3): Extracting archive
  - Installing league/config (v1.2.0): Extracting archive
  - Installing league/commonmark (2.7.0): Extracting archive
  - Installing laravel/serializable-closure (v2.0.4): Extracting archive
  - Installing laravel/prompts (v0.3.5): Extracting archive
  - Installing laravel/framework (v12.19.3): Extracting archive
  - Installing laravel/pail (v1.2.3): Extracting archive
  - Installing laravel/pint (v1.22.1): Extracting archive
  - Installing symfony/yaml (v7.3.0): Extracting archive
  - Installing laravel/sail (v1.43.1): Extracting archive
  - Installing nikic/php-parser (v5.5.0): Extracting archive
  - Installing psy/psysh (v0.12.9): Extracting archive
  - Installing laravel/tinker (v2.10.1): Extracting archive
  - Installing livewire/livewire (v3.6.3): Extracting archive
  - Installing hamcrest/hamcrest-php (v2.1.1): Extracting archive
  - Installing mockery/mockery (1.6.12): Extracting archive
  - Installing filp/whoops (2.18.3): Extracting archive
  - Installing nunomaduro/collision (v8.8.1): Extracting archive
  - Installing staabm/side-effects-detector (1.0.5): Extracting archive
  - Installing sebastian/version (5.0.2): Extracting archive
  - Installing sebastian/type (5.1.2): Extracting archive
  - Installing sebastian/recursion-context (6.0.2): Extracting archive
  - Installing sebastian/object-reflector (4.0.1): Extracting archive
  - Installing sebastian/object-enumerator (6.0.1): Extracting archive
  - Installing sebastian/global-state (7.0.2): Extracting archive
  - Installing sebastian/exporter (6.3.0): Extracting archive
  - Installing sebastian/environment (7.2.1): Extracting archive
  - Installing sebastian/diff (6.0.2): Extracting archive
  - Installing sebastian/comparator (6.3.1): Extracting archive
  - Installing sebastian/code-unit (3.0.3): Extracting archive
  - Installing sebastian/cli-parser (3.0.2): Extracting archive
  - Installing phpunit/php-timer (7.0.1): Extracting archive
  - Installing phpunit/php-text-template (4.0.1): Extracting archive
  - Installing phpunit/php-invoker (5.0.1): Extracting archive
  - Installing phpunit/php-file-iterator (5.1.0): Extracting archive
  - Installing theseer/tokenizer (1.2.3): Extracting archive
  - Installing sebastian/lines-of-code (3.0.1): Extracting archive
  - Installing sebastian/complexity (4.0.1): Extracting archive
  - Installing sebastian/code-unit-reverse-lookup (4.0.1): Extracting archive
  - Installing phpunit/php-code-coverage (11.0.10): Extracting archive
  - Installing phar-io/version (3.2.1): Extracting archive
  - Installing phar-io/manifest (2.0.4): Extracting archive
  - Installing myclabs/deep-copy (1.13.1): Extracting archive
  - Installing phpunit/phpunit (11.5.24): Extracting archive
Generating optimized autoload files
> Illuminate\Foundation\ComposerScripts::postAutoloadDump
> @php artisan package:discover --ansi

   INFO  Discovering packages.

  laravel/pail .................................................................................................. DONE
  laravel/sail .................................................................................................. DONE
  laravel/tinker ................................................................................................ DONE
  livewire/livewire ............................................................................................. DONE
  nesbot/carbon ................................................................................................. DONE
  nunomaduro/collision .......................................................................................... DONE
  nunomaduro/termwind ........................................................................................... DONE

80 packages you are using are looking for funding.
Use the `composer fund` command to find out more!

C:\Users\andrewkarma\Desktop\jhfdg\laravel-blog>docker compose exec app composer require livewire/livewire
./composer.json has been updated
Running composer update livewire/livewire
Loading composer repositories with package information
Updating dependencies
Nothing to modify in lock file
Writing lock file
Installing dependencies from lock file (including require-dev)
Nothing to install, update or remove
Generating optimized autoload files
> Illuminate\Foundation\ComposerScripts::postAutoloadDump
> @php artisan package:discover --ansi

   INFO  Discovering packages.

  laravel/pail .................................................................................................. DONE
  laravel/sail .................................................................................................. DONE
  laravel/tinker ................................................................................................ DONE
  livewire/livewire ............................................................................................. DONE
  nesbot/carbon ................................................................................................. DONE
  nunomaduro/collision .......................................................................................... DONE
  nunomaduro/termwind ........................................................................................... DONE

80 packages you are using are looking for funding.
Use the `composer fund` command to find out more!
> @php artisan vendor:publish --tag=laravel-assets --ansi --force

   INFO  No publishable resources for tag [laravel-assets].

No security vulnerability advisories found.
Using version ^3.6 for livewire/livewire

C:\Users\andrewkarma\Desktop\jhfdg\laravel-blog>docker compose exec app php artisan key:generate

   INFO  Application key set successfully.


C:\Users\andrewkarma\Desktop\jhfdg\laravel-blog>docker compose exec app php artisan migrate

   INFO  Preparing database.

  Creating migration table ............................................................................. 170.79ms DONE

   INFO  Running migrations.

  0001_01_01_000000_create_users_table ................................................................. 636.16ms DONE
  0001_01_01_000001_create_cache_table ................................................................. 357.58ms DONE
  0001_01_01_000002_create_jobs_table .................................................................. 384.11ms DONE


C:\Users\andrewkarma\Desktop\jhfdg\laravel-blog>docker compose exec app php artisan db:seed

   INFO  Seeding database.


C:\Users\andrewkarma\Desktop\jhfdg\laravel-blog>docker compose exec app php artisan optimize:clear

   INFO  Clearing cached bootstrap files.

  config ................................................................................................ 37.26ms DONE
  cache ................................................................................................ 393.66ms DONE
  compiled .............................................................................................. 49.95ms DONE
  events ................................................................................................. 9.01ms DONE
  routes ................................................................................................. 9.23ms DONE
  views ................................................................................................. 85.41ms DONE


C:\Users\andrewkarma\Desktop\jhfdg\laravel-blog>docker compose exec app npm install

added 94 packages, and audited 95 packages in 30s

22 packages are looking for funding
  run `npm fund` for details

found 0 vulnerabilities

C:\Users\andrewkarma\Desktop\jhfdg\laravel-blog>docker compose exec app npm run build

> build
> vite build

vite v6.3.5 building for production...
✓ 53 modules transformed.
public/build/manifest.json             0.27 kB │ gzip:  0.14 kB
public/build/assets/app-DcKHUAcs.css  11.31 kB │ gzip:  3.13 kB
public/build/assets/app-DNxiirP_.js   35.32 kB │ gzip: 14.14 kB
✓ built in 38.54s

```

## 69. Gata!

Daca ai urmat pasii de mai sus, ar trebui sa vezi aplicatia cu Livewire si tot ce trebuie. Daca ai intrebari sau ceva nu merge, lasa un issue sau scrie-mi.
