## Error response from daemon: Get https://registry-1.docker.io/v2/: net/http: request canceled while waiting for connection

While setting up my magento 2 docker containers on WSL2 i got this error message pulling images

```
Error response from daemon: Get https://registry-1.docker.io/v2/: net/http: request canceled while waiting for connection
```

- Open your windows hosts file
    - C:\Windows\System32\drivers\etc

- Comment out the registry generated by docker 
```
#some-ip-address  registry-1.docker.io
```

- This fixed my issue

Hope this works for you

Happy Coding,
Asrin

If this helped you consider buying me a coffee :)

%%[buymecoffee]

Reference
-  https://stackoverflow.com/questions/59360629/docker-windows-timeout