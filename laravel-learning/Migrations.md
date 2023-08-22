# migratios

### 1.make a migration

to make a migration type code below in any therminal or powershell:
```
php artisan make:migration databasename
```

### 2. add columns to migration

to add columns add ` $table->` :
- if your column is string --> `$table->string("your col name")`
-

### 3. run a migration file

open your therminal type:
```
php artisan migrate
```
now you have a new database with your custom columns.
#
