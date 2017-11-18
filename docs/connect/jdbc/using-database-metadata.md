---
title: "데이터베이스 메타 데이터를 사용 하 여 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 8b048371-e912-4ed1-afd7-436978f48888
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 421da278e1a4503a73fb4f4f8a8aba0b3cff672f
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="using-database-metadata"></a>데이터베이스 메타데이터 사용
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  원하는 기능에 대 한 정보에 대 한 데이터베이스를 쿼리 하는 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 구현 하는 [SQLServerDatabaseMetaData](../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md) 클래스입니다. 이 클래스에는 단일 값 형태 또는 결과 집합으로 정보를 반환하는 다양한 메서드가 들어 있습니다.  
  
 SQLServerDatabaseMetaData 개체를 만들려면 사용할 수 있습니다는 [getMetaData](../../connect/jdbc/reference/getmetadata-method-sqlserverconnection.md) 의 메서드는 [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) 클래스에 연결 되어 있는 데이터베이스에 대 한 정보를 얻을 수 있습니다.  
  
 다음 예에서는 열린 연결에에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 예제 데이터베이스는 함수에 전달 된, SQLServerConnection 클래스의 getMetaData 메서드를 사용 하 여 SQLServerDatabaseMetadata 개체와의 다음 다양 한 메서드를 반환 하는 SQLServerDatabaseMetaData 개체 드라이버, 드라이버 버전, 데이터베이스 이름 및 데이터베이스 버전에 대 한 정보를 표시 하는 데 사용 됩니다.  
  
 [!code[JDBC#UsingDBMetaData1](../../connect/jdbc/codesnippet/Java/using-database-metadata_1.java)]  
  
## <a name="see-also"></a>관련 항목:  
 [JDBC 드라이버로 메타데이터 처리](../../connect/jdbc/handling-metadata-with-the-jdbc-driver.md)  
  
  

