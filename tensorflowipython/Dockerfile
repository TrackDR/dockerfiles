FROM b.gcr.io/tensorflow/tensorflow

WORKDIR /notebooks
RUN apt-get update
RUN apt-get install -y --force-yes git ipython ipython-notebook
RUN git clone https://github.com/TrackDR/tensorflow

EXPOSE 8888

# You can mount your own SSL certs as necessary here
ENV PEM_FILE /mycert.pem
# $PASSWORD will get `unset` within notebook.sh, turned into an IPython style hash
ENV PASSWORD Dont make this your default
ENV USE_HTTP 0

ADD notebook.sh /
RUN chmod u+x /notebook.sh

CMD ["/notebook.sh"]
