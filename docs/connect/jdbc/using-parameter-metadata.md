---
title: 매개 변수 메타 데이터를 사용 하 여 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: db2c1957-91c6-4989-a07b-9f8be6d2033a
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: e2c0e9f7589f58a1ef3c1cc5ee4026dd9eea5076
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66798570"
---
# <a name="using-parameter-metadata"></a>매개 변수 메타데이터 사용

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

[SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) 또는 [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) 개체가 가진 매개 변수에 대해 쿼리하기 위해 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]는 [SQLServerParameterMetaData](../../connect/jdbc/reference/sqlserverparametermetadata-class.md) 클래스를 구현합니다. 이 클래스에는 단일 값 형태로 정보를 반환하는 다양한 필드와 메서드가 들어 있습니다.

SQLServerParameterMetaData 개체를 만들려면 사용할 수 있습니다 합니다 [getParameterMetaData](../../connect/jdbc/reference/getparametermetadata-method-sqlserverpreparedstatement.md) SQLServerPreparedStatement 및 SQLServerCallableStatement 클래스의 메서드.

다음 예제에 대해 열린 연결을 여 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] SQLServerParameterMetaData 개체 및 반환할 다음 다양 한 SQLServerCallableStatement 클래스의 getParameterMetaData 메서드를 사용 하는, 샘플 데이터베이스 함수에 전달 SQLServerParameterMetaData 개체의 메서드는 형식 및 매개 변수 여 HumanResources.uspUpdateEmployeeHireInfo 저장 프로시저 내에 포함 된 모드에 대 한 정보를 표시할 사용 됩니다.

[!code[JDBC#UsingParamMetaData1](../../connect/jdbc/codesnippet/Java/using-parameter-metadata_1.java)]  

> [!NOTE]  
> SQLServerParameterMetaData 클래스를 사용 하 여 준비 된 문을 사용 하는 데는 몇 가지 제한이 있습니다.
>
> **SQL Server용 Microsoft JDBC Driver 6.0 이상 사용**: SQL Server 2008 또는 2008 R2를 사용하는 경우 SELECT, DELETE, INSERT 및 UPDATE 문에 하위 쿼리 및/또는 조인이 포함되지 않는 한 JDBC 드라이버에서 이러한 명령문을 지원합니다.

또한 SQL Server 2008 또는 2008 R2를 사용하는 경우 SQLServerParameterMetaData 클래스에 대해 쿼리 병합이 지원되지 않습니다. SQL Server 2012 이상 버전의 경우 복잡한 쿼리에서 매개 변수 메타데이터가 지원됩니다.

암호화 된 열에 대 한 매개 변수 메타 데이터 검색을 사용할 수 없습니다. **SQL Server용 Microsoft JDBC Driver 4.1 또는 4.2 사용**: SELECT, DELETE, INSERT 및 UPDATE 문에 하위 쿼리 및/또는 조인이 포함되지 않는 한 JDBC 드라이버에서 이러한 명령문을 지원합니다. 쿼리 병합은 또한 SQLServerParameterMetaData 클래스에 대해 지원 되지 않습니다.
