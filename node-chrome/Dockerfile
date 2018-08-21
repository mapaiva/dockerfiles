# DESCRIPTION:  Image containing NodeJS + Google Chrome
# AUTHOR:       Matheus Paiva <matheus.a.paiva@gmail.com>
# COMMENTS:
#       Based on the amazing post of @tekkie at
#       https://tekkie.flashbit.net/devops/angular-e2e-tests-on-gitlab-ci. Many thanks for this 
#       awesome and helpful walkthrough.
# USAGE:
#       Run:
#       ```
#       docker run -it --name ci-environment mapaiva/node-chrome google-chrome --headless \
#         --disable-gpu --screenshot --no-sandbox
#       ```
FROM node:8

LABEL maintainer "Matheus Paiva <matheus.a.paiva@gmail.com>"

# Add Google Chrome to aptitude's (package manager) sources
RUN echo "deb http://dl.google.com/linux/chrome/deb/ stable main" | tee -a /etc/apt/sources.list

# Fetch Chrome's PGP keys for secure installation
RUN wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add -

# Update aptitude's package sources
RUN apt-get -qq update -y

# Install latest Chrome stable, Xvfb packages
RUN apt-get -qq install -y google-chrome-stable xvfb gtk2-engines-pixbuf xfonts-cyrillic xfonts-100dpi xfonts-75dpi xfonts-base xfonts-scalable imagemagick x11-apps default-jre
    
# Launch Xvfb
RUN Xvfb :0 -ac -screen 0 1024x768x24 &

# Export display for Chrome
RUN export DISPLAY=:99

CMD ["node"]
