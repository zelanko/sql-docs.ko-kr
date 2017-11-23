---
title: "JDBC 드라이버와 함께 SQL Server에 연결 | Microsoft Docs"
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
ms.assetid: 94bcfbe3-f00e-4774-bda8-bb7577518fec
caps.latest.revision: "30"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 624a6874931cb8af32bb69ea3ac0f8b395ef8915
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/18/2017
---
# <a name="connecting-to-sql-server-with-the-jdbc-driver"></a>JDBC 드라이버로 SQL Server에 연결
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  로 수행 하는 가장 기본적인 작업 중 하나는 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 에 대 한 연결을 확인 하는 것을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 데이터베이스입니다. 데이터베이스와 모든 상호 작용을 통해 발생 된 [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) 개체를 거의 모든 주요 동작 SQLServerConnection 개체와 연결 된 JDBC 드라이버가 처럼 평면 아키텍처 이기 때문에 한 합니다.  
  
 경우는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 은 java.net.preferIPv6Addresses 시스템 속성에 연결 하는 데 IPv4 대신 i p v 6이 사용 되도록 설정 IPv6 포트 에서만 수신 대기는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]:  
  
```  
System.setProperty("java.net.preferIPv6Addresses", "true");  
```  
  
 이 섹션의 항목에 대 한 연결을 사용 하는 방법에 설명 된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 데이터베이스입니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
|항목|Description|  
|-----------|-----------------|  
|[연결 URL 작성](../../connect/jdbc/building-the-connection-url.md)|에 연결 하기 위한 연결 URL을 형성 하는 방법에 설명 된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 데이터베이스입니다. 명명 된 인스턴스에 연결에 대해서도 설명는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 데이터베이스입니다.|  
|[연결 속성 설정](../../connect/jdbc/setting-the-connection-properties.md)|다양 한 연결 속성 및 수는 방법에 연결할 때에 설명 된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 데이터베이스입니다.|  
|[데이터 원본 속성 설정](../../connect/jdbc/setting-the-data-source-properties.md)|Java Platform, Enterprise Edition(Java EE) 환경에서 데이터 원본을 사용하는 방법에 대해 설명합니다.|  
|[연결 작업](../../connect/jdbc/working-with-a-connection.md)|에 대 한 연결의 인스턴스를 만들 수 있는 다양 한 방법에 설명 된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 데이터베이스입니다.|  
|[연결 풀링 사용](../../connect/jdbc/using-connection-pooling.md)|JDBC 드라이버에서 연결 풀링의 사용을 지원하는 방법을 설명합니다.|  
|[데이터베이스 미러링 &#40;를 사용 하 여 JDBC &#41;](../../connect/jdbc/using-database-mirroring-jdbc.md)|JDBC 드라이버에서 데이터베이스 미러링 사용을 지원하는 방법을 설명합니다.|  
|[고가용성, 재해 복구를 위한 JDBC 드라이버 지원](../../connect/jdbc/jdbc-driver-support-for-high-availability-disaster-recovery.md)|AlwaysOn 가용성 그룹에 연결할 응용 프로그램을 개발하는 방법을 설명합니다.|  
|[Kerberos 통합 인증을 사용하여 SQL Server에 연결](../../connect/jdbc/using-kerberos-integrated-authentication-to-connect-to-sql-server.md)|응용 프로그램에 연결을 위한 Java 구현을 설명는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Kerberos 통합된 인증을 사용 하 여 데이터베이스입니다.|  
|[Azure SQL 데이터베이스에 연결](../../connect/jdbc/connecting-to-an-azure-sql-database.md)|SQL Azure에서 데이터베이스의 연결 문제를 설명합니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [JDBC 드라이버 개요](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
