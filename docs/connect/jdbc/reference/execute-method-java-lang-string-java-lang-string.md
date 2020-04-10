---
title: execute 메서드(java.lang.String, java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.execute (java.lang.String.java.lang.String[])
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 9451c7c2-4c0d-4d1e-9b42-a26ff28e3f6a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4bbc0a0828bcc146cf2a49625e51baa77703593b
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80922110"
---
# <a name="execute-method-javalangstring-javalangstring"></a>execute 메서드(java.lang.String, java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  여러 결과를 반환할 수 있는 지정된 SQL 문을 실행하고 지정된 배열에 표시된 자동 생성 키를 검색에 사용할 수 있도록 해야 할지 여부를 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]에 알립니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public final boolean execute(java.lang.String sql,  
                             java.lang.String[] columnNames)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *sql*  
  
 SQL 문이 포함된 **문자열**입니다.  
  
 *columnNames*  
  
 자동 생성 키의 열 이름을 사용할 수 있도록 해야 하는지 여부를 나타내는 문자열의 배열입니다.  
  
## <a name="return-value"></a>Return Value  
 첫 번째 결과가 결과 집합이면 **true**이고, 그렇지 않으면 **false**입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 execute 메서드는 java.sql.Statement 인터페이스의 execute 메서드에 의해 지정됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [execute 메서드&#40;SQLServerStatement&#41;](../../../connect/jdbc/reference/execute-method-sqlserverstatement.md)   
 [SQLServerStatement 멤버](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 클래스](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
