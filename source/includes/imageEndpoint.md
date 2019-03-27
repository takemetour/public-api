
# Image Endpoint

## Development and Production Image Endpoint

We also provide 2 image endpoints using in seperated environment.

If you are developing (or testing) please use development endpoint.

Environment | Endpoint
---------  | -----------
Development | [https://dja3e86j343dh.cloudfront.net/](https://dja3e86j343dh.cloudfront.net/)
Production | [https://dglw4xbnd0ycq.cloudfront.net/](https://dglw4xbnd0ycq.cloudfront.net/)

In several APIs, you'll see `avatar_image`, `images`, `cover_image` fields contain a string that looks like path
eg. `/trips/1CTXi-1426778450712908.jpg`, `users/rtitM-14267784330583837.jpg` 

To access the image, just concat image endpoint with image path. For example, avatar_image is `users/rtitM-14267784330583837.jpg` and you're in development
so completed path will be [https://dja3e86j343dh.cloudfront.net/users/rtitM-14267784330583837.jpg](https://dja3e86j343dh.cloudfront.net/users/rtitM-14267784330583837.jpg)
