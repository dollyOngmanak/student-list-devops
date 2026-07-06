FROM python:3.9-slim
LABEL maintainer="dollyongmanak@gmail.com"
RUN apt update -y && apt install -y gcc build-essential python3-dev libsasl2-dev libldap2-dev libssl-dev
COPY requirements.txt /
RUN pip3 install --upgrade pip
RUN pip3 install -r /requirements.txt
COPY student_age.py /
RUN mkdir -p /data
VOLUME [ "/data" ]
EXPOSE 5000
CMD [ "python3", "/student_age.py" ]
