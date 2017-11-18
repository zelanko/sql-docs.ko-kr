---
title: "JDBC 드라이버로 메타 데이터를 처리 합니다. | Microsoft Docs"
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
ms.assetid: 5cfb35d4-ddcd-40a2-8091-f29cddc32552
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 63d691c8bef93ad734a7596532ba567708128a2d
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="handling-metadata-with-the-jdbc-driver"></a>JDBC 드라이버로 메타데이터 처리
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 의 메타 데이터를 사용할 수는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 여러 가지 방법으로 데이터베이스입니다. JDBC 드라이버는 데이터베이스, 결과 집합 또는 매개 변수에 관한 메타데이터를 가져오는 데 사용할 수 있습니다.  
  
 메타 데이터를 검색 하기 위한 세 가지 클래스를 제공 하는 JDBC 드라이버는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 데이터베이스:  
  
-   [SQLServerDatabaseMetaData](../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md), 현재 연결 되어 있는 데이터베이스에 대 한 정보를 반환 하는 데 사용 되는 합니다.  
  
-   [SQLServerResultSetMetaData](../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md), 결과 집합에 대 한 정보를 반환 하는 데 사용 되는 합니다.  
  
-   [SQLServerParameterMetaData](../../connect/jdbc/reference/sqlserverparametermetadata-class.md), 준비 및 호출 가능한 문의 매개 변수에 관한 정보를 반환 하는 데 사용 되는 합니다.  
  
 이 섹션의 항목 메타 데이터에 세 개의 메타 데이터 클래스를 사용할 수는 방법을 설명는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 데이터베이스입니다.  
  
> [!NOTE]  
>  이 섹션에 설명된 메타데이터 메서드는 대개 응용 프로그램의 성능 측면에서 많은 비용이 소모되므로 신중하게 사용해야 합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
|항목|Description|  
|-----------|-----------------|  
|[데이터베이스 메타데이터 사용](../../connect/jdbc/using-database-metadata.md)|현재 연결된 데이터베이스에 관한 메타데이터 정보를 검색하는 방법을 설명합니다.|  
|[결과 집합 메타데이터 사용](../../connect/jdbc/using-result-set-metadata.md)|현재 결과 집합에 관한 메타데이터 정보를 검색하는 방법을 설명합니다.|  
|[매개 변수 메타데이터 사용](../../connect/jdbc/using-parameter-metadata.md)|준비된 문 및 호출 가능한 문의 매개 변수에 관한 메타데이터 정보를 검색하는 방법을 설명합니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [JDBC 드라이버 개요](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  

