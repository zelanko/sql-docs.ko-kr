---
title: SQLServerConnectionPoolDataSource 클래스 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: b00e5a90-2af7-4d04-8ef8-256183777dcf
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bb073be8ef92d44f8821078f60622341638a010d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67971653"
---
# <a name="sqlserverconnectionpooldatasource-class"></a>SQLServerConnectionPoolDataSource 클래스
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  연결 풀 관리자를 위한 실제 데이터베이스 연결을 나타냅니다.  
  
 **패키지:** com.microsoft.sqlserver.jdbc  
  
 **Extends:** [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
 **구현:** javax.sql.ConnectionPoolDataSource  
  
## <a name="syntax"></a>구문  
  
```  
  
public class SQLServerConnectionPoolDataSource  
```  
  
## <a name="remarks"></a>Remarks  
 SQLServerConnectionPoolDataSource는 일반적으로 기본 제공 연결 풀링을 지원하는 JDBC 3.0 API 사양 연결 풀링을 제공하는 Java 애플리케이션 서버 환경에서 사용되며, Java Platform, Enterprise Edition(Java EE) 애플리케이션 서버와 같이 실제 연결을 제공하기 위해 ConnectionPoolDataSource가 필요합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerConnectionPoolDataSource 멤버](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-members.md)   
 [JDBC 드라이버 API 참조](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
