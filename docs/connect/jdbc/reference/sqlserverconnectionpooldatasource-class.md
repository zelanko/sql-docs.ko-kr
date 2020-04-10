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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0accd21f53a4ba1a86e4b7555be9d2ba9a087474
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80921047"
---
# <a name="sqlserverconnectionpooldatasource-class"></a>SQLServerConnectionPoolDataSource 클래스
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  연결 풀 관리자를 위한 실제 데이터베이스 연결을 나타냅니다.  
  
 **패키지:** com.microsoft.sqlserver.jdbc  
  
 **확장:** [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
 **구현:** javax.sql.ConnectionPoolDataSource  
  
## <a name="syntax"></a>구문  
  
```  
  
public class SQLServerConnectionPoolDataSource  
```  
  
## <a name="remarks"></a>설명  
 SQLServerConnectionPoolDataSource는 일반적으로 기본 제공 연결 풀링을 지원하는 JDBC 3.0 API 사양 연결 풀링을 제공하는 Java 애플리케이션 서버 환경에서 사용되며, Java Platform, Enterprise Edition(Java EE) 애플리케이션 서버와 같이 실제 연결을 제공하기 위해 ConnectionPoolDataSource가 필요합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerConnectionPoolDataSource 멤버](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-members.md)   
 [JDBC 드라이버 API 참조](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
