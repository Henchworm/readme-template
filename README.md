# Sweater Weather 
> A rails backend for a service oriented application. A user can request and receieve data from endpoints to plan road trips. Endpoints include querying weather forecasts for a destination, drive time between two destinations, and background image resources for the front end. 
Multiple API endpoints are consumed for each call, their data is integrated into the JSON body of sweater-weather's response. 

## Schema
```
  create_table "users", force: :cascade do |t|
    t.string "email"
    t.string "api_key"
    t.string "password_digest"
    t.datetime "created_at", null: false
    t.datetime "updated_at", null: false
  end
end
```

## Design Principles: 
The design of this application relies on the facade design pattern. Here's a very high level overview: 
A controller receives a request from the front end and intiates the creation of a facade, and passes it data(params, from JSON or query). 
A facade is a ruby class that initializes a Service, and sends the service data to a PORO. 
A service calls an external api enpoint(get (https://web.site?optional_param) and returns parsed JSON. 
The parsed JSON is turned into a Ruby object through a PORO. 
The object is serialized and sent to the route matching the controller action. 

That's a lot, right? To see it step-by-step in action, if you checkout and pull down ```pry-branch``` you can pry ever step of the way! Just exit each pry to move on when you are finished exploring each section. 

I chose to keep my POROs as close to the original JSON response as possible, but filtering out all irrelevant data. You can see an example of this in the test (that one JSON test). 

## Setup

1. clone this repository 
2. cd into 'sweater-weather' directory 
3. run ```'bundle install' to install gems```
4. run ```rake db:{drop,create,migrate,seed} to prepare the database ```
6. run ```bundle exec rspec``` to run the test suite
7. run ```rails s``` to launch the production environment
8. send requests to "https://localhost:3000"! List of requests and anticipated responses below. 

That's it! I reccomend using Postman for the requests, as it's easy to format a request by adding it to the "raw body" of a 
POST request. All endpoints and request bodies here: 
GET http://localhost:3000/api/v1/forecast?location=denver,co&Content-Type=application/json&Accept
Response: 
```
{
    "data": {
        "id": null,
        "type": "forecast",
        "attributes": {
            "current_weather": {
                "datetime": "2022-03-08T12:31:50.000-07:00",
                "sunrise": "2022-03-08T06:22:28.000-07:00",
                "sunset": "2022-03-08T17:59:10.000-07:00",
                "temperature": 36.45,
                "feels_like": 31.53,
                "humidity": 29,
                "uvi": 3.61,
                "visibility": 10000,
                "conditions": null,
                "icon": "01d"
            },
            "daily_weather": [
                {
                    "date": "2022-03-08",
                    "sunrise": "2022-03-08T06:22:28.000-07:00",
                    "sunset": "2022-03-08T17:59:10.000-07:00",
                    "max_temp": 36.45,
                    "min_temp": 20.25,
                    "conditions": "clear sky",
                    "icon": "01d"
                },
                {
                    "date": "2022-03-09",
                    "sunrise": "2022-03-09T06:20:54.000-07:00",
                    "sunset": "2022-03-09T18:00:13.000-07:00",
                    "max_temp": 28.31,
                    "min_temp": 16.97,
                    "conditions": "light snow",
                    "icon": "13d"
                },
                {
                    "date": "2022-03-10",
                    "sunrise": "2022-03-10T06:19:19.000-07:00",
                    "sunset": "2022-03-10T18:01:16.000-07:00",
                    "max_temp": 24.76,
                    "min_temp": 14.38,
                    "conditions": "snow",
                    "icon": "13d"
                },
                {
                    "date": "2022-03-11",
                    "sunrise": "2022-03-11T06:17:45.000-07:00",
                    "sunset": "2022-03-11T18:02:18.000-07:00",
                    "max_temp": 33.85,
                    "min_temp": 14.31,
                    "conditions": "clear sky",
                    "icon": "01d"
                },
                {
                    "date": "2022-03-12",
                    "sunrise": "2022-03-12T06:16:09.000-07:00",
                    "sunset": "2022-03-12T18:03:20.000-07:00",
                    "max_temp": 53.56,
                    "min_temp": 27.77,
                    "conditions": "clear sky",
                    "icon": "01d"
                }
            ],
            "hourly_weather": [
                {
                    "time": "12:00:00",
                    "temperature": 35.62,
                    "conditions": "clear sky",
                    "icon": "01d"
                },
                {
                    "time": "13:00:00",
                    "temperature": 36.45,
                    "conditions": "clear sky",
                    "icon": "01d"
                },
                {
                    "time": "14:00:00",
                    "temperature": 36.14,
                    "conditions": "clear sky",
                    "icon": "01d"
                },
                {
                    "time": "15:00:00",
                    "temperature": 36.05,
                    "conditions": "clear sky",
                    "icon": "01d"
                },
                {
                    "time": "16:00:00",
                    "temperature": 35.83,
                    "conditions": "clear sky",
                    "icon": "01d"
                },
                {
                    "time": "17:00:00",
                    "temperature": 34.54,
                    "conditions": "clear sky",
                    "icon": "01d"
                },
                {
                    "time": "18:00:00",
                    "temperature": 31.28,
                    "conditions": "clear sky",
                    "icon": "01n"
                },
                {
                    "time": "19:00:00",
                    "temperature": 30.36,
                    "conditions": "clear sky",
                    "icon": "01n"
                }
            ]
        }
    }
}
```






Never used Postman? [Check it out here.](https://www.postman.com/postman/workspace/postman-public-workspace/documentation/12959542-c8142d51-e97c-46b6-bd77-52bb66712c9a)

For further testing of requests, check out ```spec api/v1/requests``` for a complete list of requests and a detailed breakdown of the structure of the app's response Ruby-parsed JSON. 

## Development setup
```ruby 2.7.2```

```rails 5.2.6```

## Gems

![pry v badge](https://img.shields.io/gem/v/pry?color=blue&label=pry)
![shoulda-matchers v badge](https://img.shields.io/gem/v/shoulda-matchers?label=shoulda-matchers)
![rspec v badge](https://img.shields.io/gem/v/rspec?color=orange&label=rspec)
![simplecov v badge](https://img.shields.io/gem/v/simplecov?color=green&label=simplecov)
]![json-apiserializer](https://img.shields.io/badge/json-apiserializer-green)

## Contributing

1. fork it (<https://github.com/Henchworm/rails-engine/fork>)
2. create your feature branch (`git checkout -b feature/myfeature`)
3. use TDD
4. commit your changes (`git commit -am 'Add new merchant'`)
5. push to the branch (`git push origin feature/myfeature`)
6. create a new pull request

## Who am I?

Chris Hewitt – [My Cool Website That's Mostly About Music](http://www.goldenbullfrog.com/) – agop5134@gmail.com


[https://github.com/Henchworm/](https://github.com/Henchworm/)



