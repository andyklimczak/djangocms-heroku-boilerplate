### Deploying super basic djangocms application to Heroku with AWS S3

0. Clone repo
0. `cp ._env_example .env`
0. Create a new postgres database `createdb djangocms_test`. Set the database url in `.env`
  Note that you might have to edit `pg.cof` to `trust` connections on localhost
0. Create an AWS S3 bucket following the [instructions here](https://www.caktusgroup.com/blog/2014/11/10/Using-Amazon-S3-to-store-your-Django-sites-static-and-media-files/)  Also follow the CORS instructions at the bottom of the guide
0. Edit `.env` with the 3 AWS values needed to connect to your S3 bucket
0. Start the project locally,
  ```
    python manage.py migrate
    python manage.py createsuperuser
    python manage.py runserver
  ```
0. Login to project (`localhost:8000`) and create a page with an `Image` component to test S3 is setup correctly locally
0. Create new Heroku project, using the `postgres` addon and `heroku/python` build pack
0. In the `Settings` tab of your Heroku project, add your 3 AWS environment variables, `SECRET_KEY` variable, add `DISABLE_COLLECTSTATIC` env variable with value of `1`.
0. Deploy the project to Heroku `heroku push https://git.heroku...`
0. Run the djangocms migrations on your heroku instance `heroku run python manage.py migrate`
0. Create a django admin user to log in to start making content `heroku run python manage.py createsuperuser`
0. Go to your Heroku project, create a page, and add an `Image` component to make sure S3 is correctly setup.

If you spot anything incorrect, create an issue and let me know!
