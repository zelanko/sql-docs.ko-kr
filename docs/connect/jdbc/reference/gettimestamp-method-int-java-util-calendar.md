---
title: "getTimestamp 메서드 (int, java.util.Calendar) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLServerCallableStatement.getTimestamp (int, java.util.Calendar)
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: 161c559a-8651-44ba-a914-15eb6a612417
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ce7ad759d6901ccdc641d693f836180a1152fe84
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/18/2017
---
# <a name="gettimestamp-method-int-javautilcalendar"></a>getTimestamp 메서드(int, java.util.Calendar)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 Java 프로그래밍 언어에서 달력 개체를 사용 하 여 지정 된 매개 변수 인덱스의에서 java.sql.Timestamp 개체로 지정된 된 매개 변수의 값을 검색 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.sql.Timestamp getTimestamp(int index,  
                                       java.util.Calendar cal)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *인덱스*  
  
 **int** 매개 변수 인덱스를 나타내는입니다.  
  
 *cal*  
  
 일정 개체입니다.  
  
## <a name="return-value"></a>반환 값  
 타임 스탬프 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 getTimestamp 메서드는 java.sql.CallableStatement 인터페이스의 getTimestamp 메서드에 의해 지정 됩니다.  
  
 이 메서드가 반환 값만 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] **datetime** 및 **smalldatetime** 열입니다.  
  
## <a name="see-also"></a>관련 항목:  
 [getTimestamp 메서드 &#40; SQLServerCallableStatement &#41;](../../../connect/jdbc/reference/gettimestamp-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 멤버](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 클래스](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
