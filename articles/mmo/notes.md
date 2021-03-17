- clone

- flyctl init

  ```
  ? App Name (leave blank to use an auto-generated name) ex-venture

  Automatically selected personal organization: Christopher Keele

  ? Select builder: Dockerfile
      (Do not set a builder and use the existing Dockerfile)
  Error We need your payment information to continue! Add a credit card or buy credit: https://fly.io/organizations/personal
  ```
- flyctl init
  ```
  ? App Name (leave blank to use an auto-generated name) ex-venture

  Automatically selected personal organization: Christopher Keele

  ? Select builder: Dockerfile
      (Do not set a builder and use the existing Dockerfile)
  ? Select Internal Port: 4000
  New app created
    Name         = ex-venture
    Organization = personal
    Version      = 0
    Status       =
    Hostname     = <empty>

  App will initially deploy to sea (Seattle, Washington (US)) region

  Wrote config file fly.toml
  ```

- flyctl deploy
  
  ```
  2021-03-10T18:53:45Z [info] 18:53:45.518 [info] Application ex_venture exited: ExVenture.Application.start(:normal, []) returned an error: shutdown: failed to start child: ExVenture.Repo
  2021-03-10T18:53:45Z [info] ENV vars not set: DATABASE_URL, POOL_SIZE
  2021-03-10T18:53:45Z [info]         ** (Vapor.LoadError) There were errors loading configuration:
  2021-03-10T18:53:45Z [info]             (vapor 0.10.0) lib/vapor.ex:42: Vapor.load!/1

  ***v0 failed - Failed due to unhealthy allocations - no stable job version to auto revert to

  Troubleshooting guide at https://fly.io/docs/getting-started/troubleshooting/
  ```

- flyctl postgres create

  ```
  ? App name: ex-venture-db
  Automatically selected personal organization: Christopher Keele
  ? Select region: sea (Seattle, Washington (US))
  ? Select VM size: shared-cpu-1x - 256
  ? Volume size (GB): 10
  Creating postgres cluster ex-venture-db in organization personal
  Postgres cluster ex-venture-db created
    Username:    postgres
    Password:    4d68908453686d2c03fb445d9f8aeeb13b18cab060a4a027
    Hostname:    ex-venture-db.internal
    Proxy Port:  5432
    PG Port: 5433
  Save your credentials in a secure place, you won't be able to see them again!

  Monitoring Deployment
  You can detach the terminal anytime without stopping the deployment

  2 desired, 2 placed, 2 healthy, 0 unhealthy [health checks: 6 total, 6 passing]
  --> v0 deployed successfully

  Connect to postgres
  Any app within the personal organization can connect to postgres using the above credentials and the hostname "ex-venture-db.internal."
  For example: postgres://postgres:4d68908453686d2c03fb445d9f8aeeb13b18cab060a4a027@ex-venture-db.internal:5432
  ```

- flyctl scale show

  ```
  VM Resources for ex-venture
        VM Size: shared-cpu-1x
      VM Memory: 256 MB
          Count: 1
  ```

- flyctl secrets set DATABASE_URL=postgres://postgres:4d68908453686d2c03fb445d9f8aeeb13b18cab060a4a027@ex-venture-db.internal:5432 POOL_SIZE=2

- flyctl pg attach

  ```
  Error Could not resolve App
  ```

- flyctl pg attach --app ex-venture --postgres-app ex-venture-db

  ```
    Postgres cluster ex-venture-db is now attached to ex-venture
    The following secret was added to ex-venture:
      DATABASE_URL=postgres://ex_venture_yk19l8qd5r6nvgqe:6d373f2d73885d24baad95c66758234c@ex-venture-db.internal:5432/ex_venture?sslmode=disable
    ```

  - flyctl deploy
    ```
    2021-03-10T21:06:03Z [info] 21:06:03.059 [info] Application ex_venture exited: ExVenture.Application.start(:normal, []) returned an error: shutdown: failed to start child: Web.Endpoint
  2021-03-10T21:06:03Z [info]     ** (EXIT) an exception was raised:
  2021-03-10T21:06:03Z [info]         ** (Vapor.LoadError) There were errors loading configuration:
  2021-03-10T21:06:03Z [info] ENV vars not set: PORT, SECRET_KEY_BASE, HOST, URL_PORT, URL_SCHEME
  ```

- flyctl secrets set PORT=4000 SECRET_KEY_BASE=fBvLEEUJd7ylAK21fjJ2I1CzolZPXO/aEjQ0VLBA1KHBkY4GSGvypJGBZTSX8zQf HOST=ex-venture.fly.dev URL_PORT=80 URL_SCHEME=http

- flyctl secrets set URL_PORT=443 URL_SCHEME=https

- flyctl deploy
  ```

  ```

- flyctl open

- change pg inets

- register -> 500

- env dev, log level debug

  ```
  2021-03-10T21:42:09.112Z 2313bea6 sea [info] Request: POST /register
  2021-03-10T21:42:09.113Z 2313bea6 sea [info]     ** (Postgrex.Error) ERROR 42P01 (undefined_table) relation "users" does not exist
  2021-03-10T21:42:09.115Z 2313bea6 sea [info]     query: INSERT INTO "users" ("email","email_verification_token","password_hash","token","username","inserted_at","updated_at") VALUES ($1,$2,$3,$4,$5,$6,$7) RETURNING "id"
  ```

- wireguard setup

- ecto migration

- flyctl regions add ams

- flyctl status

  ```
  App
  Name     = ex-venture
  Owner    = personal
  Version  = 13
  Status   = running
  Hostname = ex-venture.fly.dev

  Deployment Status
    ID          = 4425a0cd-72b8-cfbf-ac8e-aab1420fc3b3
    Version     = v13
    Status      = running
    Description = Deployment is running
    Instances   = 2 desired, 2 placed, 0 healthy, 0 unhealthy

  Instances
  ID       VERSION REGION DESIRED STATUS  HEALTH CHECKS      RESTARTS CREATED
  3e3ac0c1 13      ams    run     pending                    0        5s ago
  c35a6cdb 13      sea    run     running 1 total, 1 passing 0        2m3s ago
  ```

  