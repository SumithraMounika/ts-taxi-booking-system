## Taxi booking system
[![Build Status](https://travis-ci.org/immanuel192/ts-taxi-booking-system.svg?branch=master)](https://travis-ci.org/immanuel192/ts-taxi-booking-system)
[![Coverage Status](https://coveralls.io/repos/github/immanuel192/ts-taxi-booking-system/badge.svg?branch=master&t=1)](https://coveralls.io/github/immanuel192/ts-taxi-booking-system?branch=master)
[![semantic-release](https://img.shields.io/badge/%20%20%F0%9F%93%A6%F0%9F%9A%80-semantic--release-e10079.svg)](https://travis-ci.org/immanuel192/nest-todo)

### Problem statememt
You are tasked to implement a simple taxi booking system in a 2D grid world with the following criteria:

- The 2D grid world consists of `x` and `y` axis that each fit in a 32 bit integer, i.e. `-2,147,483,648` to `2,147,483,647`.
- There are **3** cars in the system, All three cars should have id `1`, `2` and `3` respectively and initial start location is at origin `(0, 0)`. Note that you can store the car states in memory and there is no need for persistent storage for this exercise.
- A car travels through the grid system will require **1 time unit** to move along the `x` or `y` axis by **1 unit** (i.e. Manhattan distance). For example
    - Car at `(0, 0)` will reach `(0, 2)` in 2 time units.
    - Car at `(1, 1)` will reach `(4, 4)` in 6 time units.
    - More than 1 car can be at the same point at any time.

### APIs

Your service should be running on PORT 8080. For simplicity, you

- **DO NOT** need to implement any form persistent storage. **In memory** data structures will be sufficient for this exercise.
- **DO NOT** need to handle concurrent API calls/data races. The APIs will be triggered **serially**.

There are 3 REST APIs you will need to implement.

#### `POST /api/book`

Your system should pick the nearest available car to the customer location and return the total time taken to travel from the current car location to customer location then to customer destination.

- Request payload
```json
{
  "source": {
    "x": x1,
    "y": y1
  },
  "destination": {
    "x": x2,
    "y": y2
  }
}
```

- Response payload
```json
{
  "car_id": id,
  "total_time": t
}
```
- All car are available initially, and become booked once it is assigned to a customer. It will remain booked until it reaches its destination, and immediately become available again.
- In the event that there are more than one car near the customer location, your service should return the car with the smallest id.
- Only one car be assigned to a customer, and only one customer to a car.
- Cars can occupy the same spot, e.g. car 1 and 2 can be at point (1, 1) at the same time.
- If there is no available car that can satisfy the request, your service should return an empty response, not an error

#### `POST /api/tick`

To facilitate the review of this exercise, your service should expose /api/tick REST endpoint, when called should advance your service time stamp by 1 time unit.

#### `PUT /api/reset` 
Your service should also provide /api/reset REST endpoint, when called will reset all cars data back to the initial state regardless of cars that are currently booked.


### System requirements
Your solution should

- Be implemented using any web framework and/or language of your own choice (e.g. Nodejs, Django, Dropwizard, Play, C#, Go ...etc.)
- Use appropriate algorithms/data structures
- Demonstrate proper software design and engineering practices (i.e. SOLID principles, unit testing ...etc.)
- Be of production quality
- Able to run on Linux
- Contains unit tests and clear instructions on how to build/execute them
- Have clear design/API documentation

   
## Versioning
We use `semantic-release` to generate release notes. This make use of [conventional commit structure](https://www.conventionalcommits.org/en/v1.0.0-beta.4/) for both the notes and release numbers.


### Setup your working environment:
- Create Github and NPM [tokens](https://github.com/immanuel192/semantic-release-sample)
- Export these tokens into your `~/.bash_profile` and source it:
```sh
export GH_TOKEN={your github token}
export NPM_TOKEN={your npm token} # should be optional
```
- Available tasks
```sh
npm install
npm run start:local # to start app
npm run start:local:watch # to start app and watch for any changes
npm run test # to test app
npm run cover # to get code coverage
```

### Using docker
- Run
```sh
docker-compose up -d
```

## API Documentation
There is swagger integrated to help you easier navigate through all exposed restful api. Please follow:
```sh
docker-compose up -d
open http://localhost:8080/docs/
```

### Release Production:
- `npm run release`
