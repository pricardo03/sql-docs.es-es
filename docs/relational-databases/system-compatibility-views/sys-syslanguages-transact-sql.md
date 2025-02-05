---
title: Sys.syslanguages (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.syslanguages
- sys.syslanguages_TSQL
- syslanguages
- syslanguages_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- syslanguages system table
- sys.syslanguages compatibility view
ms.assetid: f216d1cd-997c-42f0-a737-abbdfcd88383
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 131cabc90680a9d1069802f4549c7c3754a78dec
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68053393"
---
# <a name="syssyslanguages-transact-sql"></a>sys.syslanguages (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Contiene una fila por cada idioma presente en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|langid|**smallint**|Id. de idioma único.|  
|dateformat|**nchar(3)**|Orden de la fecha (por ejemplo, DMA).|  
|datefirst|**tinyint**|Primer día de la semana: 1 para el lunes, 2 para el martes y así sucesivamente hasta 7 para el domingo.|  
|upgrade|**int**|Reservado para uso del sistema.|  
|name|**sysname**|Nombre de idioma oficial, por ejemplo, en francés.|  
|alias|**sysname**|Nombre alternativo del idioma (por ejemplo, francés).|  
|meses|**nvarchar(372)**|Lista separada por comas con los nombres completos de los meses, de enero a diciembre, en la que cada mes puede contener hasta 20 caracteres.|  
|shortmonths|**nvarchar(132)**|Lista separada por comas con los nombres cortos de los meses, de enero a diciembre, en la que cada mes puede contener hasta 9 caracteres.|  
|days|**nvarchar(217)**|Lista separada por comas con los nombres de los días, de lunes a domingo, en la que cada nombre puede contener hasta 30 caracteres.|  
|lcid|**int**|Id. de configuración regional de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows para el idioma.|  
|msglangid|**smallint**|Identificador del grupo de mensajes del [!INCLUDE[ssDE](../../includes/ssde-md.md)].|  
  
 El [!INCLUDE[ssDE](../../includes/ssde-md.md)] contiene los siguientes idiomas instalados.  
  
|Nombre en español|LCID de Windows|Id. de grupo de mensajes del [!INCLUDE[ssDE](../../includes/ssde-md.md)]|  
|---------------------|------------------|-----------------------------------------|  
|Inglés|3082|3082|  
|Alemán|1031|1031|  
|Francés|1036|1036|  
|Japonés|1041|1041|  
|Danish|1030|1030|  
|Español|3082|3082|  
|Italiano|1040|1040|  
|Neerlandés|1043|1043|  
|Noruego|2068|2068|  
|Portugués|2070|2070|  
|Finlandés|1035|1035|  
|Sueco|1053|1053|  
|Czech|1029|1029|  
|Húngaro|1038|1038|  
|Polaco|1045|1045|  
|Rumano|1048|1048|  
|Croata|1050|1050|  
|Eslovaco|1051|1051|  
|Esloveno|1060|1060|  
|Greek|1032|1032|  
|Búlgaro|1026|1026|  
|Ruso|1049|1049|  
|Turco|1055|1055|  
|British English|2057|3082|  
|Estonio|1061|1061|  
|Letón|1062|1062|  
|Lituano|1063|1063|  
|Portugués (Brasil)|1046|1046|  
|Chino tradicional|1028|1028|  
|Coreano|1042|1042|  
|Chino simplificado|2052|2052|  
|Árabe|1025|1025|  
|Tailandés|1054|1054|  
  
## <a name="see-also"></a>Vea también  
 [Vistas de compatibilidad &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)   
 [Asignar tablas del sistema a vistas del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)  
  
  
