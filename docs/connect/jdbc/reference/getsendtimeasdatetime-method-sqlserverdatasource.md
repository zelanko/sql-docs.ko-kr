---
title: getSendTimeAsDatetime 메서드 (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 02287122-5dc1-455d-987f-95fd9a69d503
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f18836d12be9834512783f90a2d7730fcfc98798
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47845211"
---
# <a name="getsendtimeasdatetime-method-sqlserverdatasource"></a>getSendTimeAsDatetime 메서드(SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 메서드는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] JDBC 드라이버 3.0에서 추가되었습니다.  
  
 설정을 반환 합니다 **sendTimeAsDatetime** 연결 속성입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public boolean getSendTimeAsDatetime();  
```  
  
## <a name="return-value"></a>반환 값  
 **true** java.sql.Time 값을 서버로 보내집니다는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **datetime** 형식입니다. **false** java.sql.Time 값을 서버로 보내집니다는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **시간** 형식입니다.  
  
## <a name="remarks"></a>Remarks  
 참조 [연결 속성 설정](../../../connect/jdbc/setting-the-connection-properties.md) 에 대 한 자세한 내용은 합니다 **sendTimeAsDatetime** 연결 속성입니다.  
  
 [SQLServerDataSource.setSendTimeAsDatetime](../../../connect/jdbc/reference/setsendtimeasdatetime-method-sqlserverdatasource.md)을 사용하면 **sendTimeAsDatetime** 연결 속성을 프로그래밍 방식으로 설정할 수 있습니다.  
  
 자세한 내용은 [어떻게 구성 java.sql.Time 값을 서버로 전송 됩니다](../../../connect/jdbc/configuring-how-java-sql-time-values-are-sent-to-the-server.md)합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerDataSource 멤버](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 클래스](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
