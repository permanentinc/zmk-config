docker volume create --driver local -o o=bind -o type=none -o device="/Users/jd/Sites/zmk-config/config/" zmk-config

docker volume create --driver local -o o=bind -o type=none -o device="/Users/jd/Sites/zmk-config/modules/" zmk-modules


devcontainer up --workspace-folder "/Users/jd/Sites/zmk"
docker exec -w /workspaces/zmk -it 89ce55cf07a9 /bin/bash
cd app/


