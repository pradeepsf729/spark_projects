FROM ubuntu

WORKDIR /spark_work

# Install OpenJDK-8
RUN apt-get update && \
    apt-get install -y openjdk-14-jdk && \
    apt-get install -y maven && \
    apt-get clean;

# Fix certificate issues
RUN apt-get update && \
    apt-get install ca-certificates-java && \
    apt-get clean && \
    update-ca-certificates -f;

# Setup JAVA_HOME -- useful for docker commandline
RUN echo "export JAVA_HOME=/usr/lib/jvm/java-14-openjdk-arm64/" >> ~/.bashrc
RUN echo "export PATH=$PATH:/usr/lib/jvm/java-14-openjdk-arm64/bin" >> ~/.bashrc

RUN apt-get install -y python3
RUN /usr/bin/ln -s /usr/bin/python3 /usr/bin/python

# download and install spark
RUN apt-get update && \
    apt-get install -y wget && \
    apt-get install -y supervisor && \
    apt-get install -y python3-pip && \
    apt-get install -y vim

RUN wget https://downloads.apache.org/spark/spark-3.1.2/spark-3.1.2-bin-hadoop3.2.tgz && \
    tar -xzf spark-3.1.2-bin-hadoop3.2.tgz && \
    mv spark-3.1.2-bin-hadoop3.2 /opt/spark && \
    rm -f spark-3.1.2-bin-hadoop3.2.tgz

RUN echo "export SPARK_HOME=/opt/spark" >> ~/.bashrc
RUN echo "export PATH=$PATH:/opt/spark/bin:/opt/spark/sbin" >> ~/.bashrc
RUN echo "export PYSPARK_PYTHON=/usr/bin/python3" >> ~/.bashrc

RUN pip3 install pyspark
RUN pip3 install jupyter

# portforwarding of the Spark UI port (localmode)
EXPOSE 4040

CMD ["/usr/local/bin/pyspark"]
