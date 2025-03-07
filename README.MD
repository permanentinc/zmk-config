docker volume create --driver local -o o=bind -o type=none -o device="/Users/jd/Sites/zmk-config/config/" zmk-config

docker volume create --driver local -o o=bind -o type=none -o device="/Users/jd/Sites/zmk-config/modules/" zmk-modules


devcontainer up --workspace-folder "/Users/jd/Sites/zmk"
docker exec -w /workspaces/zmk -it 89ce55cf07a9 /bin/bash
cd app/


west build --pristine -d build/left --board "nice_nano_v2" -- -DSHIELD="corne_left;nice_oled" -DZMK_CONFIG="/workspaces/zmk-config/config/"  -DZMK_EXTRA_MODULES="/workspaces/zmk-config/zmk-nice-oled"
west build --pristine -d build/right --board "nice_nano_v2" -- -DSHIELD="corne_right;nice_oled" -DZMK_CONFIG="/workspaces/zmk-config/config/"  -DZMK_EXTRA_MODULES="/workspaces/zmk-config/zmk-nice-oled"


cp /workspaces/zmk/app/build/left/zephyr/zmk.uf2 /tmp/left_zmk.uf2
cp /workspaces/zmk/app/build/right/zephyr/zmk.uf2 /tmp/right_zmk.uf2

docker cp 89ce55cf07a9:/tmp/left_zmk.uf2 /Users/jd/Sites/zmk-config/build
docker cp 89ce55cf07a9:/tmp/right_zmk.uf2 /Users/jd/Sites/zmk-config/build