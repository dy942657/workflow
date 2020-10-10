# Managing resources for an Application

We can use blow command to create resources and bind which resource is created.
This command depend on [service-catalog](https://svc-cat.io).

## Create resource in application

Use `drycc resources` to create and bind a resource for a deployed application.

    $ drycc help resources
    Valid commands for resources:

    resources:create           create a resource for the application
    resources:list             list resources in the application
    resources:describe         get a resource detail info in the application
    resources:update           update a resource from the application
    resources:destroy          delete a resource from the applicationa
    resources:bind             bind a resource to servicebroker
    resources:unbind           unbind a resource from servicebroker

    Use 'drycc help [command]' to learn more.

You can create a resource with one `drycc resources:create` command

    $ drycc resources:create memcached:custom memcached
    Creating memcached to scenic-icehouse... done

After resource created, you can list the resources in this application.

    $ drycc resources:list
    === scenic-icehouse resources
    memcached      memcached:custom

## Binding resources

The resource which is named memcached has created, you can bind the memcached with the application,
use the command of `drycc resources:bind memcached`.

    $ drycc resources:bind memcached
    Binding resource... done

And use `drycc resources:describe` show bind detail. If binding successful, this command will show the information of connect to resource.

    $ drycc resources:describe memcached
    === scenic-icehouse resource memcached
    plan:        memcached:custom
    status:      Ready
    binding:     Ready

    HOST:        10.1.7.241 10.1.7.101
    PORT:        11211

## Migrating between plans

You can use the `drycc resources:update` command to migrate to a new plan.
An example of how to upgrade to a 100MB plan:

    $ drycc resources:update memcached:100 memcached
    Updating memcached to scenic-icehouse... done

## Removing the resource

If you don't need resources, use `drycc resources:unbind` unbind the resource and `drycc resources:destroy` delete resource in the application.
Before deleting resource, the resource has to unbind.

    $ drycc resources:unbind memcached
    Unbinding resource... done

    $ drycc resources:destroy memcached
    Deleting memcached from scenic-icehouse... done


