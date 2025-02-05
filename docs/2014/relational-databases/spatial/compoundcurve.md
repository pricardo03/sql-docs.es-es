---
title: CompoundCurve | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: ae357f9b-e3e2-4cdf-af02-012acda2e466
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: e234b06917d77e68577e72fbdc7bca1ad033cef8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66014341"
---
# <a name="compoundcurve"></a>CompoundCurve
  Una `CompoundCurve` es una recopilación de cero o más instancias de `CircularString` o `LineString` de tipos de geometría o de geografía.  
  
> [!IMPORTANT]  
>  Para obtener una descripción detallada y ejemplos de las nuevas características espaciales en esta versión, incluido el `CompoundCurve` subtipo, descargue las notas del producto, [nuevas características espaciales de SQL Server 2012](https://go.microsoft.com/fwlink/?LinkId=226407).  
  
 Se puede crear una instancia vacía de `CompoundCurve`, pero para que una `CompoundCurve` sea válida debe cumplir los siguientes criterios:  
  
1.  Debe contener al menos una instancia de `CircularString` o de `LineString`.  
  
2.  La secuencia de instancias de `CircularString` o `LineString` debe ser continua.  
  
 Si un `CompoundCurve` contiene una secuencia de varias `CircularString` y `LineString` instancias, el extremo final de cada instancia, salvo el último debe ser el extremo inicial de la siguiente instancia de la secuencia. Esto significa que si el punto final de una instancia anterior de la secuencia es (4 3 7 2), el punto inicial para la instancia siguiente de la secuencia debe ser (4 3 7 2). Observe que los valores M (medida) y Z (elevación) para el punto también deben ser iguales. Si hay diferencia entre ambos puntos, se produce una excepción `System.FormatException` . Los puntos de una `CircularString` no tienen que tener valor Z o M. Si no se proporcionan valores Z o M para el punto final de la instancia anterior, el punto inicial de la instancia siguiente no puede incluir valores Z o M. Si el punto final para la secuencia anterior es (4 3), el punto inicial para la secuencia siguiente debe ser (4 3); no puede ser (4 3 7 2). Todos los puntos de una instancia `CompoundCurve` deben tener el mismo valor Z, o bien, ningún valor Z.  
  
## <a name="compoundcurve-instances"></a>Instancias de CompoundCurve  
 La siguiente ilustración muestra tipos válidos de `CompoundCurve`.  
  
 ![](../../database-engine/media/f278742e-b861-4555-8b51-3d972b7602bf.png "f278742e-b861-4555-8b51-3d972b7602bf")  
  
### <a name="accepted-instances"></a>Instancias aceptadas  
 Se acepta la instancia `CompoundCurve` si es una instancia vacía o cumple los siguientes criterios.  
  
1.  Todas las instancias contenidas en la instancia `CompoundCurve` son instancias de segmento de arco circular aceptadas. Para obtener más información sobre instancias de segmento de arco circular aceptadas, vea [LineString](linestring.md) y [CircularString](circularstring.md).  
  
2.  Todos los segmentos de arco circulares contenidos en la instancia `CompoundCurve` están conectados. El primer punto de cada segmento de arco circular siguiente coincide con el último punto del segmento de arco circular precedente.  
  
    > [!NOTE]  
    >  Esto incluye las coordenadas Z y M. Por tanto, las cuatro coordenadas X, Y, Z y M deben coincidir para ambos puntos.  
  
3.  Ninguna de las instancias contenidas son instancias vacías.  
  
 El siguiente ejemplo muestra instancias aceptadas de `CompoundCurve`.  
  
```  
DECLARE @g1 geometry = 'COMPOUNDCURVE EMPTY';  
DECLARE @g2 geometry = 'COMPOUNDCURVE(CIRCULARSTRING(1 0, 0 1, -1 0), (-1 0, 2 0))';  
```  
  
 El siguiente ejemplo muestra instancias de `CompoundCurve` no aceptadas. Estas instancias producen una excepción `System.FormatException`.  
  
```  
DECLARE @g1 geometry = 'COMPOUNDCURVE(CIRCULARSTRING EMPTY)';  
DECLARE @g2 geometry = 'COMPOUNDCURVE(CIRCULARSTRING(1 0, 0 1, -1 0), (1 0, 2 0))';  
```  
  
### <a name="valid-instances"></a>Instancias válidas  
 Una instancia de `CompoundCurve` es válida si cumple los siguientes criterios.  
  
1.  La instancia de `CompoundCurve` es aceptada.  
  
2.  Todas las instancias de segmento de arco circular contenidas en la instancia `CompoundCurve` son instancias válidas.  
  
 En el siguiente ejemplo se muestran instancias válidas de `CompoundCurve`.  
  
```  
DECLARE @g1 geometry = 'COMPOUNDCURVE EMPTY';  
DECLARE @g2 geometry = 'COMPOUNDCURVE(CIRCULARSTRING(1 0, 0 1, -1 0), (-1 0, 2 0))';  
DECLARE @g3 geometry = 'COMPOUNDCURVE(CIRCULARSTRING(1 1, 1 1, 1 1), (1 1, 3 5, 5 4))';  
SELECT @g1.STIsValid(), @g2.STIsValid(), @g3.STIsValid();  
  
```  
  
 `@g3` es válido porque la instancia `CircularString` es válida. Para obtener más información sobre la validez de la `CircularString` la instancia, vea [CircularString](circularstring.md).  
  
 El siguiente ejemplo muestra instancias de `CompoundCurve` no válidas.  
  
```  
DECLARE @g1 geometry = 'COMPOUNDCURVE(CIRCULARSTRING(1 1, 1 1, 1 1), (1 1, 3 5, 5 4, 3 5))';  
DECLARE @g2 geometry = 'COMPOUNDCURVE((1 1, 1 1))';  
DECLARE @g3 geometry = 'COMPOUNDCURVE(CIRCULARSTRING(1 1, 2 3, 1 1))';  
SELECT @g1.STIsValid(), @g2.STIsValid(), @g3.STIsValid();  
```  
  
 `@g1` no es válida porque la segunda instancia no es una instancia válida de LineString. `@g2` no es válida porque la instancia de `LineString` no es válida. `@g3` no es válida porque la instancia de `CircularString` no es válida. Para obtener más información sobre válido `CircularString` y `LineString` instancias, consulte [CircularString](circularstring.md) y [LineString](linestring.md).  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-instantiating-a-geometry-instance-with-an-empty-compooundcurve"></a>A. Crear una instancia de geometry con una CompoundCurve vacía  
 En el ejemplo siguiente, se muestra cómo crear una instancia vacía de `CompoundCurve` :  
  
```sql  
DECLARE @g geometry;  
SET @g = geometry::Parse('COMPOUNDCURVE EMPTY');  
```  
  
### <a name="b-declaring-and-instantiating-a-geometry-instance-using-a-compoundcurve-in-the-same-statement"></a>b. Declarar y crear una instancia de geometry usando una CompoundCurve en la misma instrucción  
 En el siguiente ejemplo, se muestra cómo declarar e inicializar una instancia de `geometry` con una `CompoundCurve`en la misma instrucción:  
  
```sql  
DECLARE @g geometry = 'COMPOUNDCURVE ((2 2, 0 0),CIRCULARSTRING (0 0, 1 2.1082, 3 6.3246, 0 7, -3 6.3246, -1 2.1082, 0 0))';  
```  
  
### <a name="c-instantiating-a-geography-instance-with-a-compoundcurve"></a>C. Crear una instancia de geography con una CompoundCurve  
 En el siguiente ejemplo, se muestra cómo declarar e inicializar una instancia `geography` con una `CompoundCurve`:  
  
```sql  
DECLARE @g geography = 'COMPOUNDCURVE(CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))';  
```  
  
### <a name="d-storing-a-square-in-a-compoundcurve-instance"></a>D. Almacenar un cuadrado en una instancia de CompoundCurve  
 En el siguiente ejemplo, se muestran dos maneras diferentes de utilizar una instancia `CompoundCurve` para almacenar un cuadrado.  
  
```sql  
DECLARE @g1 geometry, @g2 geometry;  
SET @g1 = geometry::Parse('COMPOUNDCURVE((1 1, 1 3), (1 3, 3 3),(3 3, 3 1), (3 1, 1 1))');  
SET @g2 = geometry::Parse('COMPOUNDCURVE((1 1, 1 3, 3 3, 3 1, 1 1))');  
SELECT @g1.STLength(), @g2.STLength();  
```  
  
 Las longitudes de `@g1` y `@g2` son iguales. Observe en el ejemplo que una instancia de `CompoundCurve` puede almacenar una o más instancias de `LineString`.  
  
### <a name="e-instantiating-a-geometry-instance-using-a-compoundcurve-with-multiple-circularstrings"></a>E. Crear una instancia de geometry usando una CompoundCurve con varias CircularStrings  
 En el siguiente ejemplo, se muestra cómo utilizar dos instancias `CircularString` diferentes para inicializar una `CompoundCurve`.  
  
```sql  
DECLARE @g geometry;  
SET @g = geometry::Parse('COMPOUNDCURVE(CIRCULARSTRING(0 2, 2 0, 4 2), CIRCULARSTRING(4 2, 2 4, 0 2))');  
SELECT @g.STLength();  
```  
  
 Produce el siguiente resultado: 12,566370 …, que equivale a 4???. La instancia de `CompoundCurve` del ejemplo almacena un círculo de radio 2. Ambos ejemplos de código anteriores no tuvieron que utilizar una `CompoundCurve`. Para el primer ejemplo, habría sido más fácil utilizar una instancia de `LineString` , mientras que para el segundo ejemplo habría sido más fácil una instancia de `CircularString` . Sin embargo, el ejemplo siguiente muestra un caso donde `CompoundCurve` proporciona una mejor alternativa.  
  
### <a name="f-using-a-compoundcurve-to-store-a-semicircle"></a>F. Usar una CompoundCurve para almacenar un semicírculo  
 En el siguiente ejemplo, se utiliza una instancia de `CompoundCurve` para almacenar un semicírculo.  
  
```sql  
DECLARE @g geometry;  
SET @g = geometry::Parse('COMPOUNDCURVE(CIRCULARSTRING(0 2, 2 0, 4 2), (4 2, 0 2))');  
SELECT @g.STLength();  
```  
  
### <a name="g-storing-multiple-circularstring-and-linestring-instances-in-a-compoundcurve"></a>G. Almacenar varias instancias de CircularString y LineString en una CompoundCurve  
 En el siguiente ejemplo, se muestra cómo se pueden almacenar varias instancias de `CircularString` y `LineString` mediante una `CompoundCurve`.  
  
```sql  
DECLARE @g geometry  
SET @g = geometry::Parse('COMPOUNDCURVE((3 5, 3 3), CIRCULARSTRING(3 3, 5 1, 7 3), (7 3, 7 5), CIRCULARSTRING(7 5, 5 7, 3 5))');  
SELECT @g.STLength();  
```  
  
### <a name="h-storing-instances-with-z-and-m-values"></a>H. Almacenar instancias con valores Z y M  
 En el siguiente ejemplo, se muestra cómo utilizar una instancia `CompoundCurve` para almacenar una secuencia de instancias `CircularString` y `LineString` con valores Z y M.  
  
```sql  
SET @g = geometry::Parse('COMPOUNDCURVE(CIRCULARSTRING(7 5 4 2, 5 7 4 2, 3 5 4 2), (3 5 4 2, 8 7 4 2))');  
```  
  
### <a name="i-illustrating-why-circularstring-instances-must-be-explicitly-declared"></a>I. Obligación de declarar las instancias de CircularString explícitamente  
 En el siguiente ejemplo, se muestra por qué se deben declarar explícitamente las instancias de `CircularString` . El programador está intentando almacenar un círculo en una instancia de `CompoundCurve` .  
  
```sql  
DECLARE @g1 geometry;    
DECLARE @g2 geometry;  
SET @g1 = geometry::Parse('COMPOUNDCURVE(CIRCULARSTRING(0 2, 2 0, 4 2), (4 2, 2 4, 0 2))');  
SELECT 'Circle One', @g1.STLength() AS Perimeter;  -- gives an inaccurate amount  
SET @g2 = geometry::Parse('COMPOUNDCURVE(CIRCULARSTRING(0 2, 2 0, 4 2), CIRCULARSTRING(4 2, 2 4, 0 2))');  
SELECT 'Circle Two', @g2.STLength() AS Perimeter;  -- now we get an accurate amount  
```  
  
 El resultado es el siguiente:  
  
```  
Circle One11.940039...  
Circle Two12.566370...  
```  
  
 El perímetro para el círculo dos es aproximadamente 4???, que es el valor real para el perímetro. Sin embargo, el perímetro para el círculo uno es significativamente inexacto. La instancia `CompoundCurve` del círculo uno almacena un segmento de arco circular (ABC) y dos segmentos de línea (CD, DA). La instancia `CompoundCurve` tiene que almacenar dos segmentos de arco circular (ABC, CDA) para definir un círculo. Una instancia `LineString` define el segundo conjunto de puntos (4 2, 2 4, 0 2) en la instancia `CompoundCurve` del círculo uno. Es necesario declarar explícitamente una instancia `CircularString` dentro de una `CompoundCurve`.  
  
## <a name="see-also"></a>Vea también  
 [STIsValid &#40;tipo de datos geometry&#41;](/sql/t-sql/spatial-geometry/stisvalid-geometry-data-type)   
 [STLength &#40;tipo de datos geometry&#41;](/sql/t-sql/spatial-geometry/stlength-geometry-data-type)   
 [STStartPoint &#40;tipo de datos geometry&#41;](/sql/t-sql/spatial-geometry/ststartpoint-geometry-data-type)   
 [STEndpoint &#40;tipo de datos geometry&#41;](/sql/t-sql/spatial-geometry/stendpoint-geometry-data-type)   
 [LineString](linestring.md)   
 [CircularString](circularstring.md)   
 [Información general de los tipos de datos espaciales](spatial-data-types-overview.md)   
 [Punto](point.md)  
  
  
