# Ecommerce Auth Demo

Java 8, Hibernate, JSP/Servlet demo for role-based signup and login with email OTP.

## Features

- Customer/Admin role selection during signup
- Password hashing with PBKDF2
- Email OTP for signup verification
- Email OTP for every login
- OTP expiry and resend flow
- Role-aware dashboard after successful login
- MySQL default Hibernate configuration with Oracle alternative included

## Requirements

- JDK 8
- Maven 3
- Apache Tomcat 9
- MySQL 8 or Oracle
- SMTP account for sending OTP email

## Database

For MySQL:

```sql
SOURCE database/mysql-schema.sql;
```

Hibernate is configured with `hbm2ddl.auto=update`, so it can also create/update tables automatically after the database exists.

Update `src/main/resources/hibernate.cfg.xml` with your database username and password.

## Email OTP Setup

Update `src/main/resources/mail.properties`:

```properties
mail.username=your-email@gmail.com
mail.password=your-app-password
mail.from=your-email@gmail.com
```

For Gmail, use an app password instead of your normal account password.

## Build and Run

```bash
mvn clean package
```

Deploy `target/ecommerce-auth.war` to Tomcat 9, then open:

```text
http://localhost:8080/ecommerce-auth/
```

## Flow

1. Signup with full name, email, password, and role.
2. System stores the user and sends a signup OTP.
3. User verifies OTP and lands on the dashboard.
4. On future login, password validation succeeds first, then a login OTP is sent.
5. User verifies OTP and receives a session with role-based dashboard access.
