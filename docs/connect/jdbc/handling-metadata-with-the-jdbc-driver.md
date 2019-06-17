---
title: JDBC 드라이버로 메타 데이터 처리 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 5cfb35d4-ddcd-40a2-8091-f29cddc32552
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: c479651027429463dc88ae7ddce816a7973ac0d2
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66781776"
---
# <a name="handling-metadata-with-the-jdbc-driver"></a>JDBC 드라이버로 메타데이터 처리
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스의 메타데이터를 다양한 방법으로 처리할 수 있습니다. JDBC 드라이버는 데이터베이스, 결과 집합 또는 매개 변수에 관한 메타데이터를 가져오는 데 사용할 수 있습니다.  
  
 JDBC 드라이버는 다음과 같은 세 개의 클래스를 통해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에서 메타데이터를 검색합니다.  
  
-   [SQLServerDatabaseMetaData](../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md). 현재 연결된 데이터베이스에 관한 정보를 반환하는 데 사용됩니다.  
  
-   [SQLServerResultSetMetaData](../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md). 결과 집합에 관한 정보를 반환하는 데 사용됩니다.  
  
-   [SQLServerParameterMetaData](../../connect/jdbc/reference/sqlserverparametermetadata-class.md). 준비된 문 및 호출 가능한 문의 매개 변수에 관한 정보를 반환하는 데 사용됩니다.  
  
 이 섹션의 항목에서는 이러한 세 개의 메타데이터 클래스를 통해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스의 메타데이터를 사용하는 방법에 대해 설명합니다.  
  
> [!NOTE]  
>  이 섹션에 설명된 메타데이터 메서드는 대개 응용 프로그램의 성능 측면에서 많은 비용이 소모되므로 신중하게 사용해야 합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
|항목|설명|  
|-----------|-----------------|  
|[데이터베이스 메타데이터 사용](../../connect/jdbc/using-database-metadata.md)|현재 연결된 데이터베이스에 관한 메타데이터 정보를 검색하는 방법을 설명합니다.|  
|[결과 집합 메타데이터 사용](../../connect/jdbc/using-result-set-metadata.md)|현재 결과 집합에 관한 메타데이터 정보를 검색하는 방법을 설명합니다.|  
|[매개 변수 메타데이터 사용](../../connect/jdbc/using-parameter-metadata.md)|준비된 문 및 호출 가능한 문의 매개 변수에 관한 메타데이터 정보를 검색하는 방법을 설명합니다.|  
  
## <a name="see-also"></a>참고 항목  
 [JDBC 드라이버 개요](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
