
FROM maven:3.3.3
#替换仓库为aliyun
COPY settings.xml /usr/share/maven/conf/

ENV CATALINA_HOME /usr/local/tomcat
ENV PATH $CATALINA_HOME/bin:$PATH
RUN mkdir -p "$CATALINA_HOME"
WORKDIR $CATALINA_HOME

COPY apache-tomcat-8.0.42.tar.gz /usr/local/tomcat/
COPY apache-tomcat-8.0.42.tar.gz.asc /usr/local/tomcat/
RUN pwd && ls
	
#用于脚本调试。set是把它下面的命令打印到屏幕set -x 是开启 set +x是关闭 set -o是查看 #(xtrace)，set去追中一段代码的显示情况。执行set -x后，对整个脚本有效。
RUN set -x
RUN pwd && ls
RUN tar -xvf apache-tomcat-8.0.42.tar.gz --strip-components=1
RUN rm bin/*.bat
RUN rm apache-tomcat-8.0.42.tar.gz*



EXPOSE 8080
CMD ["catalina.sh", "run"]  