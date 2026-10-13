# Movie Booking System

This is an interview exercise: a Spring Boot app for booking movie tickets.

```bash
git clone https://github.com/LifeAyush/movie-booking-system.git
cd movie-booking-system
chmod +x mvnw
./mvnw spring-boot:run
```

The server listens on port 8081. You need Java 17 and a local MySQL database named `moviedb`. Connection settings are in `src/main/resources/application.properties`. Hibernate creates and updates the tables on startup (`spring.jpa.hibernate.ddl-auto=update`).

Open [http://localhost:8081/](http://localhost:8081/).

## API

The app serves Thymeleaf pages. It is not a JSON API. Sign-in uses Spring Security form login at `/login`. The username field is `email`, and a successful login goes to `/home`. Logout returns to `/`.

These paths require a signed-in user:

| Path | What it does |
| --- | --- |
| `GET /home` | Home page |
| `GET /movielist` | Lists movies. The account `ooadproj@ooadproj.com` is treated as an administrator on this page. |
| `GET /search?keyword=` | Lists movies whose name matches `keyword` (case-insensitive) |
| `GET /new` | Form for adding a movie |
| `GET /book` | Booking form for the signed-in user |
| `GET /profile` | Tickets booked by the signed-in user |
| `GET /confirm` | Booking confirmation |

These paths are open:

| Path | What it does |
| --- | --- |
| `GET /` | Landing page |
| `GET /register` | Sign-up form (email, password, first name, last name) |
| `POST /process_register` | Creates a user and stores a BCrypt password hash |
| `POST /save` | Saves a movie, sets the seat count to 300, then redirects to `/movielist` |
| `GET /edit/{id}` | Edit form for one movie |
| `GET /delete/{id}` | Deletes a movie and redirects to `/` |
| `POST /saveticket` | Books tickets, reduces that movie's remaining seats, then redirects to `/confirm` |
| `GET /deleteticket/{id}` | Cancels a booking, returns those seats, then redirects to `/profile` |
| `GET /error` | Error page |

A movie has a name, genre, description, rating, price, image, parental rating, and seat count. A ticket records the user, movie name, screen, number of tickets, and show time.

## License

Released under the [MIT License](LICENSE). Copyright (c) 2024 Ayush Patil.

Compiled output is checked in under `bin/`, including a team report in `bin/Reports`.
