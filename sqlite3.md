### Export :
```bash
    $ sqlite3 -header -csv db.db "select * from customer;" > out.csv
```    
    
### Import :
```bash
    $ sqlite3 db.db
    sqlite3> .mod csv
    sqlite3> .separator ","
    sqlite3> .import out.csv customer
    ```
