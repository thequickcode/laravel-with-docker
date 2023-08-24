Before running `docker compose up` please copy the `.env.example` file to `.env` and change the database credentials.

Those credentials will be used automatically during the build step of the mysql image.

You will have also to use the same credentials in the .env file which should be available in `backend/.env` which is used by laravel.

To fix file permission issues execute the following command:

```bash
docker compose run --rm php chown -R www-data:www-data /app
```

To link the storage execute the following command:

```bash
docker compose run --rm php ln -s -f /app/storage/app/public /app/public/storage
```
