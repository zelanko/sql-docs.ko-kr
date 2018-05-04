---
title: 데이터 형식 (JDBC) 사용 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: b39f44d0-3710-4bc6-880c-35bd8c10a734
caps.latest.revision: 18
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9e267465de5b8fe51a1ae6aa3e3e2f371840e6d6
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="working-with-data-types-jdbc"></a>데이터 형식(JDBC) 사용
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  기본 기능은 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] Java 개발자에 포함 된 데이터에 액세스할 수 있도록 하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 데이터베이스. 이를 위해 JDBC 드라이버는 사이의 변환을 중재 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 데이터 형식과 Java 언어 형식 및 개체입니다.  
  
> [!NOTE]  
>  에 대 한 자세한 설명은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 간 차이점 및 Java 언어 데이터 형식으로 변환 하는 방법을 포함 하 여 JDBC 드라이버 데이터 형식을 참조 및 [JDBC 드라이버 데이터 형식 이해](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)합니다.  
  
 SQL Server 데이터 형식을 사용 하려면 JDBC 드라이버는 get\<유형 > 설정 및\<유형 >에 대 한 메서드는 [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) 및 [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) 클래스 및 그 제공 get\<유형 > 업데이트 및\<유형 >에 대 한 메서드는 [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) 클래스입니다. 어떤 메서드를 사용할지는 작업하는 데이터 형식 및 결과 집합이나 쿼리 사용 여부에 따라 달라집니다.  
  
 이 섹션의 항목에 액세스 하려면 JDBC 드라이버 데이터 형식을 사용 하는 방법에 설명 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Java 응용 프로그램의 데이터입니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
|항목|Description|  
|-----------|-----------------|  
|[기본 데이터 형식 샘플](../../connect/jdbc/basic-data-types-sample.md)|기본 검색 하려면 결과 집합 getter 메서드를 사용 하는 방법을 설명 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 데이터 형식 값 및 결과 집합 업데이트 메서드를 사용 하 여 이러한 값을 업데이트 하는 방법입니다.|  
|[SQLXML 데이터 형식 샘플](../../connect/jdbc/sqlxml-data-type-sample.md)|관계형 데이터베이스에 XML 데이터를 저장 하는 방법, 데이터베이스에서 XML 데이터를 검색 하는 방법 및 사용 하 여 XML 데이터를 구문 분석 하는 방법에 설명 된 **SQLXML** Java 데이터 형식입니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [샘플 JDBC 드라이버 응용 프로그램](../../connect/jdbc/sample-jdbc-driver-applications.md)  
  
  
