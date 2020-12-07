FROM python:3.8

COPY . /opt/app
WORKDIR /opt/app

RUN pip3 install -r requirements.txt
RUN mkdir ~/.streamlit
RUN cp config.toml ~/.streamlit/config.toml
RUN cp credentials.toml ~/.streamlit/credentials.toml

EXPOSE 80
USER root

ENTRYPOINT ["streamlit", "run"]
CMD ["main/demo.py"]