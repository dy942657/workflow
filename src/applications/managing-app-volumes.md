# Mounting volumes for an Application

We can use blow command to create volumes and mount which volume is created.
Drycc create volume support [ReadWriteMany](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#access-modes), so before deploy drycc, have a StorageClass ready which support ReadWriteMany.
Deploying drycc, set controller.app_storage_class to this StorageClass.

## Create volume in application

Use `drycc volumes` to mount a volume for a deployed application's processes.

    $ drycc help volumes
    Valid commands for volumes:

    volumes:create           create a volume for the application
    volumes:list             list volumes in the application
    volumes:delete           delete a volume from the application
    volumes:mount            mount a volume to process of the application
    volumes:unmount          unmount a volume from process of the application

    Use 'drycc help [command]' to learn more.

You can create a volume with one `drycc volumes:create` command

    $ drycc volumes:create myvolume 200M
    Creating myvolumes to scenic-icehouse... done

After volume created, you can list the volumes in this application.

    $ drycc volumes:list
    === scenic-icehouse volumes
    --- myvolumes     200M

## Mounting volume

The volume which is named myvolumes has created, you can mount the volume with process of the application,
use the command of `drycc volumes:mount`. When volume mounted, a new release is created and deployed automatically.

    $ drycc volumes:mount myvolumes web=/data/web
    Mounting volume... done

And use `drycc volumes:list` show mount detail.

    $ drycc volumes:list
    === scenic-icehouse volumes
    --- myvolumes     200M
    web               /data/web

If you don't need volume, use `drycc volumes:unmount` unmount the volume and `drycc volumes:delete` delete volume in the application.
Before deleting volume, the volume has to unmounted.

    $ drycc volumes:unmount myvolumes web
    Unmounting volume... done

    $ drycc volumes:delete myvolumes
    Deleting myvolumes from scenic-icehouse... done
