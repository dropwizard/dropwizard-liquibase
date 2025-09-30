# Dropwizard Liquibase

[![Build](https://github.com/dropwizard/dropwizard-liquibase/actions/workflows/build.yml/badge.svg)](https://github.com/dropwizard/dropwizard-liquibase/actions/workflows/build.yml)
[![Maven Central](https://maven-badges.herokuapp.com/maven-central/io.dropwizard.modules/dropwizard-liquibase/badge.svg)](https://maven-badges.herokuapp.com/maven-central/io.dropwizard.modules/dropwizard-liquibase/)
[![License](https://img.shields.io/badge/license-Apache%202.0-blue.svg)](https://www.apache.org/licenses/LICENSE-2.0)

Addon bundle for [Dropwizard](https://www.dropwizard.io/) to support [Liquibase](https://www.liquibase.org/) for database migrations.

This project has been split out of the main Dropwizard repository because Liquibase changed their license from Apache 2.0 to the Functionalto Functional Source License (FSL) in Liquibase 5.0.0.

## Usage

Add the `dropwizard-liquibase` dependency to your `pom.xml`:

```xml
<dependency>
    <groupId>io.dropwizard.modules</groupId>
    <artifactId>dropwizard-liquibase</artifactId>
    <version>4.0.0</version>
</dependency>
```

Add the `MigrationsBundle` to your `Application` class:

```java
import io.dropwizard.core.Application;
import io.dropwizard.core.setup.Bootstrap;
import io.dropwizard.core.setup.Environment;
import io.dropwizard.db.DataSourceFactory;
import io.dropwizard.liquibase.MigrationsBundle;

public class MyApplication extends Application<MyConfiguration> {

    public static void main(String[] args) throws Exception {
        new MyApplication().run(args);
    }

    @Override
    public void initialize(Bootstrap<MyConfiguration> bootstrap) {
        bootstrap.addBundle(new MigrationsBundle<MyConfiguration>() {
            @Override
            public DataSourceFactory getDataSourceFactory(MyConfiguration configuration) {
                return configuration.getDataSourceFactory();
            }
        });
    }

    @Override
    public void run(MyConfiguration configuration, Environment environment) {
        // ...
    }
}
```

## Commands

The following commands are available:

* `db drop-all`: Drops all database objects in the configured schema.
* `db dump`: Dumps the current database state to a file.
* `db fast-forward`: Deploys and marks all pending migrations as executed.
* `db generate-docs`: Generates documentation for the database.
* `db migrate`: Migrates the database to the latest version.
* `db prepare-rollback`: Generates a rollback script for the next migration.
* `db rollback`: Rolls back the database to a specific tag.
* `db status`: Shows the status of all migrations.
* `db tag`: Tags the current database state.
* `db test`: Tests the database migrations.
* `db calculate-checksum`: Calculates the checksum of a migration.
* `db clear-checksums`: Clears all checksums.
* `db locks`: Shows the status of all database locks.

## License

This project is licensed under the Apache License, Version 2.0. See the [LICENSE](LICENSE) file for details.

Please note that Liquibase is licensed under the Functional Source License (FSL). See https://fsl.software/ for more information.
