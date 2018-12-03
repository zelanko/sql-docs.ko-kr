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
ms.openlocfilehash: ea08f3b58894ff269972dc2348d71fb2d589959c
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52398201"
---
# <a name="valueof-method-javasqltimestamp-javautilcalendar"></a>valueOf 메서드(java.sql.Timestamp, java.util.Calendar)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  오프섹을 나타내는 java.sql.Timestamp 값과 java.util.Calendar 값이 지정된 경우 GMT를 기준으로 특정 오프셋의 시점을 나타내는 **DateTimeOffset** 개체를 만듭니다.  
  
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
  
  
