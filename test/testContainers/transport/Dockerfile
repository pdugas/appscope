FROM cribl/cribl:latest

RUN apt update && apt install -y \
  curl \
&& rm -rf /var/lib/apt/lists/*

ENV CRIBL_NOAUTH=1
COPY transport/cribl/ /opt/cribl/local/cribl/

RUN mkdir -p /opt/test/bin
COPY transport/scope-test /opt/test/bin

ENV PATH="/usr/local/scope:/usr/local/scope/bin:${PATH}"
COPY scope-profile.sh /etc/profile.d/scope.sh
COPY gdbinit /root/.gdbinit

RUN  mkdir /usr/local/scope && \
     mkdir /usr/local/scope/bin && \
     mkdir /usr/local/scope/lib && \
     ln -s /opt/appscope/bin/linux/scope /usr/local/scope/bin/scope && \
     ln -s /opt/appscope/bin/linux/ldscope /usr/local/scope/bin/ldscope && \
     ln -s /opt/appscope/lib/linux/libscope.so /usr/local/scope/lib/libscope.so

COPY transport/scope-test /usr/local/scope/

COPY docker-entrypoint.sh /
ENTRYPOINT ["/docker-entrypoint.sh"]
CMD ["test"]
