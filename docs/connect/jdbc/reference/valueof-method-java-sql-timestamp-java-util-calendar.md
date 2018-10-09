---
title: valueOf 메서드(java.sql.Timestamp, java.util.Calendar) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 7320c383-0b06-446d-963b-7005e50324a2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fd94495081d99521758747f174268d2163cf67e7
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47742741"
---
# <a name="valueof-method-javasqltimestamp-javautilcalendar"></a>valueOf 메서드(java.sql.Timestamp, java.util.Calendar)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 java.sql.Timestamp 값과 분 단위 오프셋을 나타내는 값을 사용하여 GMT를 기준으로 특정 오프셋의 시점을 나타내는 **DateTimeOffset** 개체를 만듭니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public static DateTimeOffset valueOf(java.sql.Timestamp timestamp, java.util.Calendar calendar)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *timestamp*  
  
 java.sql.Timestamp값입니다.  
  
 *calendar*  
  
 오프셋 값입니다.  날짜 및 시간 구성 요소 *달력* 에 따라 설정 됩니다는 *타임 스탬프* 값입니다.  
  
## <a name="return-value"></a>반환 값  
 시간 지정된 java.util.Calendar 개체의 표준 시간대에서 java.sql.Timestamp 개체로 지정 된 시점을 나타내는 DateTimeOffset 개체를 반환 합니다.  
  
## <a name="remarks"></a>Remarks  
 이 메서드는 또한 java.sql.Timestamp 개체로 지정 된 시점의 지점 java.util.Calendar 개체를 설정 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [DateTimeOffset 클래스](../../../connect/jdbc/reference/datetimeoffset-class.md)   
 [DateTimeOffset 멤버](../../../connect/jdbc/reference/datetimeoffset-members.md)  
  
  
