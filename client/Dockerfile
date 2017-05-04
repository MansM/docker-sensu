FROM centos:7

ENV container docker
RUN (cd /lib/systemd/system/sysinit.target.wants/; for i in *; do [ $i == \
    systemd-tmpfiles-setup.service ] || rm -f $i; done); \
    rm -f /lib/systemd/system/multi-user.target.wants/*;\
    rm -f /etc/systemd/system/*.wants/*;\
    rm -f /lib/systemd/system/local-fs.target.wants/*; \
    rm -f /lib/systemd/system/sockets.target.wants/*udev*; \
    rm -f /lib/systemd/system/sockets.target.wants/*initctl*; \
    rm -f /lib/systemd/system/basic.target.wants/*;\
    rm -f /lib/systemd/system/anaconda.target.wants/*;


RUN yum install -y epel-release && yum-config-manager --add-repo=https://sensu.global.ssl.fastly.net/yum/7/x86_64 --nogpgcheck && \
    echo "gpgcheck=0" >> /etc/yum.repos.d/sensu.global.ssl.fastly.net_yum_7_x86_64.repo && \
    yum install -y sensu && \
    yum clean all 

RUN systemctl enable sensu-client

COPY client.json /etc/sensu/conf.d/client.json
COPY transport.json /etc/sensu/conf.d/transport.json
COPY redis.json /etc/sensu/conf.d/redis.json

RUN yum install -y httpd && systemctl enable httpd && yum clean all
RUN sensu-install -P apache,process-checks,load-checks

RUN rm -f /etc/httpd/conf.d/welcome.conf

COPY default.conf /etc/httpd/conf.d/default.conf

VOLUME [ "/sys/fs/cgroup" ]
CMD ["/usr/sbin/init"]