---
title: jdbcCompliant 메서드 (SQLServerDriver) | Microsoft Docs
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
ms.topic: conceptual
apiname:
- SQLServerDriver.jdbcCompliant
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: b299b20d-d1cd-45b3-91dc-dcf579498570
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5cc11a28ca0b63f87b42b20b00a297eb217830c7
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="jdbccompliant-method-sqlserverdriver"></a>jdbcCompliant 메서드(SQLServerDriver)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  확인 된 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] JDBC 사양을 따르는지 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public boolean jdbcCompliant()  
```  
  
## <a name="return-value"></a>반환 값  
 **true 이면** JDBC 드라이버가 최소 요구 사항을 충족 하는 경우. 그렇지 않으면 **false**입니다.  
  
## <a name="remarks"></a>주의  
 이 jdbcCompliant 메서드는 java.sql.Driver 인터페이스의 jdbcCompliant 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerDriver 메서드](../../../connect/jdbc/reference/sqlserverdriver-methods.md)   
 [SQLServerDriver 멤버](../../../connect/jdbc/reference/sqlserverdriver-members.md)   
 [SQLServerDriver 클래스](../../../connect/jdbc/reference/sqlserverdriver-class.md)  
  
  
