---
title: Identificadores (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 1f72832fd684dd59e27ce58576a7f65fa8796347
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68074811"
---
# <a name="identifiers-dmx"></a>Identificadores (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Todos los objetos de [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] debe tener un identificador. El nombre del objeto es su identificador. Servidores, bases de datos y objetos de base de datos como orígenes de datos, vistas del origen de datos, cubos, dimensiones, modelos de minería de datos etc. tienen identificadores.  
  
 Existen dos clases de identificadores en Extensiones de minería de datos (DMX):  
  
-   [Identificadores normales](#RegularIdentifiers)  
  
-   [Identificadores delimitados](#DelimitedIdentifiers)  
  
 El identificador de un objeto se crea cuando se define el objeto. Así puede utilizar el identificador para hacer referencia al objeto. Los identificadores pueden tener 100 caracteres como máximo.  
  
##  <a name="RegularIdentifiers"></a> Identificadores normales  
 Los identificadores normales de DMX siguen las reglas de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] respecto al formato de identificadores. Los identificadores normales de DMX no requieren delimitadores. Este es un ejemplo de una instrucción DMX que utiliza un identificador normal no delimitado:  
  
```  
SELECT * FROM Clustering.CONTENT;  
```  
  
### <a name="rules-for-regular-identifiers"></a>Reglas de los identificadores normales  
 A continuación, figuran las reglas de formato de los identificadores normales:  
  
1.  El primer carácter de un identificador normal debe ser uno de los siguientes:  
  
    -   Una letra, como se define en el estándar Unicode 2.0. Incluye los caracteres latinos de la "a" a la "z" y de la "A" a la "Z", además de los caracteres de letras de otros idiomas.  
  
    -   Un carácter de subrayado (_).  
  
2.  Los caracteres siguientes pueden ser:  
  
    -   Letras, tal como se define en el estándar Unicode 2.0.  
  
    -   Números decimales del alfabeto Latín básico u otros alfabetos de otros idiomas.  
  
    -   Un carácter de subrayado (_).  
  
3.  El identificador no debe ser una palabra reservada de DMX. En las palabras reservadas de DMX, no se distinguen mayúsculas de minúsculas. Para obtener más información, consulte [palabras clave reservadas &#40;DMX&#41;](../dmx/reserved-keywords-dmx.md).  
  
4.  El identificador no puede contener espacios o caracteres especiales incrustados.  
  
 Deberá escribir entre corchetes los identificadores que no sigan estas reglas cuando los emplee en instrucciones DMX.  
  
##  <a name="DelimitedIdentifiers"></a> Identificadores delimitados  
 Los identificadores delimitados se escriben entre corchetes ([ ]).  A continuación, figura un ejemplo de una instrucción DMX que utiliza un identificador delimitado que sigue las reglas.  
  
```  
SELECT * FROM [Marketing_Clusters].CONTENT;  
```  
  
 Si un identificador no sigue las reglas de formato de los identificadores normales, debe aparecer siempre delimitado. A continuación, figura un ejemplo de una instrucción DMX con un identificador delimitado que contiene un espacio:  
  
```  
SELECT * FROM [Targeted Mailing].CONTENT;  
```  
  
 Los identificadores delimitados se emplean en estas situaciones:  
  
-   Cuando utilice palabras reservadas en los nombres de objeto o partes de nombres de objeto.  
  
     Se recomienda evitar el uso de palabras clave reservadas en los nombres de objeto. Las bases de datos que se actualizan desde versiones anteriores de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] podrían contener identificadores que incluyan palabras que no estaban reservadas en la versión anterior de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , pero que son palabras reservadas para[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Puede hacer referencia al objeto con identificadores delimitados hasta que se pueda cambiar el nombre.  
  
-   Cuando utilice caracteres no considerados como identificadores aceptados.  
  
     [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] permite que se utilice cualquier carácter de la página de códigos actual en identificadores delimitados; no obstante, el uso indiscriminado de caracteres especiales en un nombre de objeto puede dificultar la lectura y el mantenimiento de las instrucciones DMX.  
  
### <a name="rules-for-delimited-identifiers"></a>Reglas para los identificadores delimitados  
 A continuación, figuran las reglas de formato de los identificadores delimitados:  
  
1.  Los identificadores delimitados pueden contener el mismo número de caracteres que los identificadores normales (de 1 a 100 caracteres, sin incluir los caracteres delimitadores).  
  
2.  La parte de cuerpo del identificador puede contener cualquier combinación de caracteres de la página actual de códigos, incluidos los propios caracteres delimitadores. Si el propio cuerpo del identificador contiene caracteres delimitadores, será necesario un tratamiento especial:  
  
    -   Si el cuerpo del identificador contiene un corchete de apertura ([), no se requiere ninguna manipulación.  
  
    -   Si el cuerpo del identificador contiene un corchete de cierre (]), deberá especificar dos corchetes de cierre (]]) para representarlo en la página de códigos.  
  
### <a name="delimiting-identifiers-with-multiple-parts"></a>Delimitar identificadores con varias partes  
 Cuando se utilizan nombres de objetos completos, podría ser necesario delimitar varios de los identificadores que componen el nombre de objeto. Deberá delimitar cada uno de ellos por separado.  
  
## <a name="see-also"></a>Vea también  
 [Referencia de Extensiones de minería de datos &#40;DMX&#41;](../dmx/data-mining-extensions-dmx-reference.md)   
 [Extensiones de minería de datos &#40;DMX&#41; elementos de sintaxis](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Extensiones de minería de datos &#40;DMX&#41; referencia de funciones](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Extensiones de minería de datos &#40;DMX&#41; referencia de operadores](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Extensiones de minería de datos &#40;DMX&#41; referencia de instrucciones](../dmx/data-mining-extensions-dmx-statements.md)   
 [Extensiones de minería de datos &#40;DMX&#41; convenciones de sintaxis](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Funciones de predicción generales &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [Estructura y uso de las consultas de predicción DMX](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [Descripción de la instrucción Select de DMX](../dmx/understanding-the-dmx-select-statement.md)  
  
  
