---
title: "executeUpdate 메서드 (SQLServerStatement) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerStatement.executeUpdate
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 10ae662a-ce3c-4b24-875c-5c2df319d93b
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 09479ee3af274d06564427c4ca60f3cc15f36644
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="executeupdate-method-sqlserverstatement"></a>executeUpdate 메서드(SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  INSERT, UPDATE 또는 DELETE 문과 같은 지정된 SQL 문이나 SQL DDL 문 같이 아무 것도 반환하지 않는 SQL 문을 실행합니다. 부터는 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] JDBC 드라이버 3.0에서는 executeUpdate 병합 작업에서 업데이트 된 행의 올바른 수를 반환 합니다.  
  
## <a name="overload-list"></a>오버로드 목록  
  
|이름|Description|  
|----------|-----------------|  
|[executeUpdate (java.lang.String)](../../../connect/jdbc/reference/executeupdate-method-java-lang-string-sqlserverstatement.md)|INSERT, UPDATE, DELETE 또는 MERGE 문과 같은 지정된 SQL 문이나 SQL DDL 문 같이 아무 것도 반환하지 않는 SQL 문을 실행합니다.|  
|[executeUpdate (java.lang.String, int)](../../../connect/jdbc/reference/executeupdate-method-java-lang-string-int.md)|지정 된 SQL 문 및 신호 실행는 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 여부에 대 한 지정 된 플래그로 생성 된 자동 생성 키 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 개체 검색에 사용할 수 있어야 합니다.|  
|[executeUpdate (java.lang.String, int &#91; &#93;)](../../../connect/jdbc/reference/executeupdate-method-java-lang-string.md)|지정된 SQL 문을 실행하고, 지정된 배열에 표시된 자동 생성 키를 검색에 사용할 수 있도록 해야 할지 여부를 JDBC 드라이버에 알립니다.|  
|[executeUpdate (java.lang.String, java.lang.String &#91; &#93;)](../../../connect/jdbc/reference/executeupdate-method-java-lang-string-java-lang-string.md)|지정된 SQL 문을 실행하고, 지정된 배열에 표시된 자동 생성 키를 검색에 사용할 수 있도록 해야 할지 여부를 JDBC 드라이버에 알립니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerStatement 멤버](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 클래스](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
