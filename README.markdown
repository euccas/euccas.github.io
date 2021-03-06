## What is Octopress?

Octopress is [Jekyll](https://github.com/mojombo/jekyll) blogging at its finest.

Check out [Octopress.org](http://octopress.org/docs) for guides and documentation.

## How to update files in the master branch

- Make changes in the source branch.
- bundle exec rake gen_deploy

## How to create a new post

- bundle exec rake new_post

## Changelog

- 3/6/2021: Changed to use yajl-ruby (1.3) when doing bundle install. This change is needed because yajl-ruby 1.2.1 is not compatible with ruby version 2.4 and above.