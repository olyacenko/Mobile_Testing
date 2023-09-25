## Charles HW Traffic capture
## Ex_0:
-----
Focus on the following requests:

```
Protocol: http
IP: 162.55.220.72
Port: 5006
```
## Ex_1:
----

```
Method: GET
EndPoint: /get_method
request url params: 
 name: str
 age: int
```
response: 
```
[
    “Str”,
    “Str”
]
```
### Task: 
Substitute the url in Charles so that the name you put in Postman goes away in the request and the name you put in Charles is returned.
Do it in both Rewrite and BreakPoint

### Solution
#### BreakPoints
Use this URL in Charles Breakpoints settings `http://162.55.220.72:5006/get_method?name=Olya&age=29` ;

Send the request in Postman ;

In `BreakPoints` change request text in `Edit Request` from `Olya` to `Alias` .

You can also sniff the Response. Go to `Edit Response` and change the name.



#### Rewrite
In Charles Rewrite settings use location `http://162.55.220.72:5006/get_method?name=Olya&age=29` ;

In Rewrite Rule select `Type: Modify Query Param` => `Match: Name: name, Value: Olya` => `Replace: Name: name, Value: Alias` ;

Send the request in Postman ;

## Ex_2:
-----

```
Method: POST
EndPoint: /user_info_3
request form data: 
 name: str
 age: int
 salary: int
```

response: 
```
{
'name': name,
'age': age,
'salary': salary,
'family': {
            'children': [
                         ['Alex', 24],
                         ['Kate', 12]
                        ],
            'u_salary_1_5_year': salary * 4
          }
}
```
### Task: 
Substitute body in Charles so that in the query the salary you entered in Postman goes away, and in u_salary_1_5_year the number returned is less than the original one from the query.
Do it in both Rewrite and BreakPoint.
### Solution
#### BreakPoints
Use this URL in Charles Breakpoints settings `http://162.55.220.72:5006/user_info_3` ;

Send the request in Postman ;

In `BreakPoints` change response text in `Edit Response` from `"u_salary_1_5_year": 2000` to `"u_salary_1_5_year": 100` .

#### Rewrite
In Charles Rewrite settings use location `http://162.55.220.72:5006/user_info_3` ;

In Rewrite Rule select `Type: Body` => `Where: Response ` => `Match: Value: 2000` => `Replace: Value: 100` ;

Send the request in Postman ;

## Ex_3:
-----

```
Method: GET
EndPoint: /object_info_1
request url params: 
 name: str
 age: int
 weight: int
```
response: 
```
{'name': name,
 'age': age,
 'daily_food': weight * 0.012,
 'daily_sleep': weight * 2.5
}
```

### Task: 
Substitute query parameters in Charles so that Postman receives a response with an another name, daily_food > weight from the query, and daily_sleep < weight from the query. Do it in both Rewrite and BreakPoint.
### Solution
#### BreakPoints
Use this URL in Charles Breakpoints settings `http://162.55.220.72:5006/object_info_1?name=Olya&age=29&weight=63` ;

Send the request in Postman ;

In `BreakPoints` change response text in `Edit response`:

`name` from `Olya` to `Alias` , 

`daily_food` from `0.756` to `157.5` , 

`daily_sleep` from `157.5` to `0.756` .
#### Rewrite
In Charles Rewrite settings use location `http://162.55.220.72:5006/object_info_1?name=Olya&age=29&weight=63` ;

In Rewrite Rule select `Type: Body` => `Where: Response ` =>

1) `Match: Value: Olya` => `Replace: Value: Alias` ,
2) `Match: Value: "daily_food": 0.756` => `Replace: Value: "daily_food": 157.5` ,
3) `Match: Value: "daily_sleep": 157.5` => `Replace: Value: "daily_sleep": 0.756` ;

Send the request in Postman ;

## Ex_4:
-----
```
Method: GET
EndPoint: /object_info_3
request url params: 
 name: str
 age: int
 salary: int
```
response: 

```
{
'name': name,
 'age': age,
 'salary': salary,
 'family': {
            'children': [
                         ['Alex', 24],
                         ['Kate', 12]
                        ],
             'pets': { 'cat':{'name':'Sunny',
                               'age': 3},
                       'dog':{'name':'Luky',
                              'age': 4}
                     },
            'u_salary_1_5_year': salary * 4
           }
}
```
### Task: 
Do it in both Rewrite and BreakPoint.
- Use Charles to make the server return a 500 code.
- Use Charles to make the server return a 405 code.
### Solution
#### BreakPoints
Use this URL in Charles Breakpoints settings `http://162.55.220.72:5006/object_info_3?name=Olya&age=29&salary=500` ;

