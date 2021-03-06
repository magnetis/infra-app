# Infra-app

It contains an HTTP server implementation. It responds to all HTTP requests to the URI paths `/app`, `/admin` and `/healthz`.

## Basic instructions

To run in development, just run:

```sh
PORT=5000 ADMIN_USER=myuser ADMIN_PASS=s3cr3t go run main.go
```

To build, just run:

```sh
go build -o app
PORT=5000 ./app
```

By using the GOOS and GOARCH environment variables, you can control which OS and architecture your final binary is built for.

```sh
GOOS=linux GOARCH=amd64 go build -o app

# to check the type of file
file app
app: ELF 64-bit LSB executable, x86-64, version 1 (SYSV), statically linked, Go BuildID=VlCWiOY1myXoArwKJ8-P/gL-oXKeuH4tOr4nCvhNv/6WUnDAZ95hnz49f7CeAV/Lg9OfRg0c1768RSFbAi4, not stripped
```

## How to use

```sh
$ curl -i http://127.0.0.1:5000/app
HTTP/1.1 200 OK
Content-Type: application/json
Date: Fri, 26 Jun 2020 20:14:57 GMT
Content-Length: 95

{
  "app": "Infra Go App",
  "hostname": "ebc919dc7272",
  "version": "0.0.3",
  "zone": "public"
}
```

```sh
$ curl -i -u myuser:s3cr3t  http://127.0.0.1:5000/admin
HTTP/1.1 200 OK
Content-Type: application/json
Date: Fri, 26 Jun 2020 20:14:57 GMT
Content-Length: 95

{
  "app": "Infra Go App",
  "hostname": "ebc919dc7272",
  "version": "0.0.3",
  "zone": "private"
}
```

```sh
$ curl -i http://127.0.0.1:5000/healthz
HTTP/1.1 200 OK
Date: Fri, 26 Jun 2020 20:14:53 GMT
Content-Length: 0
```
