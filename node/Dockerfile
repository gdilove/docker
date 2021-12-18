FROM debian:bullseye

################################Custom##########################################

# set timezone
ENV TZ=Asia/Shanghai
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

# install apt-transport-https ca-certificates
RUN  apt-get update \
  && apt-get install -y apt-transport-https ca-certificates

# https://mirrors.tuna.tsinghua.edu.cn/help/debian/
RUN mv /etc/apt/sources.list /etc/apt/sources.list.bak && \
  echo "deb https://mirrors.tuna.tsinghua.edu.cn/debian/ bullseye main contrib non-free" >> /etc/apt/sources.list  && \
  echo "# deb-src https://mirrors.tuna.tsinghua.edu.cn/debian/ bullseye main contrib non-free" >> /etc/apt/sources.list  && \
  echo "deb https://mirrors.tuna.tsinghua.edu.cn/debian/ bullseye-updates main contrib non-free" >> /etc/apt/sources.list  && \
  echo "# deb-src https://mirrors.tuna.tsinghua.edu.cn/debian/ bullseye-updates main contrib non-free" >> /etc/apt/sources.list  && \
  echo "deb https://mirrors.tuna.tsinghua.edu.cn/debian/ bullseye-backports main contrib non-free" >> /etc/apt/sources.list  && \
  echo "# deb-src https://mirrors.tuna.tsinghua.edu.cn/debian/ bullseye-backports main contrib non-free" >> /etc/apt/sources.list  && \
  echo "deb https://mirrors.tuna.tsinghua.edu.cn/debian-security bullseye-security main contrib non-free" >> /etc/apt/sources.list  && \
  echo "# deb-src https://mirrors.tuna.tsinghua.edu.cn/debian-security bullseye-security main contrib non-free" >> /etc/apt/sources.list

# install the git and other app we need
RUN apt-get update \
  && apt-get install -y git vim wget \
  && rm -rf /var/lib/apt/lists/*


# nvm config for ~/.bashrc, ~/.profile, or ~/.zshrc file
RUN { \
  echo 'export NVM_DIR="$HOME/.nvm"'; \
  echo '[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" # This loads nvm'; \
  echo '[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"  # This loads nvm bash_completion'; \
  } > /root/.bashrc

# copy nvm folder from host to container
COPY nvm/ root/.nvm/

# install node 12
RUN /bin/bash -c "source /root/.bashrc;nvm install 12"

# install lts, sass, sass-convert
# RUN /bin/bash -c "source /root/.bashrc"
# RUN /bin/bash -c "source /root/.bashrc;nvm install --lts"
# RUN /bin/bash -c "source /root/.bashrc;npm install -g sass"
# RUN /bin/bash -c "source /root/.bashrc;npm install apidoc -g"
# RUN /bin/bash -c "source /root/.bashrc;npm install -g sass-convert"

EXPOSE 80
EXPOSE 443


WORKDIR "/var/www/html"
# ADD start.sh /start.sh
# RUN set -eux; \
#         chmod 755 /start.sh
# CMD ["/start.sh"]
