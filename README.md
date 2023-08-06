# pgsql-s3-backup

Backup PostgresSQL to S3 (supports periodic backups). See [pgsql-s3-backup](https://github.com/chadweimer/pgsql-s3-restore) for restoring the backups

Special thanks to @schickling for the initial basis of these images. See <https://github.com/schickling/dockerfiles>.

## Usage

Docker:
```sh
$ docker run -e S3_ACCESS_KEY_ID=key -e S3_SECRET_ACCESS_KEY=secret -e S3_BUCKET=my-bucket -e S3_PREFIX=backup -e POSTGRES_DATABASE=dbname -e POSTGRES_USER=user -e POSTGRES_PASSWORD=password -e POSTGRES_HOST=localhost ghcr.io/chadweimer/pgsql-s3-backup
```

Docker Compose:
```yaml
postgres:
  image: postgres
  environment:
    POSTGRES_USER: user
    POSTGRES_PASSWORD: password

pgbackups3:
  image: ghcr.io/chadweimer/pgsql-s3-backup
  links:
    - postgres
  environment:
    SCHEDULE: '0 0 * * *'
    S3_REGION: region
    S3_ACCESS_KEY_ID: key
    S3_SECRET_ACCESS_KEY: secret
    S3_BUCKET: my-bucket
    S3_PREFIX: backup
    POSTGRES_DATABASE: dbname
    POSTGRES_USER: user
    POSTGRES_PASSWORD: password
    POSTGRES_EXTRA_OPTS: '--schema=public --blobs'
```
