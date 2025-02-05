---
title: Crear una base de conocimiento | Microsoft Docs
ms.custom: ''
ms.date: 06/04/2013
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql13.dqs.kb.selectkb.f1
- sql13.dqs.kb.newkb.f1
ms.assetid: 2733a284-975f-4650-abcc-cc2aad074cab
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 0512f4b1dafb44384f99d4ed056bc4322c9b2513
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67935485"
---
# <a name="create-a-knowledge-base"></a>Crear una base de conocimiento

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  En este tema se describe cómo crear una base de conocimiento en [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) y cómo prepararla para la administración de dominios, la detección de conocimiento o la adición de una directiva de coincidencia.  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Prerequisites"></a> Requisitos previos  
 Para crear una base de conocimiento, debe tener instalado [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] y [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)].  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
 Para crear una base de conocimiento, debe disponer del rol dqs_kb_editor o dqs_administrator en la base de datos DQS_MAIN.  
  
##  <a name="Createaknowledgebase"></a> Create a knowledge base  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Ejecute la aplicación Data Quality Client](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  En la página de inicio de [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] , haga clic en **Nueva base de conocimiento**.  
  
3.  Escriba un nombre y una descripción para la nueva base de conocimiento.  
  
4.  En **Crear base de conocimiento a partir de**, seleccione en qué desea basar la base de conocimiento:  
  
    -   Seleccione **Ninguno** si no desea basar la nueva base de conocimiento en una base de conocimiento o un archivo de datos existente.  
  
    -   Seleccione **Base de conocimiento existente** para basar la nueva base de conocimiento en una base de conocimiento ya existente en [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)], o en la base de conocimiento predeterminada. Seleccione la base de conocimiento en la lista desplegable **Seleccionar la base de conocimiento** , o haga clic en **Examinar** para mostrar el cuadro de diálogo **Seleccione una base de conocimiento** , seleccione la base de conocimiento existente en la que desea basar la nueva y, a continuación, haga clic en **Aceptar**. Al seleccionar una base de conocimiento en la tabla, los dominios y las reglas de coincidencia de la base de conocimiento se mostrarán en el panel derecho del cuadro de diálogo. También puede seleccionar la base de conocimiento **Datos de DQS** , la base de conocimiento predeterminada que contiene dominios e información habituales relacionados con datos de empresas, direcciones y partidos de EE. UU.  
  
    -   Seleccione **Importar desde el archivo DQS** para basar la nueva base de conocimiento en un archivo DQS de [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)]. Haga clic en **Examinar**, seleccione un archivo de datos DQS con la extensión .dqs y, a continuación, haga clic en **Aceptar**.  
  
5.  En **Seleccione la actividad**, seleccione la actividad que desea realizar en la nueva base de conocimiento:  
  
    -   Seleccione **Administración de dominios** para crear la base de conocimiento y pasar a las pantallas que se utilizan para modificar los dominios de esta.  
  
    -   Seleccione **Detección de conocimiento** para crear la base de conocimiento e iniciar el asistente que se usa para analizar una muestra de datos y rellenar los dominios de la base de conocimiento con los resultados.  
  
    -   Seleccione **Directiva de coincidencia** para crear una directiva de coincidencia y agregarla a la base de conocimiento.  
  
6.  Haga clic en **Create**(Crear).  
  
##  <a name="FollowUp"></a> Seguimiento: después de crear una base de conocimiento  
 Una vez creada la base de conocimiento, aparecerá un asistente que podrá utilizar para realizar la detección de conocimiento, un asistente para crear una directiva de coincidencia o varias páginas que le permitirán realizar la administración de dominios. Para más información sobre la detección de conocimiento, la administración de dominios o la directiva de coincidencia, vea [Realizar la detección de conocimiento](../data-quality-services/perform-knowledge-discovery.md), [Administrar un dominio](../data-quality-services/managing-a-domain.md) o [Crear una directiva de coincidencia](../data-quality-services/create-a-matching-policy.md).  
  
  
