FROM node:14.20.0

# install chrome for protractor tests
# RUN wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add -
# RUN sh -c 'echo "deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google.list'
# RUN apt-get update && apt-get install -yq google-chrome-stable

WORKDIR /code

# Add dependencies
ADD ./package.json /code
ADD ./bower.json /code
ADD ./gulpfile.js /code
ADD ./.eslintrc /code
ADD ./karma.conf.js /code

# Install Prerequisites
RUN npm config set registry https://registry.npm.taobao.org
RUN npm config set sass_binary_site https://npm.taobao.org/mirrors/node-sass/
RUN npm set puppeteer_download_host https://npm.taobao.org/mirrors 
RUN npm set chromedriver_cdnurl https://npm.taobao.org/mirrors/chromedriver
RUN npm install -g bower gulp

RUN npm link gulp

RUN npm cache clean -f
RUN npm install
RUN npm install -g karma-cli
RUN npm install -g qs
RUN bower install --allow-root
RUN sed -i 's/deb.debian.org/mirrors.aliyun.com/g' /etc/apt/sources.list
RUN apt-get update
RUN apt-get install -y libxss1

CMD ["gulp", "dev:runserver"]

EXPOSE 8888
