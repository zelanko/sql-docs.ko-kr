---
title: valueOf 메서드 (java.sql.Timestamp, int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 114f55af-62ab-4c60-8724-0affbbbbbcdc
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 290878fc0a3687a95fd6335eba4b6ed6e1c2fda2
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="valueof-method-javasqltimestamp-int"></a>valueOf 메서드(java.sql.Timestamp, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  만듭니다는 **DateTimeOffset** 지정 된 java.sql.Timestamp 값과 분 단위 오프셋을 나타내는 값을 GMT에서 특정 오프셋의 시점을 나타내는 개체입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public static DateTimeOffset valueOf(java.sql.Timestamp timestamp, int minutesOffset)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *timestamp*  
  
 java.sql.Timestamp값입니다.  
  
 *minutesOffset*  
  
 분 단위 오프셋입니다.  
  
## <a name="return-value"></a>반환 값  
 에 지정 된 시간이 지정 된 오프셋 위치 java.sql.Timestamp 개체로 분 GMT에서는 시점을 나타내는 DateTimeOffset 개체를 반환 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [DateTimeOffset 클래스](../../../connect/jdbc/reference/datetimeoffset-class.md)   
 [DateTimeOffset 멤버](../../../connect/jdbc/reference/datetimeoffset-members.md)  
  
  
