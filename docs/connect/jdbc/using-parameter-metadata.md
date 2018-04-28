---
title: 매개 변수 메타 데이터를 사용 하 여 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: db2c1957-91c6-4989-a07b-9f8be6d2033a
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9299c3cff07a594ab58014b4835b4ad796756b5c
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="using-parameter-metadata"></a>매개 변수 메타데이터 사용
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  쿼리에 [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) 또는 [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) 매개 변수를 포함 하는 방법에 대 한 개체는 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 구현 하는 [ SQLServerParameterMetaData](../../connect/jdbc/reference/sqlserverparametermetadata-class.md) 클래스입니다. 이 클래스에는 단일 값 형태로 정보를 반환하는 다양한 필드와 메서드가 들어 있습니다.  
  
 SQLServerParameterMetaData 개체를 만들려면 사용할 수 있습니다는 [getParameterMetaData](../../connect/jdbc/reference/getparametermetadata-method-sqlserverpreparedstatement.md) SQLServerPreparedStatement 및 SQLServerCallableStatement 클래스의 메서드.  
  
 다음 예에서는 열린 연결에에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 예제 데이터베이스는 함수에 전달 된, SQLServerCallableStatement 클래스의 getParameterMetaData 메서드는 SQLServerParameterMetaData 개체 및 다음 다양 한을 반환 하는 데 사용 됩니다 SQLServerParameterMetaData 개체의 메서드는 형식과 HumanResources.uspUpdateEmployeeHireInfo 저장 프로시저 내에 포함 된 매개 변수의 mode에 대 한 정보를 표시 하는 데 사용 됩니다.  
  
 [!code[JDBC#UsingParamMetaData1](../../connect/jdbc/codesnippet/Java/using-parameter-metadata_1.java)]  
    
> [!NOTE]  
SQLServerParameterMetaData 클래스를 사용 하 여 준비 된 문을 사용 하는 데는 몇 가지 제한이 있습니다. 
**Microsoft JDBC Driver 6.0 (또는 그 이상) for SQL Server**:으로 이러한 문은 하위 쿼리 및/또는 조인과 JDBC 드라이버는 SELECT, DELETE, INSERT 및 UPDATE 문을 지원 SQL Server 2008 또는 2008 r 2 사용 하면 됩니다.  

쿼리 병합도 지원 되지 않습니다 SQLServerParameterMetaData 클래스에 대 한 SQL Server 2008 또는 2008 r 2 사용 하는 경우. SQL Server 2012 이상 버전의 경우 복잡한 쿼리에서 매개 변수 메타데이터가 지원됩니다.  

암호화 된 열에 대 한 매개 변수 메타 데이터 검색을 지원 하지 않습니다. **Microsoft JDBC Driver 4.1 또는 4.2 for SQL Server와**: The JDBC 드라이버는 이러한 문은 하위 쿼리 및/또는 조인과으로 SELECT, DELETE, INSERT 및 UPDATE 문을 지원 합니다. 쿼리 병합은 또한 SQLServerParameterMetaData 클래스에 대해 지원 되지 않습니다.  
  
  
