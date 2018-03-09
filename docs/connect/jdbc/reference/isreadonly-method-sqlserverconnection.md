---
title: "isReadOnly 메서드 (SQLServerConnection) | Microsoft Docs"
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
apiname: SQLServerConnection.isReadOnly
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: 902fd2c1-05e0-436e-9779-c048cdb8475a
caps.latest.revision: "15"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0e305e9355ad43bf7603991cc40d23cf21ce8f86
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/18/2017
---
# <a name="isreadonly-method-sqlserverconnection"></a>isReadOnly 메서드(SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  나타냅니다 여부이 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 개체가 읽기 전용 모드 인지 합니다.  
  
> [!NOTE]  
>  이 메서드는 현재 지원 되지 않습니다는 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public boolean isReadOnly()  
```  
  
## <a name="return-value"></a>반환 값  
 **true 이면** 연결이 읽기 전용 모드인 경우 **false** 없는 경우.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 isReadOnly 메서드는 java.sql.Connection 인터페이스의 isReadOnly 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerConnection 멤버](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 클래스](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
