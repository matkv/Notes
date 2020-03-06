# Errors

It is possible to get information about errors by setting ```display_errors = ON``` in the php.ini file (/opt/lampp/etc/php.ini) 
or by accessing the ```error_log``` file in /opt/lampp/logs - among other things, all the PHP errors & warnings are shown here.

However if we set ```display_errors = ON```, catching exceptions won't work while it is set, the errors will be shown nonetheless.

So while working on a website, it probably makes sense to turn ```display_errors = ON```, but once it is finished it should be turned off again so that exceptions are caught as usual and the desired output is shown.

```php
$this->connection = new mysqli($this->ip, $this->username, $this->password, $this->dbname);

         if ($this->connection->connect_error) {
             echo 'Error while connecting to database';
         }
```

This will only work if the value is set to ```off``` in the ini file.