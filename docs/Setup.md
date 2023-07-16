# Setup

First you need to get the 1.10.0.83 client. If you still have Marvel Heroes in your Steam library, you can download it like this:

1. Open the Steam console: steam://open/console

2. Enter the following command: download_depot 226320 226321 2278274898429684559

3. Steam will begin to download the requested client build. There will be no download progress indication.

4. The console will display a message when the download finishes. You can find the client files in the following directory %SteamInstallationDirectory%\steamapps\content\app_226320\depot_226321

You can find depot and manifest ids for other builds on [SteamDB](https://steamdb.info/app/226320/depots/). Some versions of the client have also been uploaded to the [Internet Archive](https://archive.org/).

Then you need to set up a web server to serve SiteConfig.xml and redirect the https AuthTicket request to localhost:8080. You can use either set the server up yourself, or use a solution stack such as WAMP.

1. Set up your preferred web server.

2. Enable HTTPS support ([here](https://gist.github.com/danieldogeanu/081dc198a2d727afd6bf01174990ee8d) are instructions for WAMP)

3. Add the following lines to your virtual host configuration in httpd-ssl.conf:

```
RewriteEngine on
RewriteRule ^/marvelheroes(.*) http://%{HTTP_HOST}:8080$1
```

Now you can actually redirect the client to your server and connect.

1. Create a marvelheroes directory in your web server's www folder and put SiteConfig.xml provided in this repository in it.

2. Edit your ClientConfig.xml file located in "Marvel Heroes\Data\Configs" and replace the SiteConfigLocation value with "localhost/marvelheroes/SiteConfig.xml".

3. Compile and run MHServerEmu.

4. Run MarvelGame.exe with the -nobitraider -nosteam arguments.

5. Log in with any email and password.

If everything works correctly, the server should display client connection information.