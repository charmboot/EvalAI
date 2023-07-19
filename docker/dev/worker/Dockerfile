FROM evalai_django
RUN sed -i 's#http://deb.debian.org#https://mirrors.163.com#g' /etc/apt/sources.list
RUN apt-get update && \
  apt-get install --no-install-recommends -q -y default-jdk && \
  rm -rf /var/lib/apt/lists/*

RUN pip install -i https://pypi.tuna.tsinghua.edu.cn/simple/  -U cffi service_identity cython==0.29 numpy==1.14.5
RUN pip install -i https://pypi.tuna.tsinghua.edu.cn/simple/ -r worker.txt

ADD . /code

CMD ["./docker/wait-for-it.sh", "django:8000", "--", "python", "-m", "scripts.workers.submission_worker"]
