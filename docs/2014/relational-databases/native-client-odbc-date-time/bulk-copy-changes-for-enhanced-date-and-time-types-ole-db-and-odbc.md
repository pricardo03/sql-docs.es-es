---
title: Cambios en la copia de forma masiva para mejorada tipos de fecha y hora (OLE DB y ODBC) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC, bulk copy operations
- bulk copy [ODBC], changes for date/time improvements
ms.assetid: c29e0f5e-9b3c-42b3-9856-755f4510832f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 855d0baf0b0b890b9343378f8060919979d5f206
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63207106"
---
# <a name="bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc"></a>Cambios de copia masiva para tipos de fecha y hora mejorados (OLE DB y ODBC)
  En este tema se describen las mejoras de fecha y hora efectuadas para admitir la funcionalidad de copia masiva. La información de este tema es válida para OLE DB y ODBC en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
## <a name="format-files"></a>Archivos de formato  
 En la tabla siguiente se describe la entrada que se usa para especificar los tipos de fecha y hora, así como los nombres de tipo de datos de archivo host correspondientes, a la hora de generar archivos de formato de forma interactiva.  
  
|tipo de almacenamiento en archivo|Tipo de datos del archivo host|Respuesta a la pregunta: "Especifique el tipo de almacenamiento de archivo del campo < field_name > [\<predeterminado >]:"|  
|-----------------------|-------------------------|-----------------------------------------------------------------------------------------------------|  
|DateTime|SQLDATETIME|d|  
|Smalldatetime|SQLDATETIM4|D|  
|date|SQLDATE|de|  
|Time|SQLTIME|te|  
|Datetime2|SQLDATETIME2|d2|  
|Datetimeoffset|SQLDATETIMEOFFSET|do|  
  
 El archivo XSD con formato XML tendrá las siguientes adiciones:  
  
```  
<xs:complexType name="SQLDATETIME2">  
    <xs:complexContent>  
        <xs:extension base="bl:Fixed"/>  
    </xs:complexContent>  
</xs:complexType>  
<xs:complexType name="SQLDATETIMEOFFSET">  
    <xs:complexContent>  
        <xs:extension base="bl:Fixed"/>  
    </xs:complexContent>  
</xs:complexType>  
<xs:complexType name="SQLDATE">  
    <xs:complexContent>  
        <xs:extension base="bl:Fixed"/>  
    </xs:complexContent>  
</xs:complexType>  
<xs:complexType name="SQLTIME">  
    <xs:complexContent>  
        <xs:extension base="bl:Fixed"/>  
    </xs:complexContent>  
</xs:complexType>  
```  
  
## <a name="character-data-files"></a>Archivos de datos de caracteres  
 En los archivos de datos de caracteres, los valores de fecha y hora se representan como se describe en la "formatos de datos: Sección de cadenas y literales"de [compatibilidad con tipos de datos de ODBC mejoras de fecha y hora](data-type-support-for-odbc-date-and-time-improvements.md) para ODBC o de [compatibilidad con tipos de datos para OLE DB mejoras de fecha y hora](../native-client-ole-db-date-time/data-type-support-for-ole-db-date-and-time-improvements.md) para OLE DB.  
  
 En los archivos de datos nativos, los valores de fecha y hora para los cuatro nuevos tipos se representan como sus representaciones TDS con una escala de 7 (dado que se trata del máximo admitido por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y archivos de datos bcp no almacenan la escala de estas columnas). No hay ningún cambio en el almacenamiento de la existente `datetime` y `smalldatetime` sus datos tabulares o tipo transmitir representaciones (TDS).  
  
 Los tamaños de almacenamiento para los distintos tipos de almacenamiento son los siguientes para OLE DB:  
  
|tipo de almacenamiento en archivo|Tamaño de almacenamiento en bytes|  
|-----------------------|---------------------------|  
|datetime|8|  
|smalldatetime|4|  
|date|3|  
|time|6|  
|datetime2|9|  
|datetimeoffset|11|  
  
 Las tamaños de ODBC son los siguientes. Tenga en cuenta que no es necesario almacenar la precisión en archivos de datos o de formato porque BCP.exe siempre recuperará la precisión del servidor.  
  
|tipo de almacenamiento en archivo|Tamaño de almacenamiento en bytes|Formato de almacenamiento|  
|-----------------------|---------------------------|--------------------|  
|datetime (d)|8|TDS|  
|smalldatetime (D)|4|TDS|  
|date (de)|3|TDS|  
|time (te)|6|TDS|  
|datetime2 (d2)|9|TDS|  
|datetimeoffset (do)|11|TDS|  
  
## <a name="bcp-types-in-sqlnclih"></a>Tipos BCP en sqlncli.h  
 Los tipos siguientes se definen en sqlncli.h para usarse con las extensiones API de BCP en ODBC. Estos tipos se pasan con el *eUserDataType* parámetro de ibcpsession:: BCPColFmt en OLE DB.  
  
