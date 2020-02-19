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
ms.openlocfilehash: 11d8f8e346fdb0f07770feec815e5aa5fe88355f
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "68001589"
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
  
 오프셋 값입니다.  *calendar*의 날짜 및 시간 구성 요소는 *timestamp* 값에 따라 설정됩니다.  
  
## <a name="return-value"></a>Return Value  
 정해진 java.util.Calendar 개체의 표준 시간대에 java.sql.Timestamp 개체에서 주어진 시점을 나타내는 DateTimeOffset 개체가 반환됩니다.  
  
## <a name="remarks"></a>설명  
 이 메서드는 java.util.Calendar 개체를 java.sql.Timestamp 개체에서 주어진 시점으로도 설정합니다.  
  
## <a name="see-also"></a>참고 항목  
 [DateTimeOffset 클래스](../../../connect/jdbc/reference/datetimeoffset-class.md)   
 [DateTimeOffset 멤버](../../../connect/jdbc/reference/datetimeoffset-members.md)  
  
  
