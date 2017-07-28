FROM centos


ADD jdk-8u141-linux-x64.gz /usr/local
ADD hadoop-2.7.3.tar_2.gz /usr/local
ADD Python-3.6.2.tar.xz.gz /usr/local

ENV JAVA_HOME /usr/local/jdk1.8.0_141
ENV CLASSPATH $JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar

ENV HADOOP_HOME /usr/local/hadoop-2.7.3
ENV PYTHON_HOME /usr/local/Python-3.6.2

ENV PATH $JAVA_HOME/bin:$HADOOP_HOME/bin:$PATH

# 安装openssh-server和sudo软件包，并且将sshd的UsePAM参数设置成no  
RUN yum install -y openssh-server sudo  
RUN sed -i 's/UsePAM yes/UsePAM no/g' /etc/ssh/sshd_config  
#安装openssh-clients
RUN yum  install -y openssh-clients

# 添加测试用户root，密码root，并且将此用户添加到sudoers里  
RUN echo "hadoop:hadoop" | chpasswd  
RUN echo "hadoop   ALL=(ALL)       ALL" >> /etc/sudoers  
# 下面这两句比较特殊，在centos6上必须要有，否则创建出来的容器sshd不能登录  
RUN ssh-keygen -t dsa -f /etc/ssh/ssh_host_dsa_key  
RUN ssh-keygen -t rsa -f /etc/ssh/ssh_host_rsa_key  

# 启动sshd服务并且暴露22端口  
RUN mkdir /var/run/sshd  
EXPOSE 22  
CMD ["/usr/sbin/sshd", "-D"]