|tipo de almacenamiento en archivo|Tipo de datos del archivo host|Tipo de sqlncli.h para su uso con ibcpsession:: BCPColFmt|Valor|  
|-----------------------|-------------------------|-----------------------------------------------------------|-----------|  
|DateTime|SQLDATETIME|BCP_TYPE_SQLDATETIME|0x3d|  
|Smalldatetime|SQLDATETIM4|BCP_TYPE_SQLDATETIME4|0x3a|  
|date|SQLDATE|BCP_TYPE_SQLDATE|0x28|  
|Time|SQLTIME|BCP_TYPE_SQLTIME|0x29|  
|Datetime2|SQLDATETIME2|BCP_TYPE_SQLDATETIME2|0x2a|  
|Datetimeoffset|SQLDATETIMEOFFSET|BCP_TYPE_SQLDATETIMEOFFSET|0x2b|  
  
## <a name="bcp-data-type-conversions"></a>Conversiones de tipos de datos BCP  
 En las tablas siguientes se proporciona información de conversión.  
  
 **Nota de OLE DB** Las conversiones siguientes se realizan con IBCPSession. IRowsetFastLoad usa conversiones OLE DB, tal como se define en [conversiones realizadas de cliente a servidor](../native-client-ole-db-date-time/conversions-performed-from-client-to-server.md). Tenga en cuenta que los valores datetime se redondean a la fracción 1/300 de segundo y los valores smalldatetime tienen los segundos establecidos en cero después de que se hayan realizado las conversiones de cliente que se describen a continuación. El redondeo de datetime se propaga a las horas y minutos, pero no a la fecha.  
  
|A--><br /><br /> De|date|time|smalldatetime|datetime|datetime2|datetimeoffset|char|wchar|  
|------------------------|----------|----------|-------------------|--------------|---------------|--------------------|----------|-----------|  
|date|1|-|1,6|1,6|1,6|1,5,6|1,3|1,3|  
|Time|N/D|1,10|1,7,10|1,7,10|1,7,10|1,5,7,10|1,3|1,3|  
|Smalldatetime|1,2|1,4,10|1|1|1,10|1,5,10|1,11|1,11|  
|DateTime|1,2|1,4,10|1,12|1|1,10|1,5,10|1,11|1,11|  
|Datetime2|1,2|1,4,10|1,10 (ODBC)1,12 (OLE DB)|1,10|1,10|1,5,10|1,3|1,3|  
|Datetimeoffset|1,2,8|1,4,8,10|1,8,10|1,8,10|1,8,10|1,10|1,3|1,3|  
|Char/wchar (date)|9|-|9,6 (ODBC)9,6,12 (OLE DB)|9,6 (ODBC)9,6,12 (OLE DB)|9,6|9,5,6|N/D|N/D|  
|Char/wchar (time)|-|9,10|9,7,10 (ODBC)9,7,10,12 (OLE DB)|9,7,10 (ODBC)9,7,10, 12 (OLE DB)|9,7,10|9,5,7,10|N/D|N/D|  
|Char/wchar (datetime)|9,2|9,4,10|9,10 (ODBC)9,10,12 (OLE DB)|9,10 (ODBC)9,10,12 (OLE DB)|9,10|9,5,10|N/D|N/D|  
|Char/wchar (datetimeoffset)|9,2,8|9,4,8,10|9,8,10 (ODBC)9,8,10,12 (OLE DB)|9,8,10 (ODBC)9,8,10,12 (OLE DB)|9,8,10|9,10|N/D|N/D|  
  
#### <a name="key-to-symbols"></a>Clave de los símbolos  
  
