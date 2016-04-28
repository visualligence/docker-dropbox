### docker-dropbox

Docker image that serves a static site from dropbox

### Setup

Environment variable `DROPBOX_FOLDER` sets which dropbox folder to use for
hugo files.

First start a container:
```
docker run --rm -e DROPBOX_FOLDER="www" -p 80:80 visualligence/docker-dropbox
```
After a while you will see log messages from dropboxd:
 ```
This computer isn't linked to any Dropbox account...
Please visit https://www.dropbox.com/cli_link_nonce?nonce=.... to link this device.
 ```
Visit the link in a browser logged in with the dropbox account you want to
link. Once linked files will start to be synced and hugo will start running.

Now your site should be available at `http://docker-host`

### docker-compose

```
dropbox:
  image: visualligence/docker-dropbox
  restart: always
  environment:
    DROPBOX_FOLDER: www
```

Run `docker-compose up -d` and check logs `docker-compose logs`

### Tips

You most probably want to create a dedicated dropbox account for docker-dropbox
and share a collaborative folder with it. That way it does not sync and have
access to your other files.

To preserve dropbox configuration and data i suggest letting docker-compose
take care of it or create a data only container and use `--volumes-from`.
