---
title: 'Tutorial: Asistente para la optimización de motor de base de datos | Microsoft Docs'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- Database Engine Tuning Advisor [SQL Server], tutorials
- tutorials [Database Engine Tuning Advisor]
ms.assetid: 3b54cbbe-d8c6-424d-92f1-aa58179f4da8
author: markingmyname
ms.author: maghan
ms.openlocfilehash: ab03ee7997014308e6753f463119a3a9adc8c963
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68105845"
---
# <a name="tutorial-database-engine-tuning-advisor"></a>Tutorial: Asistente para la optimización de motor de base de datos
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
Bienvenido al tutorial del Asistente para la optimización de motor de base de datos El Asistente para la optimización de motor de base de datos analiza la forma en que se procesan las consultas en las bases de datos especificadas por el usuario y, a continuación, recomienda la forma en que se puede mejorar el rendimiento del procesamiento modificando las estructuras de base de datos tales como índices, vistas indizadas y particiones.  
  
El Asistente para la optimización de motor de base de datos proporciona dos interfaces de usuario: una interfaz gráfica de usuario (GUI) y la utilidad del símbolo del sistema **dta** . La GUI facilita y agiliza la obtención de resultados a partir de las sesiones de optimización y la utilidad **dta** facilita la incorporación de la funcionalidad del Asistente para la optimización de motor de base de datos a los scripts con el fin de automatizar la optimización. Además, este asistente admite datos de entrada XML, lo que ofrece un mayor control sobre el proceso de optimización.  
  
## <a name="what-you-will-learn"></a>Aprendizaje  
Este tutorial le mostrará cómo navegar por la GUI del Asistente para la optimización de motor de base de datos y cómo realizar algunas tareas básicas tanto con la GUI como con la utilidad **dta** . Incluye las lecciones siguientes:  
  
[Lección 1: Navegación básica en el Asistente para la optimización de motor de base de datos](../../tools/dta/lesson-1-basic-navigation-in-database-engine-tuning-advisor.md)  
En esta lección, se familiarizará con la GUI del Asistente para la optimización de motor de base de datos y aprenderá a configurar las opciones de visualización y el diseño.  
  
[Lección 2: Usar el Asistente para la optimización de motor de base de datos](../../tools/dta/lesson-2-using-database-engine-tuning-advisor.md)  
En esta lección, aprenderá a realizar tareas básicas de optimización con la GUI del Asistente para la optimización de motor de base de datos.  
  
[Lección 3: Usar la utilidad del símbolo del sistema dta](../../tools/dta/lesson-3-using-the-dta-command-prompt-utility.md)  
En esta lección, aprenderá a iniciar la utilidad del símbolo del sistema **dta** y a ejecutar algunos comandos de optimización sencillos.  
  
## <a name="requirements"></a>Requisitos  
Este tutorial está destinado a los administradores de bases de datos que no están familiarizados con la GUI del Asistente para la optimización de motor de base de datos o la utilidad del símbolo del sistema **dta** , pero que tienen experiencia con las estructuras y los conceptos de bases de datos, como los índices y las vistas indizadas.  
  
Debe instalar [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] (o una versión posterior) con la base de datos de ejemplo [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] . Con el objeto de mejorar la seguridad, las bases de datos de ejemplo no se instalan de forma predeterminada. Para instalarlas, consulte [Instalar ejemplos de SQL Server y bases de datos de ejemplo](https://sqlserversamples.codeplex.com).  
  
## <a name="after-you-finish-this-tutorial"></a>Al finalizar este tutorial  
Cuando haya finalizado las lecciones de este tutorial, consulte los temas siguientes para obtener más información acerca del Asistente para la optimización de motor de base de datos:  
  
-   [Asistente para la optimización de motor de base de datos](../../relational-databases/performance/database-engine-tuning-advisor.md) para obtener descripciones sobre cómo realizar tareas con esta herramienta.  
  
-   [dta (utilidad)](../../tools/dta/dta-utility.md) para obtener material de referencia sobre la utilidad de símbolo del sistema y el archivo XML opcional que puede usar para controlar el funcionamiento de la utilidad.  
  
## <a name="next-lesson"></a>Lección siguiente  
[Lección 1: Navegación básica en el Asistente para la optimización de motor de base de datos](../../tools/dta/lesson-1-basic-navigation-in-database-engine-tuning-advisor.md)  
  
  
  
