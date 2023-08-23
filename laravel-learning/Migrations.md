# Migratios

### 1.make a migration

to make a migration type code below in any therminal or powershell:
```
php artisan make:migration databasename
```

### 2. add columns to migration

to add columns add ` $table->` :
- if your column is a text --> `$table->string("your col name")`
- if your column is a number --> `$table->integer("yout col name")`

### 3. run a migration file

open your therminal type:
```
php artisan migrate
```
now you have a new database with your custom columns.
#

# SAFE MIGRATION

use this method for adding table to your existing DB.

### 1.make a new migration.
example: 
```
php artisan make:migration add_colname_to_myDB_table //you can change colname & myDB
```
NOTE: laravel can recognize your request by the migration name. if you type `create_table` laravel fills the file with codes that creates a table. if you type `add_col_to_myDB_table` laravel fills the file with codes that you able to add column to your table after you run the migration.
