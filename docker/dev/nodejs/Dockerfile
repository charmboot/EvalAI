FROM node:14.20.0

# install chrome for protractor tests

# RUN wget http://www.linuxidc.com/files/repo/google-chrome.list -P /etc/apt/sources.list.d/
# RUN wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add -
# RUN apt-get update && apt-get install -yq google-chrome-stable
RUN sed -i 's#http://deb.debian.org#https://mirrors.163.com#g' /etc/apt/sources.list
RUN apt-get update && apt-get install -y libxss1 libappindicator1 libindicator7
RUN git config --global url."https://".insteadOf git://
# RUN wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
# RUN dpkg -i google-chrome-stable_current_amd64.deb
# RUN apt-get -f install
WORKDIR /code

# Add dependencies
ADD ./package.json /code
ADD ./bower.json /code
ADD ./gulpfile.js /code
ADD ./.eslintrc /code
ADD ./karma.conf.js /code

# Install Prerequisites
RUN npm config set registry https://registry.npm.taobao.org
RUN npm install -g bower gulp

RUN npm link gulp

RUN npm cache clean -f
RUN npm install
RUN npm install -g karma-cli
RUN npm install -g qs
RUN bower install --allow-root
RUN apt-get install -y libxss1

CMD ["gulp", "dev:runserver"]

EXPOSE 8888
