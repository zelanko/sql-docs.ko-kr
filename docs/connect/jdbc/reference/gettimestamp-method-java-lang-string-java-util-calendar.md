---
title: "getTimestamp 메서드 (java.lang.String, java.util.Calendar) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerCallableStatement.getTimestamp (java.lang.String,java.util.Calendar)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 770668d9-2e52-4ff0-be2f-ebf78fd41644
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 99131aa06c14b70be43729d963a7ba4731acc099
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="gettimestamp-method-javalangstring-javautilcalendar"></a>getTimestamp 메서드(java.lang.String, java.util.Calendar)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 Java 프로그래밍 언어에서 달력 개체를 사용 하 여 매개 변수 이름 지정의 java.sql.Timestamp 개체로 지정된 된 매개 변수의 값을 검색 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.sql.Timestamp getTimestamp(java.lang.String name,  
                                       java.util.Calendar cal)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *name*  
  
 A **문자열** 매개 변수 이름이 들어 있는입니다.  
  
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
  
  

