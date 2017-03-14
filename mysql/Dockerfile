FROM ubuntu:14.04
MAINTAINER df007df

RUN cp /etc/apt/sources.list /etc/apt/sources.list.backup
ADD sources.list /etc/apt/sources.list

RUN apt-get -y update && apt-get -y install mysql-server
RUN /etc/init.d/mysql start \
    && mysql -uroot -e "grant all privileges on *.* to 'root'@'%' identified by '123456';" \
    && mysql -uroot -e "grant all privileges on *.* to 'root'@'localhost' identified by '123456';"

RUN sed -Ei 's/^(bind-address|log)/#&/' /etc/mysql/my.cnf \
    && echo 'skip-host-cache\nskip-name-resolve' | awk '{ print } $1 == "[mysqld]" && c == 0 { c = 1; system("cat") }' /etc/mysql/my.cnf > /tmp/my.cnf \
    && mv /tmp/my.cnf /etc/mysql/my.cnf

EXPOSE 3306

ENTRYPOINT ["/etc/init.d/mysql", "start"]

#CMD ["top"]
