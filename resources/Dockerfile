FROM python:3 as vscode

RUN apt-get update && \
    apt-get install -y \
		  libunwind8 libxkbfile1 libsecret-1-0 libnotify4 \
      libgconf-2-4 libnss3 libgtk2.0-0 libxss1 libgconf-2-4 libasound2 libxtst6 \
      libcanberra-gtk-dev libgl1-mesa-glx libgl1-mesa-dri \
      midori xdg-utils \
			rsync

# Download and install VSCode
RUN wget https://go.microsoft.com/fwlink/?LinkID=760868 -O vscode.deb && \
    dpkg -i vscode.deb; \
    apt-get -f install -y && \
    rm vscode.deb && \
    rm -rf /var/lib/apt/lists/*

# Setup extensions folder
VOLUME /extensions

# create vscode user
RUN useradd -m vscode -s /bin/bash
WORKDIR /src
RUN mkdir -p /extensions && \
    chown vscode /extensions

USER vscode

# Install Python linter
RUN python -m pip install -U pylint --user

# Install Python plugin
RUN code --extensions-dir /extensions --install-extension ms-python.python

# Environment variables
ENV DISPLAY=:0.0
ENV VS_OPTIONS=""

CMD [ "/bin/bash", "-c",  "code ${VS_OPTIONS} --verbose --disable-gpu --extensions-dir /extensions -n ." ]
