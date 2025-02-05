---
title: Nueva programación compartida (Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.swb.reportserver.newschedule.f1
ms.assetid: b2c69586-d98e-4933-827d-f5e6c15c5203
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 083fa7998e347b3aa3abe7aacbf9585a18047b20
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66100225"
---
# <a name="new-shared-schedule-management-studio"></a>Nuevo Programación compartida (Management Studio)
  Use esta página para crear una programación compartida para ejecutar suscripciones e informes publicados. Las programaciones compartidas se pueden utilizar en lugar de las programaciones específicas del informe o de la suscripción. La información de programación centralizada y la capacidad de pausar y reanudar las operaciones programadas son dos características clave que distinguen las programaciones compartidas de las programaciones específicas de elemento.  
  
 Una sola programación no admite todas las combinaciones de frecuencias. Por ejemplo, si desea ejecutar un informe todos los viernes a las 12:00 p. m. y a las 4:00 p. m. debe crear dos programaciones diarias que especifiquen una fecha de ejecución en viernes, una con las 12:00 p. m. como hora de inicio y otra con las 4:00 p. m. como hora de inicio.  
  
 El procesamiento de programaciones se basa en la hora local del servidor de informes que hospeda y procesa la programación.  
  
 Para abrir esta página, inicie [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conéctese a un servidor de informes, haga clic con el botón derecho en **Programación compartida**y seleccione **Nueva programación**. Para guardar la programación, se debe estar ejecutando el servicio del Agente SQL Server.  
  
> [!NOTE]  
>  Esta característica no está disponible en todas las ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para una lista de las características admitidas por las ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [Características compatibles con las ediciones de SQL Server 2012](https://go.microsoft.com/fwlink/?linkid=232473) (https://go.microsoft.com/fwlink/?linkid=232473).  
  
## <a name="options"></a>Opciones  
 **Name**  
 Permite escribir el nombre de la programación compartida. Este nombre aparece en listas desplegables cuando los usuarios seleccionan una programación compartida para informes y suscripciones. Asegúrese de proporcionar un nombre descriptivo que se ajuste con facilidad dentro de una lista y que distinga con facilidad una programación compartida de otra. El nombre debe incluir al menos un carácter alfanumérico. También puede incluir espacios y algunos símbolos. No utilice los caracteres siguientes al especificar un nombre:  
  
 ; ? : \@ & = + , $ / * \< >  
  
 " /  
  
 **Empezar a ejecutar esta programación el**  
 Permite especificar la fecha de inicio de esta programación.  
  
 **Detener esta programación el**  
 Permite especificar la fecha de expiración de esta programación.  
  
 **Tipo**  
 Especifica si el patrón de periodicidad se basa principalmente en las horas, los días, las semanas o los meses.  
  
 **Hora (patrón de periodicidad)**  
 Permite seleccionar las opciones correspondientes para ejecutar una operación programada en intervalos de horas (por ejemplo, ejecutar un informe cada 6 horas). Puede especificar el intervalo en horas y minutos.  
  
 **Día (patrón de periodicidad)**  
 Permite seleccionar las opciones correspondientes para ejecutar una operación programada en intervalos de días (por ejemplo, ejecutar un informe cada 2 días). Puede especificar el intervalo en días y a la hora y minutos en los que desea que se ejecute la programación.  
  
 **Semana (patrón de periodicidad)**  
 Permite seleccionar las opciones correspondientes para ejecutar una operación programada en intervalos de semanas o cuando el patrón que desea que se repita se base en semanas (por ejemplo, ejecutar un informe cada semana). Puede especificar una programación semanal para el día, hora y minuto en los que desea que se ejecute la programación.  
  
 **Mes (patrón de periodicidad)**  
 Permite seleccionar las opciones correspondientes para ejecutar una operación programada en intervalos de meses o cuando el patrón que desea que se repita se base en meses. Puede especificar una programación mensual para el día, hora y minuto en los que desea que se ejecute la programación. Puede quitar meses específicos de la programación.  
  
 **Una vez**  
 Seleccione esta opción para crear una programación que se ejecute una sola vez o en una fecha y hora específicas.  
  
## <a name="see-also"></a>Vea también  
 [Servidor de informes en Management Studio ayuda F1](report-server-in-management-studio-f1-help.md)   
 [Conectar con un servidor de informes en Management Studio](connect-to-a-report-server-in-management-studio.md)   
 [Crear, modificar y eliminar programaciones](../subscriptions/create-modify-and-delete-schedules.md)   
 [Programaciones](../subscriptions/schedules.md)   
 [Servidor de informes en Management Studio (Ayuda F1)](report-server-in-management-studio-f1-help.md)  
  
  
