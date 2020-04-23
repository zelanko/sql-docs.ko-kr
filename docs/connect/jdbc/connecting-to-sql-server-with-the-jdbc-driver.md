---
title: JDBC 드라이버로 SQL Server에 연결 | Microsoft Docs
description: Microsoft JDBC Driver for SQL Server를 사용하여 데이터베이스에 연결하는 경우 데이터베이스와의 모든 상호 작용은 SQLServerConnection 개체를 거칩니다.
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 94bcfbe3-f00e-4774-bda8-bb7577518fec
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1089960af020e648586f59914ccc91e99bf0b9af
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2020
ms.locfileid: "81487968"
---
# <a name="connecting-to-sql-server-with-the-jdbc-driver"></a>JDBC 드라이버로 SQL Server에 연결
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]로 수행하는 가장 기본적인 작업 중 하나는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 연결하는 것입니다. 데이터베이스와의 모든 상호 작용은 [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) 개체를 통해 이루어지며, JDBC 드라이버가 이처럼 평면 아키텍처이기 때문에 거의 모든 주요 동작에서 SQLServerConnection 개체에 영향을 미칩니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 IPv6 포트에서만 수신 대기하는 경우 java.net.preferIPv6Addresses 시스템 속성을 설정하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 연결하는 데 IPv4 대신 IPv6이 사용되도록 합니다.  
  
```java
System.setProperty("java.net.preferIPv6Addresses", "true");  
```  
  
 이 섹션의 항목에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 대한 연결을 사용하는 방법을 설명합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
|항목|Description|  
|-----------|-----------------|  
|[연결 URL 작성](../../connect/jdbc/building-the-connection-url.md)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 연결하는 데 사용할 연결 URL을 형성하는 방법을 설명합니다. 또한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스의 명명된 인스턴스에 연결하는 방법에 대해 설명합니다.|  
|[연결 속성 설정](../../connect/jdbc/setting-the-connection-properties.md)|다양한 연결 속성과 이러한 속성을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 연결할 때 사용하는 방법을 설명합니다.|  
|[데이터 원본 속성 설정](../../connect/jdbc/setting-the-data-source-properties.md)|Java Platform, Enterprise Edition(Java EE) 환경에서 데이터 원본을 사용하는 방법에 대해 설명합니다.|  
|[연결 사용](../../connect/jdbc/working-with-a-connection.md)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 대한 연결 인스턴스를 만드는 다양한 방법을 설명합니다.|  
|[연결 풀링 사용](../../connect/jdbc/using-connection-pooling.md)|JDBC 드라이버에서 연결 풀링의 사용을 지원하는 방법을 설명합니다.|  
|[데이터베이스 미러링 사용 &#40;JDBC&#41;](../../connect/jdbc/using-database-mirroring-jdbc.md)|JDBC 드라이버에서 데이터베이스 미러링 사용을 지원하는 방법을 설명합니다.|  
|[고가용성, 재해 복구를 위한 JDBC 드라이브 지원](../../connect/jdbc/jdbc-driver-support-for-high-availability-disaster-recovery.md)|AlwaysOn 가용성 그룹에 연결할 애플리케이션을 개발하는 방법을 설명합니다.|  
|[Kerberos 통합 인증을 사용하여 SQL Server에 연결](../../connect/jdbc/using-kerberos-integrated-authentication-to-connect-to-sql-server.md)|Kerberos 통합 인증을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 연결하는 애플리케이션을 위한 Java 구현을 설명합니다.|  
|[Azure SQL 데이터베이스에 연결](../../connect/jdbc/connecting-to-an-azure-sql-database.md)|SQL Azure에서 데이터베이스의 연결 문제를 설명합니다.|  
  
## <a name="see-also"></a>참고 항목  
 [JDBC 드라이버 개요](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
