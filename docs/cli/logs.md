logs
====

Displays logs for your app

You can optionally filter by a particular service, show timestamps or follow the logs a la `tail -f`.

> #### Info::Only shows logs written to `stdout` or `stderr`
>
> Note that `lando logs` is a light wrapper around `docker logs` and as such it will only display logs that are written
> to `stdout` of `stderr`. While we make a best effort to redirect logs when we can it is up to the user to redirect relevant
> application logs.

Usage
-----

```bash
# Get the logs=z
lando logs

# Follow the logs and show timestampls
lando logs -t -f

# Show logs for only the database and cache services
lando logs -s cache -s database
```

Options
-------

Run `lando logs --lando` to get a complete list of options defaults, choices, etc.

```bash
--clear           Clears the lando tasks cache
--follow, -f      Follow the logs
--lando           Show help for lando-based options
--services, -s    Show logs for the specified services only
--timestamps, -t  Show log timestamps
--verbose, -v     Runs with extra verbosity
--version         Show version number
```
