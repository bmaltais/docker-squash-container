docker-squash
=============

This works exactly like the native version of `docker-squash` so familiarize yourself with it's docs at https://github.com/jwilder/docker-squash.

The main difference is you'll need to swap out the `sudo docker-squash` command for `docker run -v /tmp -i myyk/docker-squash` and optionally add volumes for you inputs/outputs.

So if before you had:

    $ docker save <image id> > image.tar
    $ sudo docker-squash -i image.tar -o squashed.tar
    $ cat squashed.tar | docker load

Now you'll have:

    $ alias squash="docker run -v $(pwd)/input:/input -v $(pwd)/output:/output -v /tmp -i squash:1st"
    $ docker save <image id> > input/image.tar
    $ squash docker-squash -i /input/image.tar -o /output/squashed.tar -verbose
    $ squash tar --delete -f output/squashed.tar manifest.json
    $ docker load -i output/squashed.tar 
