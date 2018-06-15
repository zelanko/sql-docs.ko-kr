---
title: setTimestamp 메서드 (int, java.sql.Timestamp, java.util.Calendar) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerPreparedStatement.setTimestamp (int, java.sql.Timestamp, java.util.Calendar))
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 10c93cbf-f831-4e00-8e37-ea728bf34b1e
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 319972f9c911236ffbcc35c14e7489d0f581328a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32843958"
---
# <a name="settimestamp-method-int-javasqltimestamp-javautilcalendar"></a>setTimestamp 메서드(int, java.sql.Timestamp, java.util.Calendar)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 매개 변수를 지정된 타임스탬프 및 달력 값으로 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public final void setTimestamp(int n,  
                               java.sql.Timestamp x,  
                               java.util.Calendar cal)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *n*  
  
 **int** 매개 변수 수를 나타내는입니다.  
  
 *x*  
  
 타임 스탬프 개체입니다.  
  
 *cal*  
  
 일정 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 setTimestamp 메서드는 java.sql.PreparedStatement 인터페이스의 setTimestamp 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [setTimestamp 메서드 &#40;SQLServerPreparedStatement&#41;](../../../connect/jdbc/reference/settimestamp-method-sqlserverpreparedstatement.md)   
 [SQLServerPreparedStatement 멤버](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [SQLServerPreparedStatement 클래스](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
