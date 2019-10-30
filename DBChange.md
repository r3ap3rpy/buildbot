### Swapping out sqlite

This is a fairly easy step. You download [postgres](https://www.postgresql.org/download/), follow the setup with the default values. Then once the DB is up you need to create a database called **buildbot** and a new login **buildbot** with password **buildbot**.

Once this is done you issue the following command.

``` bash
buildbot upgrade-master master
```

Then restart the master to pick up the changes.

``` bash
buildbot restart master.
```