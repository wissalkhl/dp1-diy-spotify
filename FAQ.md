# Frequently Asked Questions

Here are some common issues we've seen among student projects:

- "**My API works one day but not the next**" - This is due to a broken database connection, which has to be configured a bit differently for a long-running application like FastAPI. [See the new notes and video in Step Four](https://github.com/uvasds-systems/dp1-diy-spotify/blob/main/README.md#step-four---connect-your-api-with-the-database).
- "**I open up my EC2 instance to test my API but see nothing**" - Check if your browser is trying to use HTTP or HTTPS to reach your instance. Only HTTP will work. See the notes in Step 5 and 6.
- "**My API will not connect to the database, I keep getting an 'admin'@'199.111.xxx.xxx' error in my logs**" - Check that your `DBHOST` and `DBUSER` are correct in your code or ENV variables. But most importantly, when you export or pass your `DBPASS` variable to your application, use single quotes to avoid having to escape the special characters. [See the new notes about setting up your connection string](https://github.com/uvasds-systems/dp1-diy-spotify/blob/main/README.md#2-set-up-your-connection-string) in Step 4. Also, when you run your Docker container in EC2 later in Step 5, pass the variable in wrapped in single quotes:

    ```
    docker run -d -p 80:80 -e DBPASS='xxxxx' ghcr.io/xxx/fastapi-demo:1.xx
    ```

- "**My container is not building for some reason. I can't figure out where to find it**" - When you completed Lab 6 you should have had a `/fastapi-demo` repository in your GitHub account with working builds that created a container for you, associated with that repository. If you do not see it, check your profile page in GitHub and look for the "Packages" tab. There you will find any containers that are being built.
- "**My project has gotten messy and this feels like a lot of pieces to keep track of**" - The best strategy for complex projects is to impose order on your code, your process, and your own work. 

    - Work with separate repositories: It's okay to have one repo for your data project (collecting songs, your frontend, your pacman Lambda function) and another for your FastAPI (the `fastapi-demo` repo)
    - Work in order of steps, seeing the ways the project builds successively. Future steps depend on the previous ones working well.
  
- "**My songs and images aren't showing up properly in the web UI but the names and titles are. How do I fix that?**" - Inspect your `songs` database using PhpMyAdmin and be sure the URLs to your song MP3 files and images are correct. They should have a slash before the song/image file name. Here is a working URL. Note the slash between the bucket website name and the file `1g2ccf9a.jpg`.
 
    ```
    https://nem2p-dp1-spotify.s3.us-east-1.amazonaws.com/1g2ccf9a.jpg
    ```