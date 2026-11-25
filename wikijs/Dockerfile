FROM node:18-bookworm-slim

# Outils : wget (étape 1) et de quoi compiler sqlite3 (étape 5)
RUN apt-get update && apt-get install -y --no-install-recommends \
    wget ca-certificates python3 make g++ \
    && rm -rf /var/lib/apt/lists/*

# Étape 1 : télécharger Wiki.js
RUN wget https://github.com/Requarks/wiki-v2/releases/latest/download/wiki-js.tar.gz

# Étape 2 : extraire dans le dossier wiki, puis cd ./wiki
RUN mkdir wiki && tar xzf wiki-js.tar.gz -C ./wiki
WORKDIR /wiki

# Étape 3 : renommer le fichier de config
RUN mv config.sample.yml config.yml

# Étape 4 : "nano config.yml" est impossible dans un build,
# donc on fournit notre config.yml déjà édité, qui remplace celui-ci
COPY config.yml /wiki/config.yml

# Étape 5 : SQLite uniquement
RUN npm rebuild sqlite3

EXPOSE 3000

# Étape 6 : lancer Wiki.js
CMD ["node", "server"]
