FROM alpine:3.21

RUN apk add --no-cache bash

ADD src/wait-for-it.sh /wait-for-it.sh
RUN chmod +x /wait-for-it.sh
ENTRYPOINT ["/wait-for-it.sh"]
