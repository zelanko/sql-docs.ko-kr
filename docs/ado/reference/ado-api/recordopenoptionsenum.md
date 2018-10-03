---
title: 함께 사용할 수 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- RecordOpenOptionsEnum
helpviewer_keywords:
- RecordOpenOptionsEnum enumeration [ADO]
ms.assetid: 9028aba4-90fc-4dfc-88e4-fa8a7b6fedee
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ab648d7fe60a27d36e55cd3d859d0a8c442eef50
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47644816"
---
# <a name="recordopenoptionsenum"></a>RecordOpenOptionsEnum
열기에 대 한 옵션을 지정 하는 [레코드](../../../ado/reference/ado-api/record-object-ado.md)합니다. 이러한 값을 사용 하 여 결합할 수 있습니다 또는 합니다.  
  
|상수|값|Description|  
|--------------|-----------|-----------------|  
|**adDelayFetchFields**|0x8000|필드와 연결 공급자에 게 나타내는 합니다 **레코드** 처음에 검색할 필요는 없지만 필드에 액세스 하는 첫 번째 시도에서 검색할 수 있습니다. 이 플래그가 없는 것으로 표시 된 기본 동작을 모두 검색 하는 것은 **레코드** 필드 개체입니다.|  
|**adDelayFetchStream**|0x4000|기본 스트림에 연결 된 공급자에 게 알립니다 합니다 **레코드** 처음 검색할 필요 합니다. 이 플래그가 없는 것으로 표시 된 기본 동작을 연결 된 기본 스트림을 검색 하는 것은 **레코드** 개체입니다.|  
|**adOpenAsync**|0x1000|나타내는 합니다 **레코드** 개체는 비동기 모드로 열립니다.|  
|**adOpenExecuteCommand**|0x10000|소스 문자열 실행 되어야 하는 명령 텍스트가 포함 됨을 나타냅니다. 이 값은 동일 합니다 **adCmdText** 옵션을 **Recordset.Open**합니다.|  
|**adOpenRecordUnspecified**|-1|기본. 옵션이 지정 되지 않은 것을 나타냅니다.|  
|**adOpenOutput**|0x800000|소스는 실행 가능한 스크립트를 포함 하는 노드를 가리키는 경우 (예는. ASP 페이지의 경우) 다음 열린 **레코드** 실행된 된 스크립트의 결과가 포함 됩니다. 이 값 컬렉션이 아닌 레코드를 사용 하 여만 유효합니다.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 해당  
 이러한 상수는 ADO/wfc 필요가 없습니다.  
  
## <a name="applies-to"></a>적용 대상  
 [Open 메서드(ADO 레코드)](../../../ado/reference/ado-api/open-method-ado-record.md)
