# FlaskRequestGuard

Flask Request Guard is a Python library for validating incoming HTTP requests in Flask web applications. 
It provides a simple yet flexible way to define request rules and enforce them automatically on incoming
 requests, ensuring that only requests that meet the specified requirements are allowed to proceed. 


## Installation
Use the package manager [pip](https://pip.pypa.io/en/stable/) to intall flask-request-gaurd.

```bash
pip install flask-guard
```

## Create the keys


```python
from FlaskGuard import RequestParameter

# Creates a key that has the name "name" and type str with a minimum length of 0 and 
# a maximum length of 10
name_key =  RequestParameter("name", str, 0, 10)

# Creates a key that has the name "range" and type int with a minimum value of -10 and
#  a maximum value of 10
range_key = RequestParameter("range", int, -10, 10)

```

## Create the validation function

```python
from FlaskGuard import  FlaskGuard

# Init FlaskRequestGuard
guard = FlaskRequestGuard("myapp")

# Keys from the code snippet above
required_keys = [range_key, name_key] 

# Returns a function that is used to check a request
validate_user_request = guard.create_validate_function(required_keys)

```

## Check request

```python
request = {"name": "erik", "age": 23, "range": 2}
# Returns (True, {"error_messages": []}) 
is_valid, error_messages = validate_user_request(request)

request = {"name": "eeeeeeeeeee", "age": 23, "range": 2}
# Returns (False, {"error_messages": ["The 'name' field must be 10 size or less,
#  and at least 0 size or more, but is actually 11 characters long."]})
is_valid, error_messages = validate_user_request(request)


request = {"age": 23, "range": 2}
# Returns False, {"error_messages": ["Missing name field in request body."]}
is_valid, error_messages = validate_user_request(request)

```

For an example where it's used with Flask, check out FlaskGuard-example [repo](https://github.com/beki1337/flaskguard-example).



## Run tests

Run this commad in FlaskGuard directory to run the tests

```bash
python -m unittest discover tests
```


## Contributing

Pull requests are welcome. For major changes, please open an issue first
to discuss what you would like to change.

Please make sure to update tests as appropriate.

## License

[MIT](https://choosealicense.com/licenses/mit/)

