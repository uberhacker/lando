Drupal 7 Example
================

This example exists primarily to test the following documentation:

* [Drupal 7 Recipe](https://docs.devwithlando.io/tutorials/drupal7.html)

Start up tests
--------------

Run the following commands to get up and running with this example.

```bash
# Should poweroff
lando poweroff

# Should initialize the latest Drupal 7 codebase
rm -rf drupal7 && mkdir -p drupal7 && cd drupal7
lando init --source remote --remote-url https://ftp.drupal.org/files/projects/drupal-7.59.tar.gz --remote-options="--strip-components 1" --recipe drupal7 --webroot . --name lando-drupal7

# Should start up succesfully
cd drupal7
lando start
```

Verification commands
---------------------

Run the following commands to validate things are rolling as they should.

```bash
# Should return the drupal installation page by default
cd drupal7
lando ssh -s appserver -c "curl -L localhost" | grep "Drupal 7"

# Should use 7.2 as the default php version
cd drupal7
lando php -v | grep 7.2

# Should be running apache 2.4 by default
cd drupal7
lando ssh -s appserver -c "apachectl -V | grep 2.4"
lando ssh -s appserver -c "curl -IL localhost" | grep Server | grep 2.4

# Should be running mysql 5.7 by default
cd drupal7
lando mysql -V | grep 5.7

# Should not enable xdebug by default
cd drupal7
lando php -m | grep xdebug || echo $? | grep 1

# Should use the default database connection info
cd drupal7
lando mysql -udrupal7 -pdrupal7 drupal7 -e quit

# Should use drush 8.1.x by default
cd drupal7
lando drush version | grep 8.1

# Should be able to install drupal
cd drupal7
lando drush si --db-url=mysql://drupal7:drupal7@database/drupal7 -y

# Verify that drush has infinite memory
cd drupal7
lando drush eval "phpinfo();" | grep memory_limit | grep -e "-1"
```

Destroy tests
-------------

Run the following commands to trash this app like nothing ever happened.

```bash
# Should be destroyed with success
cd drupal7
lando destroy -y
lando poweroff
```
