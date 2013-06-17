# Heroku

## Index
-[Getting Started with Rails 3.x on Heroku]

---

## [Getting Started with Rails 3.x on Heroku](https://devcenter.heroku.com/articles/rails3#deploy-your-application-to-heroku)

Deploy your code

        $ git push heroku master

Ensure you have one [dyno](https://devcenter.heroku.com/articles/dynos) running

        $ heroku ps:scale web=1

Check the state of your [dynos](https://devcenter.heroku.com/articles/dynos)

        $ heroku ps

Visit the app

        $ heroku open


---

## References

[Heroku Dev Center](https://devcenter.heroku.com/)
- [Deploying with Git](https://devcenter.heroku.com/articles/git)
- [Getting Started with Ruby](https://devcenter.heroku.com/articles/ruby)
- [Postgres](https://devcenter.heroku.com/articles/heroku-postgresql)



## INBOX


        $ heroku create

        $ git push heroku master

        $ git push heroku yourbranch:master

        $ heroku restart

        $ heroku run rake db:mibrate

        $ heroku logs --tail
