# sd-workshop5
Loadbalancer.

I modify the HAProxy configuration file which is designed to route incoming HTTP requests to different backend services according to the path of the requested URL, and uses Consul for service name resolution.
![image](https://github.com/Sebastianavia/sd-workshop5/assets/71205906/32334a17-4a77-4d27-abd4-cbe982aab8cc)

I create the image: 
- docker build -t sebastiannavia/loadbalancer .


I  run the image: 
- docker run -d -p 9000:80 -p 1936:1936 --name loadbalancer sebastiannavia/loadbalancer
![image](https://github.com/Sebastianavia/sd-workshop5/assets/71205906/35431c10-6a5e-41ef-b4d4-6f9b2e279b5f)

![image](https://github.com/Sebastianavia/sd-workshop5/assets/71205906/bd8563ef-072c-434a-8812-9bace4c5e2b8)

Api gateway.

configure this file configures API management using an API gateway, defines API endpoints, associates those endpoints with backend services, and applies various policies and pipelines to manage security, logging, and other aspects of API traffic.

![image](https://github.com/Sebastianavia/sd-workshop5/assets/71205906/4abcbc9d-052b-406e-b839-7725e881afcd)

![image](https://github.com/Sebastianavia/sd-workshop5/assets/71205906/edebce10-e065-4e9e-b697-fb9a4ef21aa0)

After the configuration run the database that will use the gateway api, and then the api image.

- docker run --network distribuidos -d --rm --name express-gateway-data-storage -p 6379:6379 redis:alpine

- docker run -d --name express-gateway --network distribuidos -v $(pwd):/var/lib/eg -p 8080:8080 -p 9876:9876 express-gateway
- ![image](https://github.com/Sebastianavia/sd-workshop5/assets/71205906/d4b21084-a4a2-4349-af4a-2deb57254d08)

I create the user to perform the tests:

![image](https://github.com/Sebastianavia/sd-workshop5/assets/71205906/65564881-80f5-46e7-9492-9c5fabb879b9)

- curl -H "Authorization: apiKey 1(Key)" http://localhost:8080/pay

![image](https://github.com/Sebastianavia/sd-workshop5/assets/71205906/7e77a617-a5b3-4386-b285-72e07613663b)
![image](https://github.com/Sebastianavia/sd-workshop5/assets/71205906/de281665-399a-4b80-8ca7-6107307f94ff)
![image](https://github.com/Sebastianavia/sd-workshop5/assets/71205906/2ba9f995-6881-4198-ba29-11dc66d75e90)



