---
title: setLoginTimeout 메서드 (SQLServerDataSource) | Microsoft Docs
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
- SQLServerDataSource.setLoginTimeout
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: b63d1cf4-dc1b-4e35-9a56-50436642eaaf
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 08aa17692a03f444a304e65b6ae7ad2f872ff34a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="setlogintimeout-method-sqlserverdatasource"></a>setLoginTimeout 메서드(SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  시간 (초) 수를 설정이 [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) 개체에서 연결을 시도 하는 동안 대기 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void setLoginTimeout(int loginTimeout)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *LoginTimeout*  
  
 **int** 까지의 시간을 초 수를 나타내는 값입니다. 0은 제한 시간이 기본 시스템 제한 시간(기본적을 15초로 지정됨)임을 의미합니다.  
  
## <a name="remarks"></a>주의  
 이 setLoginTimeout 메서드는 javax.sql.DataSource 인터페이스의 setLoginTimeout 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerDataSource 멤버](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 클래스](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
