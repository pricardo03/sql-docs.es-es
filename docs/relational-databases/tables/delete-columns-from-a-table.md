---
title: Eliminación de columnas desde una tabla (motor de base de datos) | Microsoft Docs
ms.custom: ''
ms.date: 04/11/2017
ms.prod: sql
ms.prod_service: table-view-index, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- columns [SQL Server], deleting
- removing columns
- deleting columns
- dropping columns
ms.assetid: 0d8f6e4f-bc71-4fa3-8615-74249c8e072d
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0db1834114a8bb2ea21d9fb566f2201dd933803c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68088466"
---
# <a name="delete-columns-from-a-table"></a>Eliminar columnas de una tabla

[!INCLUDE[tsql-appliesto-ss2016-all-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

En este tema se describe cómo eliminar columnas de tabla en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].

> [!CAUTION]
> Cuando se elimina una columna de una tabla, se eliminan esta columna y todos los datos que contiene.

 **En este tema**

- **Antes de empezar:**

   [Limitaciones y restricciones](#Restrictions)

   [Seguridad](#Security)

- **Para eliminar una columna de una tabla con:**

   [SQL Server Management Studio](#SSMSProcedure)

   [Transact-SQL](#TsqlProcedure)

## <a name="BeforeYouBegin"></a> Antes de comenzar

### <a name="Restrictions"></a> Limitaciones y restricciones

No puede eliminar una columna que tenga una restricción CHECK. Primero debe eliminar la restricción.

No puede eliminar una columna que tiene restricciones PRIMARY KEY o FOREIGN KEY u otras dependencias excepto si usa el Diseñador de tablas. Al utilizar el Explorador de objetos o [!INCLUDE[tsql](../../includes/tsql-md.md)], primero debe quitar todas las dependencias de la columna.

### <a name="Security"></a> Seguridad

#### <a name="Permissions"></a> Permisos

Requiere el permiso ALTER en la tabla.

## <a name="SSMSProcedure"></a> Uso de SQL Server Management Studio

### <a name="to-delete-columns-by-using-object-explorer"></a>Para eliminar columnas mediante el Explorador de objetos

1. En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)].
2. En el **Explorador de objetos**, busque la tabla de la que quiere eliminar columnas y expanda los nombres de esas columnas para exponerlas.
3. Haga clic con el botón derecho en la columna que quiera eliminar y, después, elija **Eliminar**.
4. En el cuadro de diálogo **Eliminar objeto** , haga clic en **Aceptar**.

Si la columna contiene restricciones u otras dependencias, aparecerá un mensaje de error en el cuadro de diálogo **Eliminar objeto** . Resuelva el error eliminando las restricciones a las que hace referencia.

### <a name="to-delete-columns-by-using-table-designer"></a>Para eliminar columnas mediante el Diseñador de tablas

1. En el **Explorador de objetos**, haga clic con el botón derecho en la tabla de la que quiere eliminar columnas y elija **Diseño**.
2. Haga clic con el botón derecho en la columna que quiera eliminar y elija **Eliminar columna** en el menú contextual.
3. Si la columna participa en una relación (FOREIGN KEY o PRIMARY KEY), un cuadro de mensaje le pedirá que confirme la eliminación de las columnas seleccionadas y sus relaciones. Elija **Sí**.

## <a name="TsqlProcedure"></a> Usar Transact-SQL

### <a name="to-delete-columns"></a>Para eliminar columnas

En el ejemplo siguiente se muestra cómo eliminar una columna.

```sql
ALTER TABLE dbo.doc_exb DROP COLUMN column_b;
```

Si la columna contiene restricciones u otras dependencias, se devolverá un mensaje de error. Resuelva el error eliminando las restricciones a las que hace referencia.

Para obtener otros ejemplos, vea [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md).

## <a name="FollowUp"></a>
