#!/bin/bash

# カラー定義
GREEN='\033[0;32m'
RED='\033[0;31m'
NC='\033[0m'

# 管理者権限チェック
if [ "$EUID" -ne 0 ]; then
    echo -e "${RED}エラー: sudo sh setup.sh として実行してください。${NC}"
    exit 1
fi

echo -e "${GREEN}==========================================${NC}"
echo -e "${GREEN}   Pterodactyl ツールセット インストーラー   ${NC}"
echo -e "${GREEN}==========================================${NC}"

# 1. 共通ライブラリの配置
echo "工程 1/3: 共通ライブラリを配置中..."
if [ -f "pt-lib" ]; then
    cp pt-lib /usr/local/bin/
    chmod +x /usr/local/bin/pt-lib
else
    echo -e "${RED}エラー: pt-lib が見つかりません。${NC}"
    exit 1
fi

# 2. 各コマンドの配置
echo "工程 2/3: 各コマンドを配置中..."
# pterodactyl- で始まるファイルをすべてコピー
cp pterodactyl-* /usr/local/bin/ 2>/dev/null

# 3. 実行権限の一括付与
echo "工程 3/3: 実行権限を付与中..."
chmod +x /usr/local/bin/pterodactyl-*

echo -e "\n${GREEN}✔ すべてのセットアップが完了しました！${NC}"
echo -e "以下のコマンドが使用可能です："
ls /usr/local/bin/pterodactyl-* | xargs -n 1 basename
echo -e "------------------------------------------"
