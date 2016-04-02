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
#RUN git revert aa4e1838f06eb032fd248601469b16ac95aeb08a
#RUN mvn clean install
RUN gradle build

# https://github.com/JoshData/cmusphinx-alignment-example
WORKDIR /home/ubuntu
RUN git clone https://github.com/JoshData/cmusphinx-alignment-example
WORKDIR /home/ubuntu/cmusphinx-alignment-example
RUN wget http://downloads.sourceforge.net/project/cmusphinx/Acoustic%20and%20Language%20Models/US%20English%20Generic%20Acoustic%20Model/cmusphinx-en-us-5.2.tar.gz
RUN tar -zxf cmusphinx-en-us-5.2.tar.gz

# http://cmusphinx.sourceforge.net/2014/07/long-audio-aligner-landed-in-trunk/
WORKDIR /home/ubuntu/cmusphinx-alignment-example
RUN wget -O sample_original.wav https://web.archive.org/web/20070704072132/http://www.hawksoft.com/hawkvoice/samples/ulaw.wav
RUN sox sample_original.wav -b 16 sample.wav channels 1 rate 16k
RUN echo "It's a dense crowd in two distinct ways. The fruit of a figg tree is apple shaped." > sample.txt
RUN wget -O en_us_nostress.tar.gz http://sourceforge.net/projects/cmusphinx/files/G2P%20Models/en_us_nostress.tar.gz/download
#RUN java -cp /usr/local/src/sphinx4/sphinx4-core/build/sphinx4-core-5prealpha-SNAPSHOT.jar edu.cmu.sphinx.demo.aligner.AlignerDemo cmusphinx-en-us-5.2/ sphinx4-5prealpha-src/sphinx4-data/src/main/resources/edu/cmu/sphinx/models/en-us/cmudict-en-us.dict sample.wav sample.txt
RUN java -cp /usr/local/src/sphinx4/sphinx4-core/build/libs/sphinx4-core-5prealpha-SNAPSHOT.jar edu.cmu.sphinx.demo.aligner.AlignerDemo sample.wav sample.txt en-us-generic /usr/local/src/sphinx4/sphinx4-data/src/main/resources/edu/cmu/sphinx/models/en-us/cmudict-en-us.dict  /home/ubuntu/en_us_nostress/model.fst.ser


RUN wget http://downloads.sourceforge.net/project/opencsv/opencsv/3.7/opencsv-3.7.jar
RUN javac -cp /usr/local/src/sphinx4/sphinx4-core/target/sphinx4-core-1.0-SNAPSHOT.jar:opencsv-3.7.jar Aligner.java 

