# Rails API Quiz

**Using whatever resources you like (e.g., Google, Stack Overflow, lectures, labs, notes, etc.), answer the following questions.**

1. Write the command to create a new Rails application in API mode with a Postgresql database.
```
rails new my-application-name-api  --api  -d=postgresql
```

2. What are 5 other options that can be passed in to the `rails new` command and what do they do?
```
rails -h //for help

-G no git 
-J no javascript
-T, no tests 

etc. diff functionality can be found in rails -h to see
```

3. What one line of code can be put into `routes.rb` to get all the RESTful routes for a given resource (e.g., dogs)?
```
in the routes rb file
resources :dogs

note* you will be missing new and edit routes, because they are not needed in API*
```

4. In the context of API development, what is versioning? How do we implement versioning in a Rails API?
```
we version our API's because it is a way of changing API functionality in a seamless way. Release diff versions.
Implemented using namespacing. namespace routes and namespace controllers
so in the route file :

namespace :api do
    namespace :v1 do
        resources :movies
    end
end

```

5. What is serialization in reference to a Rails API?
serialization is to make sure its in desired response format (json)
ActiveModel::Serializers
```
Converting our ActiveRecord data into JSON to send back
```

6. Imagine a dog walking domain in which a walker has many dogs. Write the `index` action from the `WalkersController`. Remember, your endpoint should return JSON.
```
def index
    walkers = Walker.all     *note you dont need @ sign now cuz were not needing to access @dogs in view anymore*

    render json: walkers  
end
```

7. Change the code from the question above so that the walkers' dogs get embedded in the JSON being returned from the `index` endpoint.
```
def index
    walkers = Walker.all

    render json: walkers, include: :dogs
end 
```

8. Again, change the code above to exclude the timestamps from the data being returned in the JSON.
```
def index
    walkers = Walker.all

    render json: walkers, include: :dogs, except: [:updated_at, :created_at]
end 
```

9. What does CORS mean? Why do we have to think about it when making an API?
```
Cross Origin Resource Sharing
(for giving permission to the api)
we have to whitelist the origins that we will accept requests from

```

10. What changes do we have to make in our application to allow CORS?

```
1. Set up our CORS initializer file to accept requests
2. Uncomment the CORS gem and bundle
```

11. In our dog walking app, what needs to be added to the following class to allow method calls like `Dog.create(name: "Neikko", breed: "mostly rat", age: 13)` and `Dog.find_by(name: "Neikko")` to function properly?

```
class Dog < ApplicationRecord
end
```

```
Nothing! we already have access because it inherits from ActiveRecord
```




