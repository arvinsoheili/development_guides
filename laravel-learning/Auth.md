# AUTH
### Auth setup

1. open therminal type `php artisan vue --auth`
auth dir with it views will create in views dir.

2. in therminal type `npm install` then `npm run dev`
   this will install all front ends for us.

### Protected Routes

1. go to your routes find your target route at the end of it type:
```
route::get('/route', 'controller')->middleware('auth');
```
