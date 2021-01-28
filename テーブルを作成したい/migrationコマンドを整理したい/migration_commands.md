## よく使うmigrationコマンド整理
1. 作成
```bash:crate
php artisan make:migration create_users_table
```
2. 実行
```bash:do
composer dump-autoload
php artisan migrate
```
3. ロールバック　最後
```bash:rollback
php artisan migrate:rollback
```
4. ロールバック　指定
```bash:rollback
php artisan migrate:rollback --step=5
```
5. 全部ロールバック
```bash:reset
php artisan migrate:reset
```
6. 全ロールバック＋migrate
```bash:refresh
php artisan migrate:refresh

# データベースをリフレッシュし、全データベースシードを実行
php artisan migrate:refresh --seed

# ステップも踏める
php artisan migrate:refresh --step=5
```
7. ロールバック失敗してぴえんなとき
```bash:fresh
# 全テーブルをdrop(削除)してからmigrateしてくれる
php artisan migrate:fresh

php artisan migrate:fresh --seed
```
8. テーブルを作り直したいとき、特定のマイグレーションファイルを指定して実行したいとき

基本的にできない。マイグレーションは連続的なバージョン管理システムなのでそういった概念がないのかもしれない。  
なので新規作成してmigrationファイルのup()メソッド内の最初にdrop()をいれる。

```bash:recreate
php artisan make:migration create_users_table
# 2つめを作成、時間がファイル名につくのでエラーにはならない
```
```php
public function up()
    {
        Schema::dropIfExists('users');

        Schema::create('users', function (Blueprint $table) {
            ///
    }
```
```bash
php artisan migrate # success
php artisan rollback # fail
composer dump-autoload
php artisan rollback # fail
```
クラス名が競合しているよと言われたのでクラス名をちょっと変更
```php
class CreateUser2Table extends Migration{}
```
```bash
php artisan rollback # success
```

<br>
ただしくはalterを使う。