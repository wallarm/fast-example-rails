# README

This is an example of integration Wallarm FAST with the simple Ruby on Rails application using RSpec, Capybara and Selenium.

Learn more about Wallarm FAST: https://wallarm.com/products/fast

## How to run tests

Install docker and docker-compose

Create your FAST node here:
https://us1.my.wallarm.com/nodes

```sh
export WALLARM_API_TOKEN=<YOUR WALLARM NODE TOKEN>

sudo -E docker-compose build

# Run tests & record baselines
sudo -E docker-compose up -d fast selenium
sudo -E docker-compose run --use-aliases app-test bundle exec rspec spec/features/posts_spec.rb
sudo -E docker-compose down

# Run security tests based on recorded baselines
sudo -E docker-compose up -d app-test
sudo -E docker-compose run --rm -e CI_MODE=testing -e TEST_RUN_URI=http://app-test:3000 fast
sudo -E docker-compose down
```

Results of security tests will be here: https://us1.my.wallarm.com/testing/?status=all

For full FAST documentation, visit: https://docs.fast.wallarm.com
