# how to deploy To heroku

**Get app ready**

1. Specify version of node in package.json

2. Specify a start script
 Mine: &quot;start&quot;: &quot;node -r dotenv/config index.js&quot;
[https://devcenter.heroku.com/articles/deploying-nodejs#specifying-a-start-script](https://devcenter.heroku.com/articles/deploying-nodejs#specifying-a-start-script)

If no start script, create a procfile to start up your app via a different script

**Dev dependencies aren&#39;t included**

**Start Up Heroku**

1. Signup for Heroku
[https://signup.heroku.com/](https://signup.heroku.com/)

2. Install Heroku CLI
[https://devcenter.heroku.com/articles/heroku-cli](https://devcenter.heroku.com/articles/heroku-cli)

3. Login
 heroku login

4. Build your app
 heroku create
**OR**
heroku create appname (it&#39;ll tell you if it&#39;s already taken)

5. Deploy your code
 git push heroku main

6. Start your app/dyno
 heroku ps:scale web=1

**Set Up Postgres and Environment variables**

1. Add Heroku Postgres as an add-on (if using Postgres)
[https://elements.heroku.com/addons/heroku-postgresql](https://elements.heroku.com/addons/heroku-postgresql)
 heroku addons:create heroku-postgresql:hobby-dev

2. Push local database to Heroku Postgres
[https://devcenter.heroku.com/articles/heroku-postgresql#pg-push-and-pg-pull](https://devcenter.heroku.com/articles/heroku-postgresql#pg-push-and-pg-pull)
 heroku pg:push mylocaldb DATABASE\_URL --app appname

3. Setup config vars (in settings) – this is equivalent to your env file
 Variables are viewable in the Heroku Postgres settings
 You can skip this if you&#39;re planning on just changing your connection string

4. Edit your database connection
[https://devcenter.heroku.com/articles/getting-started-with-nodejs#provision-a-database](https://devcenter.heroku.com/articles/getting-started-with-nodejs#provision-a-database)
 Include ssl: { rejectUnauthorized: false }

5. Push changes to heroku
 git push heroku master

6. If need be, change time zones
 config vars TZ = Australia/Melbourne
 heroku psql
 ALTER DATABASE dbname SET timezone = &#39;Australia/Melbourne&#39;;

7. If you want, change your env variables to use the heroku database

**Extra commands**

heroku psql = open psql on heroku postgres database

heroku pg:psql --app app\_name \&lt; file.sql = run local script on heroku postgres database

heroku pg:info = get information about heroku postgres
