---
title: Acerca de las propiedades OLE DB | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- OLE DB, properties
- SQL Server Native Client OLE DB provider, properties
- properties [OLE DB]
- property values [SQL Server Native Client]
ms.assetid: 0b36a61e-b542-400d-a3d2-e6f643caf2c6
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 265ace9286d9500fff914689a045261c1bec4905
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68050948"
---
# <a name="about-ole-db-properties"></a>Acerca de las propiedades de OLE DB
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Los consumidores establecen valores de propiedades para solicitar el comportamiento de un objeto específico. Por ejemplo, los consumidores usan propiedades para especificar las interfaces que va a exponer un conjunto de filas. Los consumidores obtienen los valores de las propiedades para determinar las capacidades de un objeto, como un conjunto de filas, una sesión o un objeto de origen de datos.  
  
 Cada propiedad incluye un valor, un tipo, una descripción y un atributo de lectura/escritura y, en el caso de las propiedades de conjunto de filas, un indicador de si puede aplicarse columna por columna.  
  
 Una propiedad se identifica mediante un GUID y un número entero que representa el identificador de propiedad. Un conjunto de propiedades es un conjunto de todas las propiedades que comparten el mismo GUID. Además de la propiedad de OLE DB predefinida establece, el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client implementa conjuntos de propiedades específicas del proveedor y las propiedades en ellos. Cada propiedad pertenece a uno o varios grupos de propiedades. Un grupo de propiedades es el grupo de todas las propiedades que se aplican a un objeto determinado. Algunos grupos de propiedades incluyen el grupo de propiedades de inicialización, el grupo de propiedades de origen de datos, el grupo de propiedades de sesión, el grupo de propiedades de conjunto de filas, el grupo de propiedades de tabla y el grupo de propiedades de columna. Hay propiedades en todos estos grupos de propiedades.  
  
 El establecimiento de valores de propiedades implica:  
  
1.  Determinar las propiedades para las que van a establecerse valores.  
  
2.  Determinar los conjuntos de propiedades que contienen las propiedades identificadas.  
  
3.  Asignar una matriz de estructuras DBPROPSET, una para cada conjunto de propiedades identificado.  
  
4.  Asignar una matriz de estructuras DBPROP para cada conjunto de propiedades. El número de elementos de cada matriz es igual al número de propiedades (identificado en el paso 1) que pertenecen a ese conjunto de propiedades.  
  
5.  Rellenar la estructura DBPROP para cada propiedad.  
  
6.  Rellenar la información (GUID del conjunto de propiedades, recuento del número de elementos y un puntero a la matriz DBPROP correspondiente) de la estructura DBPROPSET para cada conjunto de propiedades.  
  
7.  Llamar a un método para establecer las propiedades y pasar el recuento y la matriz de estructuras DBPROPSET.  
  
## <a name="see-also"></a>Vea también  
 [Creación de una aplicación de proveedor SQL Server Native Client OLE DB](../../relational-databases/native-client-ole-db-provider/creating-a-sql-server-native-client-ole-db-provider-application.md)   
 [Propiedades (OLE DB)](https://go.microsoft.com/fwlink/?LinkId=112207)  
  
  
