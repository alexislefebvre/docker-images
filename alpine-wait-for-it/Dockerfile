FROM frolvlad/alpine-bash

ADD src/wait-for-it.sh /wait-for-it.sh
RUN chmod +x /wait-for-it.sh
ENTRYPOINT ["/wait-for-it.sh"]
