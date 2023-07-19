# Project Description
 This is Google local service ranking tracker project. 
 User can track their business ranking on Google. 
 Also, they can also see their business's status with map having ranking points and graph analysis.

# Challenges:

1: Reducing the responsiveness and uploading bulk CSV file time using background processing of Laravel Queue and Job.
 
In this project, we bring the LSA ranking data from API.
We have to bring the data for each point in a radius of 30 km from the selected location. In this case, we usually have 60 ~ 300 ranking points.
This means we need to call API 60 ~ 300 times.
Also, we have to load the keywords and location from the bulk CSV file. It also needs more time.
If we use the original foreground method, we can't reach out for the responsiveness time because each API calling needs about a second.
So, I processed that in the background using a Laravel queue and used the parallel method with several queues.
Also, found the best number of processes according to the state of the server.
 
2: Data fetch using the scheduler.
 
In this project, we have to get the ranking data every five minutes for a premium account and every hour for a free account. 
Also, we have to generate the weekly report automatically so that user can see their business ranking, reviews, competitors and so on.
In Laravel, to implement this function, we usually use Cron.
But recently, we don't use the Cron for safe processes on the server side.
So, I used the Laravel Scheduler. 
I built the customized php artisan commands and connected them to the scheduler.
And then registered the scheduler in the server.
Every schedule process was perfect.
 
3: API calling with Random proxy.
 
To get the LSA ranking, we have to use the proxy.
But sometimes, the proxy fails due to proxy server issues.
It was a very serious error.
To fix this problem, a special method has been implemented.
First, I created the database table with 500 proxies.
And then created the failed proxy table in the database.
When we call the API to get the data, we select the random proxy from 500 proxies.
If the proxy failed, it is sent to the failed proxy table. And then we choose another random proxy. 
We save the failed proxy table and so, we don't use the failed proxies again.
This method was very efficient and solved the proxy failed error.
 
4: Screenshot a Google map with ranking points for the report.
To generate the report, we have to screenshot the Google map with ranking points so that the user can see the rankings on the map.
I used the Puppeteer Node.js library. 
The main problem is that the cPanel server doesn't support the Chrome GUI mode in general mode. In this case, we have to install an additional Graphic environment such as Xorg.
But, doing so adversely affects the server performance. 
 
So, I used the Puppeteer headless mode and, in this case, we don't need to install an additional environment in the server because it uses the headless mode of the browser.
 
5: PHP version management.
When I built the project in Local, I used the latest PHP version.
However, the cPanel server supported only PHP 8.1.9.
So, I managed the PHP version.
 
6: Google Authentication, Email notification and Weekly report
This project use Google auth. 
Users receive the email notification when the new competitors appear.
And weekly reports are emailed to you with details.

# Deployment:
<a href="https://app.lsaranktracker.com">Demo</a>
The project is deployed in cPanel server. 


<p align="center"><a href="https://laravel.com" target="_blank"><img src="https://raw.githubusercontent.com/laravel/art/master/logo-lockup/5%20SVG/2%20CMYK/1%20Full%20Color/laravel-logolockup-cmyk-red.svg" width="400" alt="Laravel Logo"></a></p>

<p align="center">
<a href="https://github.com/laravel/framework/actions"><img src="https://github.com/laravel/framework/workflows/tests/badge.svg" alt="Build Status"></a>
<a href="https://packagist.org/packages/laravel/framework"><img src="https://img.shields.io/packagist/dt/laravel/framework" alt="Total Downloads"></a>
<a href="https://packagist.org/packages/laravel/framework"><img src="https://img.shields.io/packagist/v/laravel/framework" alt="Latest Stable Version"></a>
<a href="https://packagist.org/packages/laravel/framework"><img src="https://img.shields.io/packagist/l/laravel/framework" alt="License"></a>
</p>

## About Laravel

Laravel is a web application framework with expressive, elegant syntax. We believe development must be an enjoyable and creative experience to be truly fulfilling. Laravel takes the pain out of development by easing common tasks used in many web projects, such as:

- [Simple, fast routing engine](https://laravel.com/docs/routing).
- [Powerful dependency injection container](https://laravel.com/docs/container).
- Multiple back-ends for [session](https://laravel.com/docs/session) and [cache](https://laravel.com/docs/cache) storage.
- Expressive, intuitive [database ORM](https://laravel.com/docs/eloquent).
- Database agnostic [schema migrations](https://laravel.com/docs/migrations).
- [Robust background job processing](https://laravel.com/docs/queues).
- [Real-time event broadcasting](https://laravel.com/docs/broadcasting).

Laravel is accessible, powerful, and provides tools required for large, robust applications.

## Learning Laravel

Laravel has the most extensive and thorough [documentation](https://laravel.com/docs) and video tutorial library of all modern web application frameworks, making it a breeze to get started with the framework.

You may also try the [Laravel Bootcamp](https://bootcamp.laravel.com), where you will be guided through building a modern Laravel application from scratch.

If you don't feel like reading, [Laracasts](https://laracasts.com) can help. Laracasts contains over 2000 video tutorials on a range of topics including Laravel, modern PHP, unit testing, and JavaScript. Boost your skills by digging into our comprehensive video library.

## Laravel Sponsors

We would like to extend our thanks to the following sponsors for funding Laravel development. If you are interested in becoming a sponsor, please visit the Laravel [Patreon page](https://patreon.com/taylorotwell).

### Premium Partners

- **[Vehikl](https://vehikl.com/)**
- **[Tighten Co.](https://tighten.co)**
- **[Kirschbaum Development Group](https://kirschbaumdevelopment.com)**
- **[64 Robots](https://64robots.com)**
- **[Cubet Techno Labs](https://cubettech.com)**
- **[Cyber-Duck](https://cyber-duck.co.uk)**
- **[Many](https://www.many.co.uk)**
- **[Webdock, Fast VPS Hosting](https://www.webdock.io/en)**
- **[DevSquad](https://devsquad.com)**
- **[Curotec](https://www.curotec.com/services/technologies/laravel/)**
- **[OP.GG](https://op.gg)**
- **[WebReinvent](https://webreinvent.com/?utm_source=laravel&utm_medium=github&utm_campaign=patreon-sponsors)**
- **[Lendio](https://lendio.com)**

## Contributing

Thank you for considering contributing to the Laravel framework! The contribution guide can be found in the [Laravel documentation](https://laravel.com/docs/contributions).

## Code of Conduct

In order to ensure that the Laravel community is welcoming to all, please review and abide by the [Code of Conduct](https://laravel.com/docs/contributions#code-of-conduct).

## Security Vulnerabilities

If you discover a security vulnerability within Laravel, please send an e-mail to Taylor Otwell via [taylor@laravel.com](mailto:taylor@laravel.com). All security vulnerabilities will be promptly addressed.

## License

The Laravel framework is open-sourced software licensed under the [MIT license](https://opensource.org/licenses/MIT).
