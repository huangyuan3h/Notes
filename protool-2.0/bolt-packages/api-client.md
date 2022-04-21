# API client

### GOT

We used to send request by `request` ([https://github.com/request/request](https://github.com/request/request)) before it was deprecated in 2020.

Currently, `got` was chose as the packages to send  request to microservice.

[https://github.com/sindresorhus/got](https://github.com/sindresorhus/got)



![](<../../.gitbook/assets/image (8).png>)



From the comparison table, they choose not support the `browser` to avoid unnecessary code, which means it is small. Plus, most of the function is supported. For me, it is a reasonable choice.



### Microservice

In current Backend structure, it is much more about the spring cloud, docker and Restful api.

This is the folder structure of api layer, each folder is a `got client`  mapping to the target microservice:

![](<../../.gitbook/assets/image (4).png>)



The reason to abstract it into sub-modules is that the logic to call backend should keep the same logic. So that when backend changed, the all the frontend project relay on the api could be updated and keep the same styles (if not using graphql server)

### Testing

For integration testing, I would recommend `nock` to mock the http request.

{% embed url="https://github.com/nock/nock" %}

For the UT for this layer, jest mock is enough.
