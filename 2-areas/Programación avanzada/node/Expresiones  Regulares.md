
# Expresiones regulares

## resumen regex

. - matches any character except for newline characters
| - matches either of the expressions separated by it
^ - matches the beginning of the string
$ - matches the end of the string
* - matches the preceding expression zero or more times
+ - matches the preceding expression one or more times
? - matches the preceding expression zero or one times
[] - matches any single character in the brackets
() - groups expressions together

Las propiedades de acceso estáticas RegExp.$1,…, RegExp.$9 devuelven coincidencias de subcadenas entre paréntesis.