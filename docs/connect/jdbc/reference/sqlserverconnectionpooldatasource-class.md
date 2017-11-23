---
title: "SQLServerConnectionPoolDataSource 클래스 | Microsoft Docs"
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
ms.assetid: b00e5a90-2af7-4d04-8ef8-256183777dcf
caps.latest.revision: "13"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7d59b3d81b14221233f0fc501092b8ba7c096ea7
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/18/2017
---
# <a name="sqlserverconnectionpooldatasource-class"></a>SQLServerConnectionPoolDataSource 클래스
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  연결 풀 관리자를 위한 실제 데이터베이스 연결을 나타냅니다.  
  
 **패키지에 대 한** com.microsoft.sqlserver.jdbc  
  
 **확장:** [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
 **구현:** javax.sql.ConnectionPoolDataSource  
  
## <a name="syntax"></a>구문  
  
```  
  
public class SQLServerConnectionPoolDataSource  
```  
  
## <a name="remarks"></a>주의  
 SQLServerConnectionPoolDataSource는 기본 제공 연결 풀링을 지원 하며 Java Platform, Enterprise Edition (Java와 같은 물리적 연결을 제공 하도록 ConnectionPoolDataSource 필요로 하는 Java 응용 프로그램 서버 환경에서 일반적으로 사용 JDBC 3.0 API를 제공 하는 EE) 응용 프로그램 서버 사양 연결 풀링을 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerConnectionPoolDataSource 멤버](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-members.md)   
 [JDBC 드라이버 API 참조](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