Send the request in Postman ;

In `BreakPoints` change response Headers in `Edit response` from `200` to `500`, than from `200` to `405`.

#### Rewrite
In Charles Rewrite settings use location `http://162.55.220.72:5006/object_info_3?name=Olya&age=29&salary=500` ;

In Rewrite Rule select `Type: Response status` => `Match: Value: 200 OK` => `Replace: Value: 500 OK` / `Replace: Value: 405 OK` ,


Send the request in Postman ;

## Ex_5:
----
```
Method: GET
EndPoint: /object_info_4
request url params: 
 name: str
 age: int
 salary: int
```
response: 

```
{
 'name': name,
 'age': int(age),
 'salary': [salary, str(salary * 2), str(salary * 3)]
}
```
### Task: 
Do it in both Rewrite and BreakPoint.

1) Use Charles to make the server return a 405 code.
2) Substitute salary in request
3) Substitute (salary * 2) in response
 
### Solution
#### BreakPoints
Use this URL in Charles Breakpoints settings `http://162.55.220.72:5006/object_info_4?name=Olya&age=29&salary=500` ;

Send the request in Postman ;

1) Use Charles to make the server return a 405 code.
   
In `BreakPoints` change request URL in `Edit request` substitute METHOD from `GET` to `POST` ;

Or you can change response Headers in `Edit response` from `200` to `500`, than from `200` to `405`

2) Substitute salary in request

In `BreakPoints` change request URL in `Edit request` substitute `sarary` from `500` to `100` ;

3) Substitute (salary * 2) in response

In `BreakPoints` change response text in `Edit response` substitute `(salary * 2)` from `"1000"` to `3` ;


#### Rewrite
In Charles Rewrite settings use location `http://162.55.220.72:5006/object_info_4?name=Olya&age=29&salary=500` ;

   In Rewrite Rule select 
   
1) Use Charles to make the server return a 405 code.

 - `Type: Response status` => `Match: Value: 200 OK` => `Replace: Value: 405 OK` ,
   
2) Substitute salary in request

 - `Type: Modify query param` => `Match: name: salary ; Value: 500` => `Replace: name: salary ; Value: 100` ,

3) Substitute (salary * 2) in response

 - `Type: Body , Response` => `Match: Value: 200` - (salary * 2) => `Replace: Value: 3`


Send the request in Postman ;

## Ex_6:
-----
```
Method: POST
EndPoint: /user_info_2
request form data: 
 name: str
 age: int
 salary: int
```
response: 

```
{
 'start_qa_salary': salary,
 'qa_salary_after_6_months': salary * 2,
 'qa_salary_after_12_months': salary * 2.7,
 'qa_salary_after_1.5_year': salary * 3.3,
 'qa_salary_after_3.5_years': salary * 3.8,
 'person': {
            'u_name': [user_name, salary, age],
            'u_age': age,
            'u_salary_5_years': salary * 4.2
           }
}
```

### Task:
 Do it in both Rewrite and BreakPoint. 

 ⁃ Make Charles return a response to Postman in which qa_salary_after_1.5_year is renamed to qa_salary_after_1.5_month
 
 ⁃ Make qa_salary_after_3.5_years be less than qa_salary_after_12_months in the response

### Solution
#### BreakPoints
Use this URL in Charles Breakpoints settings `http://162.55.220.72:5006/user_info_2` ;

Send the request in Postman ;

In `BreakPoints` change response text in `Edit response` from `qa_salary_after_1.5_year` to `qa_salary_after_1.5_month` than substitute from `"qa_salary_after_3.5_years": 1900.0` to `"qa_salary_after_3.5_years": 100`



#### Rewrite
In Charles Rewrite settings use location `http://162.55.220.72:5006/user_info_2` ;

In Rewrite Rule select `Type: Body , Response` => 

1. `Match: Value: qa_salary_after_1.5_year` => `Replace: Value: qa_salary_after_1.5_month`  ,

2. `Match: Value: "qa_salary_after_3.5_years": 1900.0 ` => `Replace: Value: "qa_salary_after_3.5_years": 100`
   
Send the request in Postman ;






















