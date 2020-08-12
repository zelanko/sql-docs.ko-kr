---
title: 연결 풀링 사용
description: JDBC Driver for SQL Server가 JDBC 규격 인터페이스를 제공하여 Java의 연결 풀링을 지원하는 방법을 알아봅니다.
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 699d4e8a-34bf-4c60-b0d5-4a10dad6084a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c3bcacec5f85150f7de437d936463a3b3807f9ef
ms.sourcegitcommit: cb620c77fe6bdefb975968837706750c31048d46
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2020
ms.locfileid: "86391751"
---
# <a name="using-connection-pooling"></a>연결 풀링 사용

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]는 Java Platform, Enterprise Edition(Java EE) 연결 풀링을 지원합니다. 미들웨어 공급업체가 제공하며 JDBC 3.0과 호환되는 모든 연결 풀링 구현에 참여할 수 있도록 JDBC 드라이버는 JDBC 3.0 필수 인터페이스를 구현합니다. Java EE 애플리케이션 서버와 같은 미들웨어는 대개 호환되는 연결 풀링 기능을 제공합니다. JDBC 드라이버는 이러한 환경에서 풀링된 연결에 참여합니다.  
  
> [!NOTE]  
> JDBC 드라이버는 Java EE 연결 풀링을 지원하지만 자체 풀링 구현을 제공하지는 않습니다. 대신 JDBC 드라이버는 타사 Java 애플리케이션 서버를 통해 연결을 관리합니다.  
  
## <a name="remarks"></a>설명

연결 풀링을 구현하는 데 필요한 클래스는 다음과 같습니다.  
  
| 클래스                                                           | 구현                                                    | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| --------------------------------------------------------------- | ------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| com.microsoft.sqlserver.jdbc. SQLServerXADataSource             | javax.sql.ConnectionPoolDataSource and javax.sql.XADataSource | [SQLServerXADataSource](../../connect/jdbc/reference/sqlserverxadatasource-class.md) 클래스는 모든 JDBC 3.0 풀링과 XA 인터페이스를 구현하므로 Java EE 서버가 필요한 모든 경우에 이 클래스를 사용하는 것이 좋습니다.                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| com.microsoft.sqlserver.jdbc. SQLServerConnectionPoolDataSource | javax.sql.ConnectionPoolDataSource                            | 이 클래스는 Java EE 애플리케이션 서버에서 해당 연결 풀을 실제 연결로 채울 수 있도록 하는 연결 팩터리입니다. Java EE 공급업체의 구성에 javax.sql.ConnectionPoolDataSource를 구현하는 클래스가 필요한 경우 클래스 이름을 [SQLServerConnectionPoolDataSource](../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md)로 지정합니다. [SQLServerXADataSource](../../connect/jdbc/reference/sqlserverxadatasource-class.md) 클래스는 풀링 및 XA 인터페이스를 모두 구현하고 더 많은 Java EE 서버 구성에서 검증되었으므로 일반적으로 이 클래스를 사용하는 것이 좋습니다. |
  
 JDBC 애플리케이션 코드에서 풀링의 이점을 극대화하려면 항상 연결을 명시적으로 닫아야 합니다. 애플리케이션에서 연결을 명시적으로 닫으면 풀링 구현은 연결을 바로 다시 사용할 수 있습니다. 연결을 닫지 않으면 다른 애플리케이션에서 이를 다시 사용할 수 없습니다. 애플리케이션에서는 `finally` 구문을 사용하여 예외가 발생하더라도 풀링된 연결이 닫히도록 할 수 있습니다.  
  
> [!NOTE]  
> JDBC 드라이버는 현재 연결을 풀에 반환할 때 sp_reset_connection 저장 프로시저를 호출하지 않습니다. 대신 JDBC 드라이버는 타사 Java 애플리케이션 서버를 통해 연결을 원래 상태로 되돌립니다.  
  
## <a name="see-also"></a>참고 항목

[JDBC 드라이버로 SQL Server에 연결](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)  
