---
title: 명령 (Visual c + + 구문에 대 한 ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
dev_langs:
- C++
helpviewer_keywords:
- Command collection [ADO], ADO for Visual C++ syntax
ms.assetid: cf12cbd1-25f7-4bb5-aa94-0fe823b3b6d6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1c97a8495b1877c8c72dcacba25943c04934abca
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47851101"
---
# <a name="command-ado-for-visual-c-syntax"></a>명령(Visual C++ 구문에 대한 ADO)
## <a name="methods"></a>메서드  
  
```  
Cancel(void)  
CreateParameter(BSTR Name, DataTypeEnum Type, ParameterDirectionEnum Direction, long Size, VARIANT Value, _ADOParameter **ppiprm)  
Execute(VARIANT *RecordsAffected, VARIANT *Parameters, long Options, _ADORecordset **ppirs)  
```  
  
## <a name="properties"></a>속성  
  
```  
get_ActiveConnection(_ADOConnection **ppvObject)  
put_ActiveConnection(VARIANT vConn)  
putref_ActiveConnection(_ADOConnection *pCon)  
get_CommandText(BSTR *pbstr)  
put_CommandText(BSTR bstr)  
get_CommandTimeout(LONG *pl)  
put_CommandTimeout(LONG Timeout)  
get_CommandType(CommandTypeEnum *plCmdType)  
put_CommandType(CommandTypeEnum lCmdType)  
get_Name(BSTR *pbstrName)  
put_Name(BSTR bstrName)  
get_Prepared(VARIANT_BOOL *pfPrepared)  
put_Prepared(VARIANT_BOOL fPrepared)  
get_State(LONG *plObjState)  
get_Parameters(ADOParameters **ppvObject)  
```  
  
## <a name="see-also"></a>관련 항목  
 [명령 개체(ADO)](../../../ado/reference/ado-api/command-object-ado.md)
