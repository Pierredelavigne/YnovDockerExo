FROM nginx

RUN apt update && apt install -y git
RUN rm -rf /usr/share/nginx/html/*
RUN git clone https://github.com/withaarzoo/3D-Rotate-Tube /usr/share/nginx/html

CMD ["nginx","-g","daemon off;"]
