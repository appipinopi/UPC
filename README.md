Ubuntu-Pterodactyl-Command
v1.0.0
Ubuntu環境におけるPterodactyl Panelの運用を効率化するためのシェルスクリプト集です。共通ライブラリ（pt-lib）による進捗表示機能を備えています。
📋 収録コマンド一覧
| コマンド | 工程数 | 役割 |
|---|---|---|
| pterodactyl-cm-up | 4 | [重要] GitHubの最新リリースを確認し、本ツールを自動アップデート |
| pterodactyl-backup | 2 | 現行ファイルを /var/www/pterodactyl_backup へ保存 |
| pterodactyl-restore | 3 | バックアップから復元し、権限修復とキャッシュクリアを実行 |
| pterodactyl-fix | 2 | 所有権（www-data）とファイル/ディレクトリ権限の修復 |
| pterodactyl-logs | 1 | 本日のLaravelログをリアルタイム監視（tail -f） |
🚀 インストール方法
1. リポジトリのクローン
ターミナルを開き、リポジトリをローカルにダウンロードします。
git clone https://github.com/appipinopi/UPC.git
cd UPC

2. ワンクリック・セットアップ
付属の setup.sh を実行します。このスクリプトは、すべてのコマンドを /usr/local/bin/ へコピーし、実行権限を一括で付与します。
sudo sh setup.sh

3. 手動インストール（詳細手順）
自動スクリプトを使用せず、手動でセットアップを行う場合は以下の操作を行ってください。拡張子なしで配置することで、システムコマンドとして呼び出せるようになります。
 * 共通ライブラリの配置
   sudo cp pt-lib /usr/local/bin/pt-lib
sudo chmod +x /usr/local/bin/pt-lib

 * 各コマンドの配置と権限付与
   sudo cp pterodactyl-cm-up /usr/local/bin/pterodactyl-cm-up
sudo cp pterodactyl-backup /usr/local/bin/pterodactyl-backup
sudo cp pterodactyl-restore /usr/local/bin/pterodactyl-restore
sudo cp pterodactyl-fix /usr/local/bin/pterodactyl-fix
sudo cp pterodactyl-logs /usr/local/bin/pterodactyl-logs

sudo chmod +x /usr/local/bin/pterodactyl-*

📖 使い方
セットアップ完了後、任意のディレクトリから以下のコマンドを実行可能です。
# 本ツールのアップデート確認と実行
sudo pterodactyl-cm-up

# パネルデータのバックアップ
sudo pterodactyl-backup

# バックアップからの復元（※現在の /var/www/pterodactyl/* は削除されます）
sudo pterodactyl-restore

# パーミッションおよび所有権の修復
sudo pterodactyl-fix

# リアルタイムログ監視（Ctrl+C で終了）
pterodactyl-logs

➕ 新規コマンドの追加方法（テンプレート）
新しい機能を追加する際は、以下の構造に従って作成し /usr/local/bin/ に配置してください。
#!/bin/bash
source /usr/local/bin/pt-lib
check_sudo

echo -e "${GREEN}=== [新コマンド名] ===${NC}"
echo -e "${BLUE}全 [N] 工程を開始します...${NC}\n"

# 工程1
show_progress 1 [N] "処理内容の説明"
# 実行コマンドをここに記述

# 工程2
show_progress 2 [N] "次の処理説明"
# 実行コマンドをここに記述

echo -e "\n\n${GREEN}✔ [完了] すべての工程が終了しました。${NC}"

⚠️ 注意事項
 * OS環境: Ubuntu + Nginx (User: www-data) 環境を前提としています。
 * 権限: pterodactyl-logs 以外のコマンド実行には sudo 権限が必要です。
 * データ管理: pterodactyl-restore 実行時は既存データが上書き削除されるため、事前にバックアップの整合性を確認してください。
Version: 1.0.0
Repository: https://github.com/appipinopi/UPC