|Símbolo|Significado|  
|------------|-------------|  
|-|No se admite la conversión.<br /><br /> Se genera un registro de diagnóstico ODBC con SQLSTATE 07006 y el mensaje "Infracción del atributo de tipo de datos restringido".|  
|1|Si los datos proporcionados no son válidos, se genera un registro de diagnóstico ODBC con SQLSTATE 22007 y el mensaje "Formato de fecha y hora no válido". Para los valores datetimeoffset, el espacio de tiempo debe estar comprendido dentro del intervalo después de la conversión a UTC, aunque no se haya solicitado ninguna conversión a UTC. Esto se debe a que la secuencia de datos tabulares (TDS) y el servidor siempre normalizan el tiempo en valores datetimeoffset para UTC. Por lo tanto, el cliente debe comprobar que los componentes de tiempo se encuentran dentro del intervalo admitido después de la conversión a UTC.|  
|2|Se omite el componente de hora.|  
|3|Para ODBC, si se produce un truncamiento con pérdida de datos, se genera un registro de diagnóstico con SQLSTATE 22001 y el mensaje 'Datos de cadena, truncados derecha' se determina el número de dígitos de fracciones de segundo (la escala) de tamaño de la columna de destino según el tabla siguiente. Si el tamaño de las columnas es mayor que el intervalo de la tabla, se presupone una escala de 7. Esta conversión debería permitir hasta nueve dígitos en las fracciones de segundo, que es el máximo permitido por ODBC.<br /><br /> **Tipo:** DBTIME2<br /><br /> **Escala supuesta 0** 8<br /><br /> **Escala supuesta 1.. 7** 10,16<br /><br /> <br /><br /> **Tipo:** DBTIMESTAMP<br /><br /> **Escala supuesta 0:** 19<br /><br /> **Escala supuesta 1.. 7:** 21..27<br /><br /> <br /><br /> **Tipo:** DBTIMESTAMPOFFSET<br /><br /> **Escala supuesta 0:** 26<br /><br /> **Escala supuesta 1.. 7:** 28..34<br /><br /> Para OLE DB, si se produce un truncamiento con pérdida de datos, se expone un error. Para datetime2, el número de dígitos de fracciones de segundo (la escala) se determina a partir de tamaño de la columna de destino según la tabla siguiente. Si el tamaño de la columna es mayor que el intervalo de la tabla, se presupone una escala de 9. Esta conversión debería permitir hasta nueve dígitos en las fracciones de segundo, que es el máximo permitido por OLE DB.<br /><br /> **Tipo:** DBTIME2<br /><br /> **Escala supuesta 0** 8<br /><br /> **Escala supuesta 1..9** 1..9<br /><br /> <br /><br /> **Tipo:** DBTIMESTAMP<br /><br /> **Escala supuesta 0:** 19<br /><br /> **Escala supuesta 1.. 9:** 21..29<br /><br /> <br /><br /> **Tipo:** DBTIMESTAMPOFFSET<br /><br /> **Escala supuesta 0:** 26<br /><br /> **Escala supuesta 1.. 9:** 28..36|  
|4|Se omite el componente de fecha.|  
|5|Timezone se establece en UTC (por ejemplo, 00:00).|  
|6|La hora se establece en cero.|  
|7|La fecha se establece en 1900-01-01.|  
|8|Se omite el desplazamiento de zona horaria.|  
|9|La cadena se analiza y se convierte en un valor date, datetime, datetimeoffset o time, en función del primer carácter de puntuación encontrado y de la presencia de otros componentes. A continuación, la cadena se convierte en el tipo de destino, siguiendo las reglas de la tabla del final de este tema para el tipo de origen detectado por este proceso. Si los datos proporcionados no pueden analizarse sin errores, o si cualquier parte de componente se encuentra fuera del intervalo permitido, o si no hay ninguna conversión del tipo literal al tipo de destino, se expone un error (OLE DB) o se genera un registro de diagnóstico ODBC con SQLSTATE 22018 y el mensaje "Valor de carácter no válido para especificación cast". Para los parámetros datetime y smalldatetime, si el año se encuentra fuera del intervalo que estos tipos admiten, se expone un error (OLE DB) o un registro de diagnóstico ODBC con SQLSATE 22007 y el mensaje "Formato de fecha y hora no válido".<br /><br /> Para datetimeoffset, el valor debe estar comprendido dentro del intervalo después de la conversión a UTC, aunque no se haya solicitado ninguna conversión a UTC. Esto se debe a que la secuencia de datos tabulares (TDS) y el servidor siempre normalizan la hora en valores datetimeoffset para UTC, de modo que el cliente tenga que comprobar que los componentes de hora están dentro del intervalo admitido después de la conversión a UTC. Si el valor no se encuentra dentro del intervalo UTC compatible, se expone un error (OLE DB) o se genera un registro de diagnóstico ODBC con SQLSTATE 22007 y el mensaje "Formato de fecha y hora no válido".|  
|10|Si se produce un truncamiento con pérdida de datos en una conversión de cliente a servidor, se expone un error (OLE DB) o se genera un registro de diagnóstico ODBC con SQLSTATE 22008 y el mensaje "Desbordamiento del campo DateTime". Este error también se produce si el valor está fuera del intervalo que puede representarse mediante el intervalo UTC utilizado por el servidor. Si se produce un truncamiento de segundos o fracciones de segundo en una conversión de servidor a cliente, solo se emite una advertencia.|  
|11|Si se produce un truncamiento con pérdida de datos, se genera un registro de diagnóstico.<br /><br /> En una conversión de servidor a cliente, es una advertencia (ODBC SQLSTATE S1000).<br /><br /> En una conversión de cliente a servidor, es un error (ODBC SQLSTATE 22001).|  
|12|Los segundos se establecen en cero y las fracciones de segundo se descartan. No es posible ningún error de truncamiento.|  
|N/D|Se mantiene el comportamiento de las versiones actuales y anteriores de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].|  
  
## <a name="see-also"></a>Vea también  
 [Mejoras de fecha y hora &#40;ODBC&#41;](date-and-time-improvements-odbc.md)   
 [Mejoras de fecha y hora &#40;OLE DB&#41;](../native-client-ole-db-date-time/date-and-time-improvements-ole-db.md)  
  
  
