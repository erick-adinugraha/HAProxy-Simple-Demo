# HAProxy Demo

## Build nginx blue and nginx green as backend
For nginx blue
```bash
cd nginx-blue
docker build -t nginx:blue .
docker run --name nginx-blue -d --rm -p 22001:80 nginx:blue
```
For nginx green
```bash
cd nginx-green
docker build -t nginx:green .
docker run --name nginx-green -d --rm -p 22002:80 nginx:green
```

## Edit haproxy.cfg
Edit haproxy.cfg regarding IP address of the backend accordingly
Get the private IP of your maching by using command
```bash
ifconfig | grep inet
```

## Build and run the HAProxy
```bash
docker build -t my-haproxy .
docker run --name my-haproxy -d --rm -p 22000:80 my-haproxy
```

## Access the site
The site can be access at http://localhost:22000 

## Clean up
```bash
docker stop nginx-green && \
docker stop nginx-blue && \
docker stop my-haproxy
```