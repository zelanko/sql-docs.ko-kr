---
title: "getSendTimeAsDatetime 메서드 (SQLServerDataSource) | Microsoft Docs"
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
ms.assetid: 02287122-5dc1-455d-987f-95fd9a69d503
caps.latest.revision: "15"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f784b25fe9390d98d32ab31e6f3f837e30aa746b
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/18/2017
---
# <a name="getsendtimeasdatetime-method-sqlserverdatasource"></a>getSendTimeAsDatetime 메서드(SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 메서드는에서 추가 된 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] JDBC 드라이버 3.0.  
  
 설정을 반환 하는 **sendTimeAsDatetime** 연결 속성입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public boolean getSendTimeAsDatetime();  
```  
  
## <a name="return-value"></a>반환 값  
 **true** java.sql.Time 값으로 서버에 보내집니다는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] **datetime** 유형입니다. **false** java.sql.Time 값으로 서버에 보내집니다는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] **시간** 유형입니다.  
  
## <a name="remarks"></a>주의  
 참조 [연결 속성을 설정할](../../../connect/jdbc/setting-the-connection-properties.md) 에 대 한 자세한 내용은 **sendTimeAsDatetime** 연결 속성입니다.  
  
 [SQLServerDataSource.setSendTimeAsDatetime](../../../connect/jdbc/reference/setsendtimeasdatetime-method-sqlserverdatasource.md) 프로그래밍 방식으로 설정할 수 있습니다는 **sendTimeAsDatetime** 연결 속성입니다.  
  
 자세한 내용은 참조 [구성 방법을 java.sql.Time 값에는 서버에 보내집니다](../../../connect/jdbc/configuring-how-java-sql-time-values-are-sent-to-the-server.md)합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerDataSource 멤버](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 클래스](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
