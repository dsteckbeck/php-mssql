# php-mssql
Patches for php mssql driver support

This is a patch for the soon-to-be deprecated mssql driver, in the hopes that someone still needing to run PHP 5.x could use this. It compiles against PHP-5.6.8 and a few earlier versions. I haven't tested it on anything newer.

The patch addresses a few areas of improvement:
  1. It comments out Ilia's if_ilia0 around trimming of end whitespace characters on CHAR() columns. If you're stuck with a DB schema that contains CHAR columns, then most of the time, the extra spaces just get in the way, especially when testing strings. To save you the effort of having to trim() the string, we just let the compiled driver do it.
  2. I've added an INI entry called [mssql.guidconvert]. The default is 0, which means don't touch the returned guid. You'd still need to call mssql_guid_string() on the result to do much with it. If you set the value to 1, the driver will convert it to a 36 char guid string. If you set the value to 2, it will convert the guid to a 32 char octet hex string.
  3. A few typecast compilier warnings that are cleaned up
