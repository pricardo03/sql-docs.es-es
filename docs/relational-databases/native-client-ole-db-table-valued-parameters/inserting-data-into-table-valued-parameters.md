---
title: Insertar datos en parámetros con valores de tabla | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- table-valued parameters, inserting data into
ms.assetid: 9c1a3234-4675-40d3-b473-8df06208f880
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: eb8e32b0008cba846679e7704a3a9ab9cef6e93d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68103439"
---
# <a name="inserting-data-into-table-valued-parameters"></a>Insertar datos en parámetros con valores de tabla
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor Native Client OLE DB admite dos modelos para el consumidor especifique datos para filas de parámetros con valores de tabla: un modelo de inserción y un modelo de extracción. Hay disponible un ejemplo que muestra el modelo de extracción; vea [Ejemplos de programación de datos de SQL Server](https://msftdpprodsamples.codeplex.com/).  
  
> [!NOTE]  
>  Una columna de parámetros con valores de tabla debe tener valores no predeterminados en todas las filas o valores predeterminados en todas las filas. No es posible tener valores predeterminados en algunas filas y en otras no. Por lo tanto, en enlaces de parámetros con valores de tabla, los únicos valores de estado permitidos en datos de columnas de conjunto de filas de parámetros con valores de tabla son DBSTATUS_S_ISNULL y DBSTATUS_S_OK. DBSTATUS_S_DEFAULT generará un error y el valor de estado enlazado se establecerá en DBSTATUS_E_BADSTATUS.  
  
## <a name="push-model-loads-all-table-valued-paremeter-data-in-memory"></a>Modelo de inserción (carga todos los datos de parámetros con valores de tabla en memoria)  
 El modelo de inserción es similar al uso de conjuntos de parámetros (es decir, el parámetro DBPARAMS de ICommand::Execute). El modelo de inserción solo se usa si los objetos de conjunto de filas de parámetros con valores de tabla se usan sin una implementación personalizada de las interfaces IRowset. Se recomienda usar el modelo de inserción cuando el número de filas del conjunto de filas de parámetros con valores de tabla sea pequeño y no se espere que vaya a haber un exceso de presión de memoria en la aplicación. Este modelo es más sencillo que el modelo de extracción, ya que no requiere ninguna otra funcionalidad por parte de la aplicación del consumidor más que la actualmente común en aplicaciones OLE DB típicas.  
  
 Se espera que el consumidor proporcione todos los datos de parámetro con valores de tabla al proveedor antes de ejecutar un comando. Para proporcionar los datos, el consumidor rellena un objeto de conjunto de filas de parámetros con valores de tabla por cada parámetro con valores de tabla. El objeto de conjunto de filas de parámetro con valores de tabla expone las operaciones Insert, Set y Delete del conjunto de filas, que el consumidor usará para manipular los datos de parámetros con valores de tabla. El proveedor capturará los datos de este objeto de conjunto de filas de parámetros con valores de tabla en tiempo de ejecución.  
  
 Cuando se proporciona al consumidor un objeto de conjunto de filas de parámetros con valores de tabla, el consumidor puede procesarlo como un objeto de conjunto de filas. El consumidor puede obtener la información de tipo de cada columna (tipo, longitud máxima, precisión y escala) mediante el método de interfaz IColumnsInfo:: GetColumnInfo o IColumnsRowset:: GetColumnsRowset. A continuación, el consumidor crea un descriptor de acceso para especificar los enlaces de los datos. El paso siguiente consiste en insertar filas de datos en el conjunto de filas de parámetros con valores de tabla. Esto puede hacerse mediante el uso de IRowsetChange:: insertRow. IRowsetChange:: SetData o IRowsetChange:: DeleteRows también se utiliza en el objeto de conjunto de filas de parámetros con valores de tabla si tiene que manipular los datos. Los objetos de conjunto de filas de parámetros con valores de tabla son objetos en los que se cuentan las referencias, similares a los objetos de flujo.  
  
 Si se usa IColumnsRowset:: GetColumnsRowset, habrá posteriores llamadas a IRowset:: GetNextRows, IRowset:: GetData e IRowset:: ReleaseRows métodos en el objeto de conjunto de filas de la columna resultante.  
  
 Después de la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor Native Client OLE DB comienza a ejecutar el comando, los valores de parámetro con valores de tabla se capturan de este objeto de conjunto de filas de parámetros con valores de tabla y se enviarán al servidor.  
  
 El modelo de inserción requiere un trabajo mínimo por parte del consumidor pero usa más memoria que el modelo de extracción, porque todos los datos de parámetro con valores de tabla deben estar en memoria en tiempo de ejecución.  
  
## <a name="pull-model-obtaining-table-valued-parameter-data-on-demand-from-the-consumer"></a>Modelo de extracción (obtener datos de parámetros con valores de tabla a petición del consumidor)  
 El modelo de extracción resulta útil en dos escenarios:  
  
-   Para transmitir filas por secuencias.  
  
-   Si se usa un conjunto de filas de otro proveedor como valor de parámetro con valores de tabla.  
  
 En el modelo de extracción, el consumidor proporciona datos a petición al proveedor. Use este enfoque si la aplicación tiene muchas inserciones de datos y los datos de conjunto de filas de parámetros con valores de tabla en memoria podrían dar lugar a un acceso excesivo a la memoria. Si se usan varios proveedores OLE DB, el modelo de extracción del consumidor permite que el consumidor proporcione cualquier objeto de conjunto de filas como valor de parámetro con valores de tabla.  
  
 Para usar el modelo de extracción, los consumidores deben proporcionar su propia implementación de un objeto de conjunto de filas. Cuando se usa el modelo de extracción con conjuntos de filas de parámetro con valores de tabla (CLSID_ROWSET_TVP), el consumidor se debe agregar el objeto de conjunto de filas de parámetro con valores de tabla que el proveedor expone a través de la ITableDefinitionWithConstraints:: Al método CreateTableWithConstraints o IOpenRowset:: OpenRowset. Solo se espera que el objeto de consumidor invalide la implementación de la interfaz IRowset. Debe invalidar las funciones siguientes:  
  
-   IRowset::GetNextRows  
  
-   IRowset::AddRefRows  
  
-   IRowset::GetData  
  
-   IRowset::ReleaseRows  
  
-   IRowset::RestartPosition  
  
 El proveedor OLE DB de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client leerá una o varias filas del objeto de conjunto de filas del consumidor a la vez para admitir el comportamiento de transmisión por secuencias en parámetros con valores de tabla. Por ejemplo, el usuario puede tener los datos de conjunto de filas de parámetros con valores de tabla en el disco (no en la memoria) e implementar la funcionalidad necesaria para leer datos del disco cuando así lo requiera el proveedor OLE DB de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
 El consumidor comunicará su formato de datos para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor Native Client OLE DB mediante el uso de IAccessor:: CreateAccessor en el objeto de conjunto de filas de parámetros con valores de tabla. Al leer los datos del búfer del consumidor, el proveedor comprueba que todas las columnas de escritura no predeterminadas están disponibles a través de al menos un identificador de descriptor de acceso, y usa los identificadores correspondientes para leer los datos de las columnas. Para evitar la ambigüedad, tiene que existir una correspondencia de uno a uno entre una columna de conjunto de filas de parámetros con valores de tabla y un enlace. Los enlaces duplicados a la misma columna generarán un error. Además, se espera que cada descriptor de acceso tiene el *iOrdinal* miembro DBBindings en secuencia. Habrá tantas llamadas a IRowset::GetData como número de descriptores de acceso por fila y el orden de las llamadas se basará en el orden del valor *iOrdinal*, de menor a mayor.  
  
 Se espera que el proveedor implemente la mayoría de las interfaces expuestas por el objeto de conjunto de filas de parámetros con valores de tabla. El consumidor implementará un objeto de conjunto de filas con interfaces mínimas (IRowset). Debido a la agregación oculta, el objeto de conjunto de filas de parámetros con valores de tabla implementará todas las demás interfaces obligatorias del objeto de conjunto de filas.  
  
 En cualquier otro objeto de conjunto de filas, como los objetos de conjunto de filas que se obtienen para cualquier proveedor OLE DB, el conjunto de filas proporcionado por el consumidor debe implementar todas las interfaces obligatorias del objeto de conjunto de filas, tal y como se indica en la especificación de OLE DB.  
  
 En tiempo de ejecución, el proveedor OLE DB de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client volverá a llamar al objeto de conjunto de filas para capturar las filas y leer los datos de columna.  
  
## <a name="see-also"></a>Vea también  
 [Parámetros con valores de tabla &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-table-valued-parameters/table-valued-parameters-ole-db.md)   
 [Usar parámetros con valores de tabla &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
