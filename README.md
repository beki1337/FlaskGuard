# FlaskRequestGaurd

Flask Request Guard is a Python library for validating incoming HTTP requests in Flask web applications. It provides a simple yet flexible way to define request rules and enforce them automatically on incoming requests, ensuring that only requests that meet the specified requirements are allowed to proceed. 


## Installation
Use the package manager [pip](https://pip.pypa.io/en/stable/) to intall flask-request-gaurd.

```bash
pip install flask-request-gaurd
```

## Creat the keys


```python
from FlaskRequestGaurd import RequestParameter

# creats a key that has the name "name" and type str with min 0 and max 10 length
name_key =  RequestParameter("name",str,0,10)

#creats a key that has the name "range" and type int with min -10 and max 10 value
range_key = RequestParameter("range",int,-10,10)

```

## Create vaildate funcktion 

```python
from FlaskRequestGaurd import FlaskRequestGaurd

#Init FlaskRequestGaurd
gaurd = FlaskRequestGaurd("myapp")

reqeuerd_keys = [range_key,name_key] 

#Returns a funcktion that is used for check a request
vaildet_user_request = gaurd.creat_validate_funcktion(reqeuerd_keys)

```

## Check request

```python
request = {"name":"erik","age":23,"range":2}
# returns True,{"error_messages":[]} 
isvaild,erros_messages =vaildet_user_request(request)

request = {"name":"eeeeeeeeeee","age":23,"range":2}
# returns False,{'error messages': ["The 'name' field must be 10 size or less, and at least 0 size or more,but is actually 11 characters long."]}
isvaild,erros_messages =vaildet_user_request(request)


request = {"age":23,"range":2}
# returns False,{'error messages': ["Missing name field in request body."]}
isvaild,erros_messages =vaildet_user_request(request)

```




## Contributing

Pull requests are welcome. For major changes, please open an issue first
to discuss what you would like to change.

Please make sure to update tests as appropriate.

## License

[MIT](https://choosealicense.com/licenses/mit/)

