FROM ubuntu:14.04
MAINTAINER me

RUN sudo apt-get update -qq && sudo apt-get install -y --force-yes \
    git \
    default-jdk \
    maven \
    gradle \
    wget \
    sox \
    
    
WORKDIR /usr/local/src
RUN git clone https://github.com/cmusphinx/sphinx4
WORKDIR /usr/local/src/sphinx4/sphinx4-core
RUN gradle build

# https://github.com/JoshData/cmusphinx-alignment-example
WORKDIR /home/ubuntu
RUN git clone https://github.com/JoshData/cmusphinx-alignment-example
WORKDIR /home/ubuntu/cmusphinx-alignment-example
RUN wget http://downloads.sourceforge.net/project/cmusphinx/Acoustic%20and%20Language%20Models/US%20English%20Generic%20Acoustic%20Model/cmusphinx-en-us-5.2.tar.gz
RUN tar -zxf cmusphinx-en-us-5.2.tar.gz

WORKDIR /home/ubuntu/cmusphinx-alignment-example
RUN wget -O sample_original.wav https://web.archive.org/web/20070704072132/http://www.hawksoft.com/hawkvoice/samples/ulaw.wav
RUN sox sample_original.wav -b 16 sample.wav channels 1 rate 16k
RUN echo "It's a dense crowd in two distinct ways. The fruit of a figg tree is apple shaped." > sample.txt
RUN java -cp /usr/local/src/sphinx4/sphinx4-core/target/sphinx4-core-1.0-SNAPSHOT.jar edu.cmu.sphinx.tools.aligner.Aligner cmusphinx-en-us-5.2/ sphinx4-5prealpha-src/sphinx4-data/src/main/resources/edu/cmu/sphinx/models/en-us/cmudict-en-us.dict sample.wav "$(cat sample.txt)"

RUN wget http://downloads.sourceforge.net/project/opencsv/opencsv/3.7/opencsv-3.7.jar
RUN javac -cp /usr/local/src/sphinx4/sphinx4-core/target/sphinx4-core-1.0-SNAPSHOT.jar:opencsv-3.3.jar Aligner.java 

