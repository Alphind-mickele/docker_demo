# Lab to Create an NGINX Container

Use the `docker run` command to launch a new container based on the `nginx` image with the name `web`. Ensure the container is running while detached. To do so, complete the following:

**Run docker:**

      docker run --name web -dt nginx

Check that the container is running:

      docker container ls

Outside of docker, use `ls` too check that we have `webfiles`.
Use `ls webfiles/` and look for `default.conf`.
Use cat `webfiles/default.conf` to check for the location of our expected webroots. In this lab, we're using `/var/www/html/`.

## Configure Nginx
**Create and configure the `/var/www/` directory on the container:**

Create the `/var/www/` directory on the container:

      docker exec web mkdir /var/www

Copy the default `nginx` configuration in `webfiles' to `/etc/nginx/conf.d:`

      docker cp webfiles/default.conf web:/etc/nginx/conf.d/default.conf

Move the webfiles/html documents to `/var/www/`:

      docker cp webfiles/html/ web:/var/www/

Check that the documentation transferred:

      docker exec web ls /var/www/html

Ensure the nginx user and group owns these directories:

      docker exec web chown -R nginx:nginx /var/www/html

Reload docker:

      docker exec web nginx -s reload

**Test and Publish the Website to Port 80**

Test that the configuration was successful by trying to access the website on the container:

**Get our IP address:**

      docker inspect web | grep IPAddress

Copy the IPAddress output.
Use curl <IPAddress> and take a look at the html that appears.
**Create a container for our web image:**

      docker commit web web-image

Launch a new container called `web01` for the image:

      docker run -dt --name web01 -p 80:80 web-image

Check the `localhost` and make sure that we get the same information as we did when we used `curl` on the IP address:

            curl localhost

* Use the IP address provided by the lab and enter it into your preferred web browser. You'll know that you've completed the lab completely when the webpage loads correctly.
* With everything transferred to `web01` and our website working, we can get rid of the `web` container, as it is no longer needed. To do so, stop the container with `docker stop web`, and then remove it with `docker rm web`.