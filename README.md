
// в самом начале 
 git submodule update --init --recursive


cd path/to/submodule

# Обновить подмодуль до последнего коммита
# Обновить информацию о подмодулях
git fetch
# Переключиться на основную ветку
git checkout main
# Обновить основную ветку
git pull origin main
# Обновить подмодули до последнего коммита в их репозиториях
git submodule update --remote