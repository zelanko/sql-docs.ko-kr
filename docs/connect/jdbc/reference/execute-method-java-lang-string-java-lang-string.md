---
title: "execute 메서드 (java.lang.String, java.lang.String) | Microsoft Docs"
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
- SQLServerStatement.execute (java.lang.String.java.lang.String[])
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 9451c7c2-4c0d-4d1e-9b42-a26ff28e3f6a
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9dc327a107a8a164e00f2f34f21515c96766e21d
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="execute-method-javalangstring-javalangstring"></a>execute 메서드 (java.lang.String, java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  여러 결과 및 신호를 반환할 수 있는 지정된 된 SQL 문을 실행 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 지정된 된 배열에 표시 되는 자동 생성 키 수 있도록 검색에 사용할 수 있습니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public final boolean execute(java.lang.String sql,  
                             java.lang.String[] columnNames)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *sql*  
  
 A **문자열** SQL 문이 들어 있는입니다.  
  
 *columnNames*  
  
 자동 생성 키의 열 이름을 사용할 수 있도록 해야 하는지 여부를 나타내는 문자열의 배열입니다.  
  
## <a name="return-value"></a>반환 값  
 **true 이면** 첫 번째 결과가 결과 집합이 면 합니다. 그렇지 않으면 **false**입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 execute 메서드는 java.sql.Statement 인터페이스의 execute 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [방법 &#40; 실행 SQLServerStatement &#41;](../../../connect/jdbc/reference/execute-method-sqlserverstatement.md)   
 [SQLServerStatement 멤버](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 클래스](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  

