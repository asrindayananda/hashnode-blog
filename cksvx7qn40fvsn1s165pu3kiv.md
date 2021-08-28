## Blocked by CORS policy, No Access-control-allow-origin' error when creating AWS Lambda script

I setup a AWS Lambda service and connected my website to it via AWS API gateway but I got a CORS error. Below is steps on my fix.
```
CORS policy: No 'Access-Control-Allow-Origin' header is present on the requested resource.
```

```
getDataAjax.html:1 Access to XMLHttpRequest at 'https://<url>.amazonaws.com/my-function-apigateway' from origin 'null' has been blocked by CORS policy: No 'Access-Control-Allow-Origin' header is present on the requested resource.
``` 


![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1625038727522/ysc2J3BYj.png)
When calling your lambda request

Change your code in your lambda to add allow origin of where your ajax request is coming from

eg.
```
 "Access-Control-Allow-Origin": "https://www.azcodez.com",
```

```
exports.handler = async (event) => {
    const response = {
        statusCode: 200,
        headers: {
            "Access-Control-Allow-Headers" : "Content-Type",
            "Access-Control-Allow-Origin": "https://www.azcodez.com",
            "Access-Control-Allow-Methods": "OPTIONS,POST,GET"
        },
        body: JSON.stringify('Hello from Lambda!!'),
    };
    return response;
};
``` 

- Multiple domains are quite tricky to add so forward your domain to domain you want to use using Route 53. I couldn't create a lambda fix for this. Let me know if you did :)

    - Add a CNAME 
        - www.azcodez.com to azcodez.com
Or
    - Forward www.azcode.com to azcodez.com resource


References
- https://docs.aws.amazon.com/apigateway/latest/developerguide/how-to-cors.html

Hope this solution worked for you! If this didn't please comment and I will try to assist.

Happy Coding,
Asrin

If this helped you consider buying me a coffee :)

%%[buymecoffee]
