---
title: getQueryTimeout 메서드 (SQLServerStatement) | Microsoft Docs
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
- SQLServerStatement.getQueryTimeout
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 8dff954f-b458-4fa6-abe6-be62ff75e2b9
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b38e527fe8d63624e98d9d29d7654c693705b8de
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="getquerytimeout-method-sqlserverstatement"></a>getQueryTimeout 메서드(SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  시간 (초)의 수를 검색 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 이 대기 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 실행 하는 개체입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public final int getQueryTimeout()  
```  
  
## <a name="return-value"></a>반환 값  
 **int** 제한이 없는 경우 JDBC 드라이버에서 대기 하는 시간 (초) 또는 0의 수를 나타내는입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 getQueryTimeout 메서드는 java.sql.Statement 인터페이스의 getQueryTimeout 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerStatement 멤버](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 클래스](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
