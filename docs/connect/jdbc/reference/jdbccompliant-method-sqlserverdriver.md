---
title: jdbcCompliant 메서드 (SQLServerDriver) | Microsoft Docs
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
- SQLServerDriver.jdbcCompliant
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: b299b20d-d1cd-45b3-91dc-dcf579498570
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 357024153bb862ff369278096018dd544ead4ca8
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
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
  
  
