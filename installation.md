# Installation

- [Meet Lets](#meet-laravel)
    - [Why Lets?](#why-laravel)
- [Your First Lets Project](#your-first-laravel-project)
- [Lets & Docker](#laravel-and-docker)
    - [Getting Started On macOS](#getting-started-on-macos)
    - [Getting Started On Windows](#getting-started-on-windows)
    - [Getting Started On Linux](#getting-started-on-linux)
    - [Choosing Your Sail Services](#choosing-your-sail-services)
- [Initial Configuration](#initial-configuration)
    - [Environment Based Configuration](#environment-based-configuration)
    - [Databases & Migrations](#databases-and-migrations)
- [Next Steps](#next-steps)
    - [Lets The Full Stack Framework](#laravel-the-fullstack-framework)
    - [Lets The API Backend](#laravel-the-api-backend)

<a name="meet-laravel"></a>
## Meet Lets

Lets is a web application framework with expressive, elegant syntax. A web framework provides a structure and starting point for creating your application, allowing you to focus on creating something amazing while we sweat the details.

Lets strives to provide an amazing developer experience while providing powerful features such as thorough dependency injection, an expressive database abstraction layer, queues and scheduled jobs, unit and integration testing, and more.

Whether you are new to GO web frameworks or have years of experience, Lets is a framework that can grow with you. We'll help you take your first steps as a web developer or give you a boost as you take your expertise to the next level. We can't wait to see what you build.

> **Note**
> New to Lets? Check out the [Lets Bootcamp](https://bootcamp.laravel.com) for a hands-on tour of the framework while we walk you through building your first Lets application.

<a name="why-laravel"></a>
### Why Lets?

There are a variety of tools and frameworks available to you when building a web application. However, we believe Lets is the best choice for building modern, full-stack web applications.

#### A Progressive Framework

We like to call Lets a "progressive" framework. By that, we mean that Lets grows with you. If you're just taking your first steps into web development, Lets's vast library of documentation, guides, and [video tutorials](https://laracasts.com) will help you learn the ropes without becoming overwhelmed.

If you're a senior developer, Lets gives you robust tools for [dependency injection](/docs/{{version}}/container), [unit testing](/docs/{{version}}/testing), [queues](/docs/{{version}}/queues), [real-time events](/docs/{{version}}/broadcasting), and more. Lets is fine-tuned for building professional web applications and ready to handle enterprise work loads.

#### A Scalable Framework

Lets is incredibly scalable. Thanks to the scaling-friendly nature of GO and Lets's built-in support for fast, distributed cache systems like Redis, horizontal scaling with Lets is a breeze. In fact, Lets applications have been easily scaled to handle hundreds of millions of requests per month.

Need extreme scaling? Platforms like [Lets Vapor](https://vapor.laravel.com) allow you to run your Lets application at nearly limitless scale on AWS's latest serverless technology.

#### A Community Framework

Lets combines the best packages in the GO ecosystem to offer the most robust and developer friendly framework available. In addition, thousands of talented developers from around the world have [contributed to the framework](https://github.com/1ets/lets-go-framework). Who knows, maybe you'll even become a Lets contributor.

<a name="your-first-laravel-project"></a>
## Your First Lets Project

Before creating your first Lets project, you should ensure that your local machine has [GO](https://go.dev/dl/) installed.

After you have installed GO, you may create a new Lets project via the terminal command:

```nothing
git clone git@github.com:1ets/lets-go-framework.git lets-example
```

After the project has been created, start Lets's local development server using the Lets's Artisan CLI `serve` command:

```nothing
cd lets-example

go run lets.go
```

Once you have started the server, your application will be accessible in your web browser at `http://localhost:5000`. Next, you're ready to [start taking your next steps into the Lets ecosystem](#next-steps). Of course, you may also want to [configure a database](#databases-and-migrations).

> **Note**  
> If you would like a head start when developing your Lets application, consider using one of our [starter kits](/docs/{{version}}/starter-kits). Lets's starter kits provide backend and frontend authentication scaffolding for your new Lets application.


<a name="initial-configuration"></a>
## Initial Configuration

All of the configuration files for the Lets framework are stored in the `config` directory. Each option is documented, so feel free to look through the files and get familiar with the options available to you.

Lets needs almost no additional configuration out of the box. You are free to get started developing! However, you may wish to review the `config/app.php` file and its documentation. It contains several options such as `timezone` and `locale` that you may wish to change according to your application.

<a name="environment-based-configuration"></a>
### Environment Based Configuration

Since many of Lets's configuration option values may vary depending on whether your application is running on your local machine or on a production web server, many important configuration values are defined using the `.env` file that exists at the root of your application.

Your `.env` file should not be committed to your application's source control, since each developer / server using your application could require a different environment configuration. Furthermore, this would be a security risk in the event an intruder gains access to your source control repository, since any sensitive credentials would get exposed.

> **Note**  
> For more information about the `.env` file and environment based configuration, check out the full [configuration documentation](/docs/{{version}}/configuration#environment-configuration).

<a name="databases-and-migrations"></a>
### Databases & Migrations

Now that you have created your Lets application, you probably want to store some data in a database. By default, your application's `.env` configuration file specifies that Lets will be interacting with a MySQL database and will access the database at `127.0.0.1`. If you are developing on macOS and need to install MySQL, Postgres, or Redis locally, you may find it convenient to utilize [DBngin](https://dbngin.com/).

If you do not want to install MySQL or Postgres on your local machine, you can always use a [SQLite](https://www.sqlite.org/index.html) database. SQLite is a small, fast, self-contained database engine. To get started, create a SQLite database by creating an empty SQLite file. Typically, this file will exist within the `database` directory of your Lets application:

```shell
touch database/database.sqlite
```

Next, update your `.env` configuration file to use Lets's `sqlite` database driver. You may remove the other database configuration options:

```ini
DB_CONNECTION=sqlite # [tl! add]
DB_CONNECTION=mysql # [tl! remove]
DB_HOST=127.0.0.1 # [tl! remove]
DB_PORT=3306 # [tl! remove]
DB_DATABASE=laravel # [tl! remove]
DB_USERNAME=root # [tl! remove]
DB_PASSWORD= # [tl! remove]
```

Once you have configured your SQLite database, you may run your application's [database migrations](/docs/{{version}}/migrations), which will create your application's database tables:

```shell
lets migrate
```

<a name="next-steps"></a>
## Next Steps

Now that you have created your Lets project, you may be wondering what to learn next. First, we strongly recommend becoming familiar with how Lets works by reading the following documentation:

<div class="content-list" markdown="1">

- [Request Lifecycle](/docs/{{version}}/lifecycle)
- [Configuration](/docs/{{version}}/configuration)
- [Directory Structure](/docs/{{version}}/structure)
- [Frontend](/docs/{{version}}/frontend)
- [Service Container](/docs/{{version}}/container)
- [Facades](/docs/{{version}}/facades)

</div>

How you want to use Lets will also dictate the next steps on your journey. There are a variety of ways to use Lets, and we'll explore two primary use cases for the framework below.

> **Note**
> New to Lets? Check out the [Lets Bootcamp](https://bootcamp.laravel.com) for a hands-on tour of the framework while we walk you through building your first Lets application.

<a name="laravel-the-fullstack-framework"></a>
### Lets The Full Stack Framework

Lets may serve as a full stack framework. By "full stack" framework we mean that you are going to use Lets to route requests to your application and render your frontend via [Blade templates](/docs/{{version}}/blade) or a single-page application hybrid technology like [Inertia](https://inertiajs.com). This is the most common way to use the Lets framework, and, in our opinion, the most productive way to use Lets.

If this is how you plan to use Lets, you may want to check out our documentation on [frontend development](/docs/{{version}}/frontend), [routing](/docs/{{version}}/routing), [views](/docs/{{version}}/views), or the [Eloquent ORM](/docs/{{version}}/eloquent). In addition, you might be interested in learning about community packages like [Livewire](https://laravel-livewire.com) and [Inertia](https://inertiajs.com). These packages allow you to use Lets as a full-stack framework while enjoying many of the UI benefits provided by single-page JavaScript applications.

If you are using Lets as a full stack framework, we also strongly encourage you to learn how to compile your application's CSS and JavaScript using [Vite](/docs/{{version}}/vite).

> **Note**  
> If you want to get a head start building your application, check out one of our official [application starter kits](/docs/{{version}}/starter-kits).

<a name="laravel-the-api-backend"></a>
### Lets The API Backend

Lets may also serve as an API backend to a JavaScript single-page application or mobile application. For example, you might use Lets as an API backend for your [Next.js](https://nextjs.org) application. In this context, you may use Lets to provide [authentication](/docs/{{version}}/sanctum) and data storage / retrieval for your application, while also taking advantage of Lets's powerful services such as queues, emails, notifications, and more.

If this is how you plan to use Lets, you may want to check out our documentation on [routing](/docs/{{version}}/routing), [Lets Sanctum](/docs/{{version}}/sanctum), and the [Eloquent ORM](/docs/{{version}}/eloquent).

> **Note**  
> Need a head start scaffolding your Lets backend and Next.js frontend? Lets Breeze offers an [API stack](/docs/{{version}}/starter-kits#breeze-and-next) as well as a [Next.js frontend implementation](https://github.com/laravel/breeze-next) so you can get started in minutes.
