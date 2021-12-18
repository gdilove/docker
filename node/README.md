# Nvm 0.39 and node 12

If you want to install node 14 or 16 by default, please change 12 to 14 or 16 on line 41 in Dockerfile

# install node 12
RUN /bin/bash -c "source /root/.bashrc;nvm install 12"