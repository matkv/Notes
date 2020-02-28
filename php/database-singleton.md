```php
private static $staticInstance = NULL;

public static function getInstance(){
    if(Database::$staticInstance == NULL){
        Database::$staticInstance = new Database();
        Database::$staticInstance->connect();
    }
    return Database::$staticInstance;
}

//accessing the database
$mydb = Database::getInstance();
```
