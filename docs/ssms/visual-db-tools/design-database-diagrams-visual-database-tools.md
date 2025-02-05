---
title: Diseñar diagramas de base de datos (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdtsql.chm:65536
- vdt.DatabaseDesigner
helpviewer_keywords:
- Database Diagram Designer
- Visual Database Tools [SQL Server], database diagrams
- database diagrams [SQL Server], designing
- diagrams [SQL Server], designing
ms.assetid: 6d2c14e1-3d73-4d10-ae5b-7f2b5d6c4ea8
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 55505f8f14bb28d2724bbb53b733b25311b0e0a9
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/16/2019
ms.locfileid: "68263778"
---
# <a name="design-database-diagrams-visual-database-tools"></a>Diseñar diagramas de base de datos (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
El Diseñador de bases de datos es una herramienta visual que permite diseñar y ver una base de datos a la que está conectado. Cuando diseña una base de datos, puede utilizar el Diseñador de bases de datos para crear, editar o eliminar tablas, columnas, claves, índices, relaciones y restricciones. Para ver una base de datos, puede crear uno o varios diagramas que muestren algunas o todas las tablas, columnas, claves y relaciones de la base de datos.  
  
![Diagrama de base de datos en el que se ilustran las relaciones de tabla](../../ssms/visual-db-tools/media/dv3w7c1.gif "Diagrama de base de datos en el que se ilustran las relaciones de tabla")  
  
Para cualquier base de datos, puede crear tantos diagramas de base de datos como desee; cada tabla de base de datos puede aparecer en un número cualquiera de diagramas. De este modo, puede crear diagramas distintos para ver partes diferentes de la base de datos o resaltar diversos aspectos del diseño. Por ejemplo, puede crear un diagrama grande que muestre todas las tablas con sus columnas y también puede crear un diagrama más pequeño que muestre todas las tablas sin mostrar las columnas.  
  
Cada diagrama de base de datos que crea se almacena en la base de datos asociada.  
  
## <a name="tables-and-columns-in-a-database-diagram"></a>Tablas y columnas de un diagrama de base de datos  
En un diagrama de base de datos, cada tabla puede aparecer con tres características distintas: una barra de título, un selector de fila y un conjunto de columnas de propiedades.  
  
**Barra de título** La barra de título muestra el nombre de la tabla  
  
Si ha modificado una tabla y no la ha guardado todavía, aparecerá un asterisco (*) al final del nombre de la tabla que indica que hay cambios no guardados. Para información sobre cómo guardar tablas y diagramas modificados, consulte [Trabajar con diagramas de base de datos &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/work-with-database-diagrams-visual-database-tools.md)  
  
**Selector de fila** Puede hacer clic en el selector de fila para seleccionar una columna de base de datos de la tabla. El selector de fila muestra un símbolo de clave si la columna se encuentra en la clave principal de la tabla. Para información sobre las claves principales, consulte [Trabajar con claves (Visual Database Tools)](https://msdn.microsoft.com/31fbcc9f-2dc5-4bf9-aa50-ed70ec7b5bcd).  
  
**Columnas de propiedades** El conjunto de columnas de propiedades solo es visible en determinadas vistas de la tabla. Dispone de cinco vistas diferentes para ver una tabla, que le ayudan a controlar el tamaño y el diseño del diagrama.  
  
Para más información sobre las vistas de tabla, consulte [Personalizar la cantidad de información mostrada en los diagramas &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/customize-the-amount-of-information-displayed-in-diagrams-visual-database-tools.md).  
  
## <a name="relationships-in-a-database-diagram"></a>Relaciones de un diagrama de base de datos  
En un diagrama de base de datos, cada relación puede aparecer con tres características distintas: los extremos, un estilo de línea y las tablas relacionadas.  
  
**Extremos** Los extremos de la línea indican si la relación es de uno a uno o de uno a varios. Si una relación tiene una clave en un extremo y un símbolo en forma de ocho en el otro extremo, se trata de una relación de uno a varios. Si una relación tiene una clave en cada extremo, se trata de una relación de uno a uno.  
  
**Estilo de línea** La línea en sí misma (no sus extremos) indica si el sistema de administración de bases de datos (DBMS) exige integridad referencial para la relación cuando se agregan datos nuevos a la tabla de clave externa. Si la línea aparece sólida, el DBMS exige integridad referencial para la relación cuando se agregan o modifican filas en la tabla de clave externa. Si la línea aparece punteada, el DBMS no exige integridad referencial para la relación cuando se agregan o modifican filas en la tabla de clave externa.  
  
**Tablas relacionadas** Una relación de clave externa entre dos tablas se indica mediante una línea de relación entre ellas. En el caso de una relación de uno a varios, la tabla de clave externa es la tabla situada cerca del símbolo en forma de ocho de la línea. Si ambos extremos de la línea están conectados a la misma tabla, la relación es reflexiva. Para más información, consulte [Dibujar relaciones reflexivas &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/draw-reflexive-relationships-visual-database-tools.md).  
  
## <a name="in-this-section"></a>En esta sección  
[Descripción de la propiedad de un diagrama de base de datos &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/understand-database-diagram-ownership-visual-database-tools.md)  
  
[Desplazarse por el Diseñador de diagramas de base de datos &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/navigate-in-database-diagram-designer-visual-database-tools.md)  
  
[Configurar el Diseñador de diagramas de base de datos &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/set-up-database-diagram-designer-visual-database-tools.md)  
  
[Actualizar diagramas de base de datos de ediciones anteriores &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/upgrade-database-diagrams-from-previous-editions-visual-database-tools.md)  
  
[Abrir el Diseñador de diagramas de base de datos &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/open-database-diagram-designer-visual-database-tools.md)  
  
## <a name="see-also"></a>Consulte también  
[Trabajar con diagramas de base de datos &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/work-with-database-diagrams-visual-database-tools.md)  
[Trabajar con tablas en diagramas de base de datos &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/work-with-tables-in-database-diagram-visual-database-tools.md)  
[Trabajar con el diseño de diagramas &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/work-with-diagram-layout-visual-database-tools.md)  
  
