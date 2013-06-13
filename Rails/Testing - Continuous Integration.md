# Continuous Integration for Fun and Profit

###### [Copied from ndelage's gist of the same name](https://gist.github.com/ndelage/5593921)

### Continu-what?

__Definition:__ _the practice of frequently integrating one's new or changed code with the existing code repository -Wikipedia_

Merging new code into master often sounds awesome, but we've been learning the value of testing and the importance of a passing test __suite__.

__But,__ as your projects grow, your test suite should grow as well. We're all lazy and forget to run the entire test suite everytime we create a new commit. For large projects, running the entire test suite can take _hours_. So we do what all lazy people do, make a computer to the work for us.

### But Nate, I just wanna merge!

...and I don't want to wait for a million tests to run, don't you realize I have things to do??

### Super Build Server to your rescue

A build server will be responsible to run the entire test suite after ever commit and let you know if any tests failed. That way when your change to the `User` model breaks the `Vote` creation integration test, you'll be notified (email) without having to run every test yourself.

If your build passes, then you know you're ready to merge into master.

### Keep master green

As you begin to push your apps to production, you don't want to introduce any bugs in your `master` branch (keep those in your feature branches). With `master` green you can always deploy to production without fear.

### OK. I'm convinced. I can haz build server?

Yes you can. Travis-CI is an automated, hosted build _service_ that we'll be using.

__Requirements__

- a public repository
- .travis.yml file (build configuration)
- tests (duh)

Head over to travis-ci.org and click the login button in the upper right. We'll do the other details together.

#### ```.travis.yml``` file for a RoR project:
```yml
language: ruby
rvm:
  - 1.9.3
env:
  - DB=postgresql
script:
  - bundle exec rake db:migrate
  - bundle exec rake db:test:prepare
  - bundle exec rake spec
before_script:
  - bundle exec rake db:create RAILS_ENV=test
bundler_args: --binstubs=./bundler_stubs
```

