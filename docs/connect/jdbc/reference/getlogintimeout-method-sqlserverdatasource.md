---
title: "getLoginTimeout 메서드 (SQLServerDataSource) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLServerDataSource.getLoginTimeout
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: 316f067c-9e08-456a-af19-b80b0bbd4a5c
caps.latest.revision: "13"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: db6a44bdf43b46eccbcd3562975a6aa5a77e2d76
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/18/2017
---
# <a name="getlogintimeout-method-sqlserverdatasource"></a>getLoginTimeout 메서드(SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  시간 (초)의 수를 반환이 [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) 개체에서 연결을 시도 하는 동안 대기 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public int getLoginTimeout()  
```  
  
## <a name="return-value"></a>반환 값  
 **int** 까지의 시간을 초 수를 나타내는 값입니다.  
  
## <a name="remarks"></a>주의  
 응용 프로그램에서 제한 시간 값을 명시적으로 지정하지 않은 경우 이 메서드는 기본값인 15초를 반환합니다.  
  
 이 getLoginTimeout 메서드는 javax.sql.DataSource 인터페이스의 getLoginTimeout 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerDataSource 멤버](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 클래스](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
