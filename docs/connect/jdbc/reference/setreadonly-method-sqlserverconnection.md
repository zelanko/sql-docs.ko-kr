---
title: "setReadOnly 메서드 (SQLServerConnection) | Microsoft Docs"
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
apiname: SQLServerConnection.setReadOnly
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: bd11fd50-f092-43a0-a6bc-c63e70cff8da
caps.latest.revision: "14"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7acd45c0594d53e4121f1162c98a91a183b650a8
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/18/2017
---
# <a name="setreadonly-method-sqlserverconnection"></a>setReadOnly 메서드(SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 배치 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 개체의 읽기 전용 모드는 힌트를 JDBC 드라이버에서 데이터베이스 최적화를 사용할 수 있습니다.  
  
> [!NOTE]  
>  이 메서드는에서 지원 되지 않습니다는 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void setReadOnly(boolean readOnly)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *읽기 전용*  
  
 **true 이면** 연결이 읽기 전용으로 설정 될 경우. 그렇지 않으면 **false**입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 setReadOnly 메서드는 java.sql.Connection 인터페이스의 setReadOnly 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerConnection 멤버](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 클래스](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
