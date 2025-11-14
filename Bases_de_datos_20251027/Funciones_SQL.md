1. Funciones de Texto (String Functions)
SQL Server	            SQLite	                Notas
LEN()	                LENGTH()	            Mide longitud del texto.
LEFT(campo, n)	        SUBSTR(campo, 1, n)	    SQLite no tiene LEFT.
RIGHT(campo, n)	        SUBSTR(campo, -n)	        Usar índice negativo.
SUBSTRING(campo, inicio, len)	SUBSTR(campo, inicio, len)	Muy similar.
UPPER()	UPPER()	Igual.
LOWER()	LOWER()	Igual.
LTRIM()	LTRIM()	Igual.
RTRIM()	RTRIM()	Igual.
LTRIM(RTRIM())	TRIM()	Funciona igual.
REPLACE(campo, a, b)	REPLACE(campo, a, b)	Igual.
CHARINDEX(sub, texto)	INSTR(texto, sub)	Inverso de parámetros.
CONCAT(a,b,c)	`a	


2. Funciones Numéricas
SQL Server	                    SQLite	                Notas
ABS()	                        ABS()	                Igual.
ROUND(num, decimales)	        ROUND(num, decimales)	Igual.
CEILING()	                    CEIL()	SQLite usa CEIL.
FLOOR()	                        FLOOR()	Igual.
POWER(x, y)	                    POWER(x, y)	Igual.
SQRT()	                        SQRT()	Igual.
RAND()	                        RANDOM() / 9223372036854775807.0	RANDOM devuelve entero.





3. Funciones de Fecha y Hora

SQLite maneja fechas como texto (ISO), números o epoch. Usa datetime(), date() y strftime().

SQL Server	                                    SQLite	                    Notas
GETDATE()	                                    datetime('now')	Fecha actual.
CURRENT_TIMESTAMP	                            CURRENT_TIMESTAMP	Igual.
DATEADD(día, n, fecha)	                        date(fecha, '+n day')	Ej: date('now', '+3 day').
DATEDIFF(día, f1, f2)	                        julianday(f2) - julianday(f1)	Diferencia en días.
DATENAME()	                                    strftime('%w'), etc.	Usar formatos.
YEAR(fecha)	                                    strftime('%Y', fecha)	Año.
MONTH(fecha)	                                strftime('%m', fecha)	Mes.
DAY(fecha)	                                    strftime('%d', fecha)	Día.
GETUTCDATE()	                                datetime('now','utc')	UTC.


FORMATOS útiles con strftime()

%Y año
%m mes
%d día
%H hora
%M minuto
%S segundo


4. Funciones de Agregación
SQL Server	                            SQLite	Notas
COUNT()	                                COUNT()	Igual.
SUM()	                                SUM()	Igual.
AVG()	                                AVG()	Igual.
MIN()	                                MIN()	Igual.
MAX()	                                MAX()	Igual.
STRING_AGG()	                        GROUP_CONCAT()	Hace concatenación.


5. Funciones Lógicas / Condicionales
SQL Server	SQLite	Notas
IIF(cond, a, b)	CASE WHEN cond THEN a ELSE b END	SQLite no tiene IIF.
CASE	CASE	Igual.
COALESCE()	COALESCE()	Igual.
ISNULL(campo, valor)	IFNULL(campo, valor)	SQL Server → ISNULL / SQLite → IFNULL.




6. Funciones de Conversión
SQL Server	SQLite	Notas
CAST(x AS INT)	CAST(x AS INTEGER)	Igual.
CAST(x AS VARCHAR)	CAST(x AS TEXT)	SQLite usa TEXT.
CONVERT(VARCHAR, fecha, estilo)	strftime('%Y-%m-%d', fecha)	Requiere formatos.



7. Funciones Matemáticas adicionales
SQL Server	SQLite	Notas
PI()	PI()	Disponible.
EXP()	EXP()	Exponencial.
LOG()	LOG()	Natural.
LOG10()	LOG10()	Igual.



8. Window Functions (Funciones Analíticas)

SQLite sí soporta Window Functions desde la versión 3.25+.

SQL Server	SQLite	Notas
ROW_NUMBER()	ROW_NUMBER()	Igual.
RANK()	RANK()	Igual.
DENSE_RANK()	DENSE_RANK()	Igual.
LEAD()	LEAD()	Igual.
LAG()	LAG()	Igual.
OVER(PARTITION BY …)	OVER(PARTITION BY …)	Igual.





9. Funciones de Sistema
SQL Server	SQLite	Notas
@@VERSION	sqlite_version()	Similar información.
DB_NAME()	No existe	SQLite solo tiene archivo.
SCOPE_IDENTITY()	last_insert_rowid()	Último ID insertado.





SELECT *
FROM Clientes
LIMIT 100;


1. TOP en SQL Server → LIMIT en SQLite
SELECT date('now', '+7 day');
2. DATEADD en SQL Server → date() en SQLite
SELECT date('2024-02-01', '+2 month');
3. LEFT() en SQL Server → SUBSTR() en SQLite
SELECT SUBSTR('ABCDE', 1, 3);
4. RIGHT() en SQL Server → SUBSTR() negativo en SQLite
SELECT SUBSTR('ABCDE', -2);


5. JOINs
🔷 LEFT JOIN (funciona igual en SQLite)
SELECT a.Id, a.Nombre, b.Saldo
FROM Clientes a
LEFT JOIN Cuentas b ON a.Id = b.ClienteId;


🔷 RIGHT JOIN
SQLite NO soporta RIGHT JOIN.
Debes convertirlo en LEFT JOIN invirtiendo tablas.
SELECT *
FROM B
LEFT JOIN A ON A.Id = B.Id;


6. HASH (HASHBYTES en SQL Server)
SELECT lower(hex(md5('hola')));

7. CONVERT y CAST
SELECT strftime('%Y-%m-%d', 'now');

8. STRING_AGG en SQL Server → GROUP_CONCAT en SQLite
SELECT GROUP_CONCAT(nombre, ',') AS Nombres
FROM Personas;

9. CASE WHEN (igual en ambos)
SELECT CASE WHEN Edad >= 18 THEN 'Adulto' ELSE 'Menor' END;


10. TOP con Order By → LIMIT + OFFSET
SELECT *
FROM Ventas
ORDER BY Fecha DESC
LIMIT 100;

TOP N desde la fila 10 (OFFSET)
SELECT *
FROM Ventas
ORDER BY Fecha DESC
LIMIT 100 OFFSET 10;



comentar script 
/*limit 1*/
--limit 1
