---
title: Stream (Visual c + + 구문에 대 한 ADO) | Microsoft Docs
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
- Stream collection [ADO]
ms.assetid: dddcceef-9296-4fb3-8eca-94b17d0148de
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 77da08e1d6ead2ad5777f41113a1ed164a7fb5da
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47715751"
---
# <a name="stream-ado-for-visual-c-syntax"></a>스트림(Visual C++ 구문에 대한 ADO)
## <a name="methods"></a>메서드  
  
```  
Cancel(void)  
Close(void)  
CopyTo(_ADOStream *DestStream, LONG CharNumber = -1)  
Flush(void)  
LoadFromFile(BSTR FileName)  
Open(VARIANT Source, ConnectModeEnum Mode, StreamOpenOptionsEnum Options, BSTR UserName, BSTR Password)  
Read(long NumBytes, VARIANT *pVal)  
ReadText(long NumChars, BSTR *pbstr)  
SaveToFile(BSTR FileName, SaveOptionsEnum Options = adSaveCreateNotExist)  
SetEOS(void)  
SkipLine(void)  
Write(VARIANT Buffer)  
WriteText(BSTR Data, StreamWriteEnum Options = adWriteChar)  
```  
  
## <a name="properties"></a>속성  
  
```  
get_Charset(BSTR *pbstrCharset)  
put_Charset(BSTR Charset)  
get_EOS(VARIANT_BOOL *pEOS)  
get_LineSeparator(LineSeparatorEnum *pLS)  
put_LineSeparator(LineSeparatorEnum LineSeparator)  
get_Mode(ConnectModeEnum *pMode)  
put_Mode(ConnectModeEnum Mode)  
get_Position(LONG *pPos)  
put_Position(LONG Position)  
get_Size(LONG *pSize)  
get_State(ObjectStateEnum *pState)  
get_Type(StreamTypeEnum *pType)  
put_Type(StreamTypeEnum Type)  
```  
  
## <a name="see-also"></a>관련 항목  
 [스트림 개체(ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
