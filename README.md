#### Not for ~~Windows users~~ the faint hearted

## Mosaic generator using PHP, GD, MySQL

_Forked from [`eflorit/mosaic-generator`](https://github.com/eflorit/mosaic-generator) (and quite a lot is updated)_

Setup changes:
 - Add Docker support
 - Use PHP 8.x
 - Use MySQL 8.x

### Installation

1. Make sure you have Docker installed
1. Run `docker-compose up -d`
   1. This will start PHP and MySQL containers
   1. MySQL server host is `23.45.1.2`
   2. Username, password, and database name are `mosaic`
1. Create the table [ TODO: Create entrypoint script to do this]
    ```sql
        CREATE TABLE IF NOT EXISTS `thumbnails` (
          `filename` varchar(255) NOT NULL,
          `red` smallint(6) NOT NULL,
          `green` smallint(6) NOT NULL,
          `blue` smallint(6) NOT NULL
        );
    ```
1. Copy as many different pictures as you can to ./photos (at least a few hundreds)
1. Modify variables from Mosaic.php to your needs (especially database info)
1. Connect to the PHP container
    ```bash
    docker-compose exec mosaic-app bash
    ```

### Usage

From command line:
```bash
./cl-script.php --input {filename} --rows {int} --columns {int} [--thumbs]

--input                  path to the original picture that shall be recreated
--rows                   number of thumbnails to create per row
--columns                number of thumbnails to create per column
--no-thumbs (optional)   will not (re)generate thumbnails
```

...Directly from class:

```php
$ouput_filename = new Mosaic(string $input_filename, int $rows, int $columns [, bool $gen_thumbs = true ] );
```

### Troubleshoot

You may need to tweak your php config and increase `max_execution_time` and/or `memory_limit` if you're not using cl-script.php.

This is what an outpout looks like:

![demo](https://github.com/jdecode/mosaic-generator/raw/main/examples/output-demo.jpg)

256 rows and 256 columns.
10.000 pictures were used

