---
title: executeUpdate 메서드 (java.lang.String, java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
apiname:
- SQLServerStatement.executeUpdate (java.lang.String[])
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 2f44a689-65c8-4c94-9574-e9c08ea7918e
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f1e54a91eb98ee628cd01e429aa81da6df876005
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="executeupdate-method-javalangstring-javalangstring"></a>executeUpdate 메서드 (java.lang.String, java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  주어진 신호 및 SQL 문을 실행 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 자동 생성 키 지정된 배열에 표시는 이루어져야 검색에 사용할 수 있습니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public final int executeUpdate(java.lang.String sql,  
                               java.lang.String[] columnNames)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *sql*  
  
 A **문자열** SQL 문이 들어 있는입니다.  
  
 *columnNames*  
  
 형식의 배열 **문자열** 나타내는 자동 생성 키의 열 이름을 사용할 수 있어야 합니다.  
  
## <a name="return-value"></a>반환 값  
 **int** 행의 수, 영향을 받는 0 DDL 문을 사용 하는 경우를 나타내는입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 executeUpdate 메서드는 java.sql.Statement 인터페이스의 executeUpdate 메서드에 의해 지정 됩니다.  
  
 1 보다 큰 또는 둘 이상의 결과 집합을 사용 하 여 생성 하 여 업데이트 횟수로 인해 저장된 프로시저를 실행 하는 경우는 [실행](../../../connect/jdbc/reference/execute-method-sqlserverstatement.md) 메서드를 저장된 프로시저를 실행 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [executeUpdate 메서드 &#40;SQLServerStatement&#41;](../../../connect/jdbc/reference/executeupdate-method-sqlserverstatement.md)   
 [SQLServerStatement 멤버](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 클래스](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
