---
description: getClientConnectionID 메서드(SQLServerConnection)
title: getClientConnectionID 메서드(SQLServerConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: bee39c11-733a-461f-92cc-33efcb2af87d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 18bd2254052364c746ad88e972a57bdfc7bfbf5f
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91725444"
---
# <a name="getclientconnectionid-method-sqlserverconnection"></a>getClientConnectionID 메서드(SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  연결 시도가 성공 또는 실패했는지 여부에 관계 없이 최근 연결 시도의 연결 ID를 가져옵니다.  
  
## <a name="syntax"></a>구문  
  
``` 
public Java.util.UUID SQLServerConnection.getClientConnectionID();  
```  
  
## <a name="return-value"></a>Return Value  
 가장 최근에 연결을 시도한 연결 ID를 나타내는 16바이트 GUID입니다. 또는 연결 요청이 시작된 후 실패하거나 사전 로그인 핸드셰이크가 있을 경우 NULL입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 확장 이벤트 로그의 진단 정보 액세스에 대한 자세한 내용은 [확장 이벤트 로그의 진단 정보 액세스](../../../connect/jdbc/accessing-diagnostic-information-in-the-extended-events-log.md)를 참조하세요.  
  
 다음 예제는 연결 ID를 가져오는 방법을 설명합니다.  
  
```  
Connection con = DriverManager.getConnection(connectionUrl);  
UUID id = ((ISQLServerConnection)con).getClientConnectionId();  
```  
  
 다음 예제는 연결 ID를 가져오는 다른 방법을 설명합니다.  
  
```  
SQLServerConnectionPoolDataSource ds = new SQLServerConnectionPoolDataSource();  
ds.setUser("...");  
ds.setPassword("...");  
ds.setServerName("...");  
PooledConnection pcon= ds.getPooledConnection();  
Connection cn = pcon.getConnection();  
UUID conid = ((ISQLServerConnection)cn).getClientConnectionId();  
```  
  
 **getClientConnectionID**는 연결하는 서버의 버전에 상관없이 작동하지만 확장 이벤트 로그 및 연결 링 버퍼 오류에 대한 항목은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 2008 R2 이전 버전에 표시되지 않습니다.  
  
 연결 ID 로깅이 활성화되어 있는 확장 이벤트이고 서버에서 실패가 발생한 경우 확장 이벤트 로그에서 연결 ID를 찾아 확인할 수 있습니다. 특정 연결 오류의 경우 연결 링 버퍼([연결 링 버퍼를 사용하여 SQL Server 2008의 연결 문제 해결](/archive/blogs/sql_protocols/connectivity-troubleshooting-in-sql-server-2008-with-the-connectivity-ring-buffer))에서 연결 ID를 찾을 수도 있습니다. 연결 ID가 연결 링 버퍼에 없는 경우 네트워크 오류를 가정해 볼 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerConnection 멤버](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 클래스](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
