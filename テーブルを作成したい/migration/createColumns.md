# カラム生成のメソッドまとめ（よく使うやつ）
```php:up method
public function up()
{
    Schema::create('users', function (Blueprint $table) {
        // ここにはいるやつ 
    });
}
```

## プライマリキー

| 型       | 数値範囲                                       |
| ------- | ------------------------------------------ |
| sallint | -32768 ~ 32767                             |
| integer | -2147483648 ~ 2147483647                   |
| bigint  | -9223372036854775808 ~ 9223372036854775807 |

<br>

```php
$table->bigIncrements('id');
$table->increments('id');
$table->tinyIncrements('id');
```

<br>

## ○○_id とかでよく使うint型
```php
$table->integer('user_id');
```

## 文字列　めっちゃつかう

| 型                                | 説明                         |
| -------------------------------- | -------------------------- |
| character(n), char(n)            | n文字制限、後ろの空白をトリムして取得        |
| character varying(n), varchar(n) | n文字制限、うしろに空白があったらそのまま保存、取得 |
| text                             | 制限なし可変長                    |

<br>

charは固定長保存、varcharは可変長保存

```php
$table->char('name', 100);
$table->string('name', 100); // varchar
$table->text('description');
```
