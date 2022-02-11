# Rails Engine Lite
> A Rails project that exposes API endpoints for a fictional Etsy clone. 

Rails Engine Lite is a backend Rails application that provides API endpoints related to merchants, items, and the items merchants sell. 

![](header.png)

## Setup

1. clone this repository 
2. cd into 'rails-engine-lite' directory 
3. run 'bundle install' to install gems
4. run rake db:{drop,create,migrate,seed} to prepare the database 
5. run rails db:schema:dump 
6. run 'bundle exec rspec' to run the test suite
7. run 'rails s' to launch the production environment

That's it! You can view the database structure by running rails c in the terminal and querying the database. Try Item.all. 
Alternatively, you can view the ActiveRecord relationships by placing a pry "binding.pry" in the specs and querying the database. Try Merchant.all this time. 

```

## Usage example: retrieving JSON data from endpoints 
Start the application server with rails -s, then run $ curl localhost:300/api/v1/endpoint_you_want
possible endpoints and their data are as follows: 


## Development setup
ruby 2.7.2
rails 5.2.6

## Meta

Your Name – [@YourTwitter](https://twitter.com/dbader_org) – YourEmail@example.com

Distributed under the XYZ license. See ``LICENSE`` for more information.

[https://github.com/yourname/github-link](https://github.com/dbader/)

## Contributing

1. Fork it (<https://github.com/yourname/yourproject/fork>)
2. Create your feature branch (`git checkout -b feature/fooBar`)
3. Commit your changes (`git commit -am 'Add some fooBar'`)
4. Push to the branch (`git push origin feature/fooBar`)
5. Create a new Pull Request

<!-- Markdown link & img dfn's -->
[npm-image]: https://img.shields.io/npm/v/datadog-metrics.svg?style=flat-square
[npm-url]: https://npmjs.org/package/datadog-metrics
[npm-downloads]: https://img.shields.io/npm/dm/datadog-metrics.svg?style=flat-square
[travis-image]: https://img.shields.io/travis/dbader/node-datadog-metrics/master.svg?style=flat-square
[travis-url]: https://travis-ci.org/dbader/node-datadog-metrics
[wiki]: https://github.com/yourname/yourproject/wiki
