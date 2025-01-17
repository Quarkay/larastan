# Custom config parameters

All custom config parameters that are defined by Larastan are listed here.

## `noUnnecessaryCollectionCall`, `noUnnecessaryCollectionCallOnly`, `noUnnecessaryCollectionCallExcept`

These parameters are related to the `NoUnnecessaryCollectionCall` rule. You can find the details about these parameters and the rule [here](rules.md#NoUnnecessaryCollectionCall).

## `databaseMigrationsPath`

By default, the default Laravel database migration path (`database/migrations`) is used to scan migration files to understand the table structure and model properties. If you have database migrations in other place than the default, you can use this config parameter to tell Larastan where the database migrations are stored.

You can give absolute paths, or paths relative to the PHPStan config file.

#### Example
```neon
parameters:
    databaseMigrationsPath:
        - app/Domain/DomainA/migrations
        - app/Domain/DomainB/migrations
```

## `squashedMigrationsPath`

By default, Larastan will check `database/schema` directory to find schema dumps. If you have them in other locations or if you have multiple folders, you can use this config option to add them.

#### Example
```neon
parameters:
    squashedMigrationsPath:
        - app/Domain/DomainA/schema
        - app/Domain/DomainB/schema
```

#### PostgreSQL

The package used to parse the schema dumps, [phpmyadmin/sql-parser](https://github.com/phpmyadmin/sql-parser), is primarily focused on the MySQL dialect.
It can read (or rather, try to read) PostgreSQL dumps provided they are in the *plain text (and not the 'custom') format*, but the mileage may vary as problems have been noted with timestamp columns and lengthy parse time on more complicated dumps.

The viable options for PostgreSQL at the moment are:
1. Use the [laravel-ide-helper](https://github.com/barryvdh/laravel-ide-helper) package to write PHPDocs directly to the Models. 
2. Use the [laravel-migrations-generator](https://github.com/kitloong/laravel-migrations-generator) to generate migration files (or a singular squashed migration file) for Larastan to scan with the `databaseMigrationsPath` setting.

## `checkModelProperties`
**default**: `false`

This config parameter enables the checks for model properties that are passed to methods. You can read the details [here](rules.md#modelpropertyrule).

To enable you can set it to `true`:

```neon
parameters:
    checkModelProperties: true
```
