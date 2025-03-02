# Backend 

This is a basic example of a go web server.

It uses the [go fiber](https://github.com/gofiber/fiber) framework 

## Getting started

### Running locally
Clone this repository
Download and install [golang](https://golang.org)

Download and install [postgres](https://www.postgresql.org/download/)

Setup your postgres database, env secrets can be changed in the [.env](./server/.env) file

- [A complete guide to PostgreSQL](https://prabhupant.medium.com/a-complete-guide-to-postgresql-e4d1cefb9866)

- [Installing PostgreSQL for Mac, Linux, and Windows](https://medium.com/@dan.chiniara/installing-postgresql-for-windows-7ec8145698e3)

Build and run the server. The server is available at `:8081`

## Endpoints
| endpoint      | method | body                                           | description       |
|---------------|--------|------------------------------------------------|-------------------|
| /api/session  | GET    |                                                | GET user session  |
| /api/login    | POST   | { email String, password String }              | login user        |
| /api/logout   | GET    |                                                | logout user       |
| /api/register | POST   | { email String, password String, name String } | register new user |
| /api/ping     | GET    |                                                | health check |
|               |        |                                                |                   |

## License
[MIT](https://choosealicense.com/licenses/mit/)

## Author Information
This app was created by Israel A., edited by Alexandr Anoshin

