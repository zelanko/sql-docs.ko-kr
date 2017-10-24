---
title: "함께 사용할 수 | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- RecordOpenOptionsEnum
helpviewer_keywords:
- RecordOpenOptionsEnum enumeration [ADO]
ms.assetid: 9028aba4-90fc-4dfc-88e4-fa8a7b6fedee
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 157b0683dc9d68e4fb00dce0d4a468fa5f622179
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="recordopenoptionsenum"></a>함께 사용할 수
열기에 대 한 옵션을 지정 된 [레코드](../../../ado/reference/ado-api/record-object-ado.md)합니다. 사용 하 여 이러한 값을 결합할 수 있습니다 또는 합니다.  
  
|상수|값|Description|  
|--------------|-----------|-----------------|  
|**adDelayFetchFields**|0x8000|필드와 연결 된 공급자에 게 알립니다는 **레코드** 처음 검색할 필요는 없지만 필드에 액세스 하는 첫 번째 시도에서 검색할 수 있습니다. 이 플래그가 없는 것으로 표시 된 기본 동작을 모두 검색 하는 것은 **레코드** 필드 개체입니다.|  
|**adDelayFetchStream**|0x4000|기본 스트림을 연결 된 공급자에 게 알립니다는 **레코드** 처음 검색할 필요 합니다. 이 플래그가 없는 것으로 표시 된 기본 동작을 연결 된 기본 스트림을 검색 하는 것은 **레코드** 개체입니다.|  
|**adOpenAsync**|0x1000|나타냅니다는 **레코드** 객체가 비동기 모드에서 열립니다.|  
|**adOpenExecuteCommand**|0x10000|소스 문자열에 실행할 명령 텍스트에 있음을 나타냅니다. 이 값은 해당 하는 **adCmdText** 옵션을 **Recordset.Open**합니다.|  
|**adOpenRecordUnspecified**|-1|기본. 옵션이 지정 되지 않은 것을 나타냅니다.|  
|**adOpenOutput**|0x800000|소스 실행 스크립트를 포함 하는 노드를 가리키는 경우 (예:는 합니다. ASP 페이지) 다음 열린 **레코드** 실행 된 스크립트의 결과가 포함 됩니다. 이 값은 컬렉션이 아닌 레코드를 사용 하 여 유효 합니다.|  
  
## <a name="adowfc-equivalent"></a>해당 하는 ADO/WFC  
 이러한 상수는 ADO/wfc 필요가 없습니다.  
  
## <a name="applies-to"></a>적용 대상  
 [Open 메서드(ADO 레코드)](../../../ado/reference/ado-api/open-method-ado-record.md)

