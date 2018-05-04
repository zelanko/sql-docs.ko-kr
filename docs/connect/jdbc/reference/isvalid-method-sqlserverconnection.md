---
title: isValid 메서드 (SQLServerConnection) | Microsoft Docs
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
ms.assetid: 3b0a8bbf-9369-4456-9ab8-1434ccacdd7e
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d6313844442f651fb64127ef0b591f1c0ffda363
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="isvalid-method-sqlserverconnection"></a>isValid 메서드(SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  나타냅니다 여부이 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 개체가 닫히지 않은 하 고 여전히 유효 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public boolean isValid(int timeout)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *timeout*  
  
 **int** 연결 유효성 검사에 대 한 대기 시간 (초)의 수를 지정 하는 합니다.  
  
## <a name="return-value"></a>반환 값  
 **true 이면** 연결이 잘못 되었습니다. **false** 경우 연결이 유효 하지 않거나 제한 시간이 만료 되기 전에 연결의 유효성을 확인할 수 없습니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 isValid 메서드는 java.sql.Connection 인터페이스의 isValid 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerConnection 멤버](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 클래스](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
