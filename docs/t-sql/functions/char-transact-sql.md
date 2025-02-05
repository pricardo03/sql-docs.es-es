---
title: CHAR (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/19/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- char_TSQL
- char
dev_langs:
- TSQL
helpviewer_keywords:
- converting int ASCII code to character
- control characters
- tab
- ASCII conversions
- CHAR function
- carriage return
- inserting control characters
- characters [SQL Server], control
- line feed
- printing ASCII values
ms.assetid: 955afe94-539c-465d-af22-16ec45da432a
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2765c7c610bd37e68124d7b45ddd0390cc8777dd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68113700"
---
# <a name="char-transact-sql"></a>CHAR (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Esta función convierte un código ASCII **int** en un valor de carácter.
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
  
```
CHAR ( integer_expression )  
```  
  
## <a name="arguments"></a>Argumentos  
*integer_expression*  
Un entero entre 0 y 255. `CHAR` devuelve un valor `NULL` para las expresiones de entero fuera de este intervalo, o cuando el entero expresa solo el primer byte de un carácter de doble byte.

> [!NOTE]
> Algunos juegos de caracteres no europeos, como [Shift Japanese Industrial Standards](https://www.wikipedia.org/wiki/Shift_JIS), incluyen caracteres que se pueden representar en un esquema de codificación de byte único, pero requieren una codificación multibyte. Para más información sobre los juegos de caracteres, vea [Single-Byte and Multibyte Character Sets](/cpp/c-runtime-library/single-byte-and-multibyte-character-sets). 
  
## <a name="return-types"></a>Tipos de valores devueltos
**char(1)**
  
## <a name="remarks"></a>Notas  
Use `CHAR` para insertar caracteres de control en las cadenas de caracteres. En esta tabla se muestran algunos caracteres de control usado con frecuencia.
  
|Carácter de control|Valor|  
|---|---|
|Pestaña|**char(9)**|  
|Avance de línea|**char(10)**|  
|Retorno de carro|**char(13)**|  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-using-ascii-and-char-to-print-ascii-values-from-a-string"></a>A. Usar ASCII y CHAR para imprimir los valores ASCII de una cadena  
En este ejemplo se imprimen el valor y el carácter ASCII de cada carácter de la cadena `New Moon`.
  
```sql
SET TEXTSIZE 0;  
-- Create variables for the character string and for the current   
-- position in the string.  
DECLARE @position int, @string char(8);  
-- Initialize the current position and the string variables.  
SET @position = 1;  
SET @string = 'New Moon';  
WHILE @position <= DATALENGTH(@string)  
   BEGIN  
   SELECT ASCII(SUBSTRING(@string, @position, 1)),   
      CHAR(ASCII(SUBSTRING(@string, @position, 1)))  
   SET @position = @position + 1  
   END;  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
----------- -
78          N  
----------- -  
101         e  
----------- -  
119         w  
----------- -  
32  
----------- -  
77          M  
----------- -  
111         o  
----------- -  
111         o  
----------- - 
110         n  
```
  
### <a name="b-using-char-to-insert-a-control-character"></a>B. Usar CHAR para insertar un carácter de control  
En este ejemplo se usa `CHAR(13)` para imprimir el nombre y la dirección de correo electrónico de un empleado en líneas independientes cuando la consulta devuelve los resultados en formato de texto. En este ejemplo se usa la base de datos [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].
  
```sql
SELECT p.FirstName + ' ' + p.LastName, + CHAR(13)  + pe.EmailAddress   
FROM Person.Person p 
INNER JOIN Person.EmailAddress pe ON p.BusinessEntityID = pe.BusinessEntityID  
  AND p.BusinessEntityID = 1;  
GO  
```
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
Ken Sanchez
ken0@adventure-works.com
  
(1 row(s) affected)
```
  
### <a name="c-using-ascii-and-char-to-print-ascii-values-from-a-string"></a>C. Usar ASCII y CHAR para imprimir los valores ASCII de una cadena  
En este ejemplo se da por hecho que hay un juego de caracteres ASCII. Devuelve el valor de carácter de seis valores numéricos de caracteres ASCII diferentes.
  
```sql
SELECT CHAR(65) AS [65], CHAR(66) AS [66],   
CHAR(97) AS [97], CHAR(98) AS [98],   
CHAR(49) AS [49], CHAR(50) AS [50];  
```
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
65   66   97   98   49   50  
---- ---- ---- ---- ---- ----  
A    B    a    b    1    2  
```
  
### <a name="d-using-char-to-insert-a-control-character"></a>D. Usar CHAR para insertar un carácter de control  
En este ejemplo se usa `CHAR(13)` para devolver información de sys.databases en líneas independientes cuando la consulta devuelve sus resultados como texto.
  
```sql
SELECT name, 'was created on ', create_date, CHAR(13), name, 'is currently ', state_desc   
FROM sys.databases;  
GO  
```
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
name                                      create_date               name                                  state_desc  
--------------------------------------------------------------------------------------------------------------------  
master                    was created on  2003-04-08 09:13:36.390   master                  is currently  ONLINE 
tempdb                    was created on  2014-01-10 17:24:24.023   tempdb                  is currently  ONLINE   
AdventureWorksPDW2012     was created on  2014-05-07 09:05:07.083   AdventureWorksPDW2012   is currently  ONLINE 
```

### <a name="e-using-char-to-return-single-byte-characters"></a>E. Usar CHAR para devolver caracteres de byte único  
Este ejemplo utiliza valores enteros y hexadecimales en el intervalo válido para ASCII. La función CHAR es capaz de generar el carácter japonés de byte único.
  
```sql
SELECT CHAR(188) AS single_byte_representing_complete_character, 
  CHAR(0xBC) AS single_byte_representing_complete_character;  
GO  
```
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
single_byte_representing_complete_character single_byte_representing_complete_character
------------------------------------------- -------------------------------------------
ｼ                                           ｼ                                         
```

### <a name="f-using-char-to-return-multibyte-characters"></a>F. Usar CHAR para devolver caracteres multibyte  
Este ejemplo utiliza un valor entero y hexadecimal en el intervalo válido para ASCII. Sin embargo, la función CHAR devuelve NULL porque el parámetro representa solo el primer byte de un carácter multibyte.
  
```sql
SELECT CHAR(129) AS first_byte_of_double_byte_character, 
  CHAR(0x81) AS first_byte_of_double_byte_character;  
GO  
```
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
first_byte_of_double_byte_character first_byte_of_double_byte_character
----------------------------------- -----------------------------------
NULL                                NULL                                         
```
  
## <a name="see-also"></a>Vea también
 [ASCII &#40;Transact-SQL&#41;](../../t-sql/functions/ascii-transact-sql.md)  
 [NCHAR &#40;Transact-SQL&#41;](../../t-sql/functions/nchar-transact-sql.md)  
 [UNICODE &#40;Transact-SQL&#41;](../../t-sql/functions/unicode-transact-sql.md)  
 [+ &#40;Concatenación de cadenas&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/string-concatenation-transact-sql.md)  
 [Funciones de cadena &#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)
  
  

