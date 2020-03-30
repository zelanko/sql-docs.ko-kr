---
title: 매개 변수 메타데이터 사용 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: db2c1957-91c6-4989-a07b-9f8be6d2033a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 80ff8cebcc4141e8363c25f83821cb4924e6c46a
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "69026081"
---
# <a name="using-parameter-metadata"></a>매개 변수 메타데이터 사용

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

[SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) 또는 [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) 개체가 가진 매개 변수에 대해 쿼리하기 위해 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]는 [SQLServerParameterMetaData](../../connect/jdbc/reference/sqlserverparametermetadata-class.md) 클래스를 구현합니다. 이 클래스에는 단일 값 형태로 정보를 반환하는 다양한 필드와 메서드가 들어 있습니다.

SQLServerParameterMetaData 개체를 만들려면 SQLServerPreparedStatement 및 SQLServerCallableStatement 클래스의 [getParameterMetaData](../../connect/jdbc/reference/getparametermetadata-method-sqlserverpreparedstatement.md) 메서드를 사용할 수 있습니다.

다음 예제에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 샘플 데이터베이스에 대한 열린 연결이 함수에 전달되고, SQLServerCallableStatement 클래스의 getParameterMetaData 메서드를 사용하여 SQLServerParameterMetaData 개체를 반환하며, 그 후 SQLServerParameterMetaData 개체의 다양한 메서드를 사용하여 HumanResources.uspUpdateEmployeeHireInfo 저장 프로시저 내에 포함된 매개 변수의 형식과 모드에 대한 정보를 표시합니다.

[!code[JDBC#UsingParamMetaData1](../../connect/jdbc/codesnippet/Java/using-parameter-metadata_1.java)]  

> [!NOTE]  
> SQLServerParameterMetaData 클래스를 준비된 문과 함께 사용할 때는 몇 가지 제한 사항이 있습니다.
>
> **SQL Server용 Microsoft JDBC Driver 6.0 이상 사용**: SQL Server 2008 또는 2008 R2를 사용하는 경우 SELECT, DELETE, INSERT 및 UPDATE 문에 하위 쿼리 및/또는 조인이 포함되지 않는 한 JDBC 드라이버에서 이러한 명령문을 지원합니다.

또한 SQL Server 2008 또는 2008 R2를 사용하는 경우 SQLServerParameterMetaData 클래스에 대해 쿼리 병합이 지원되지 않습니다. SQL Server 2012 이상 버전의 경우 복잡한 쿼리에서 매개 변수 메타데이터가 지원됩니다.

암호화된 열에 대한 매개 변수 메타데이터 검색은 지원되지 않습니다. **SQL Server용 Microsoft JDBC Driver 4.1 또는 4.2 사용**: SELECT, DELETE, INSERT 및 UPDATE 문에 하위 쿼리 및/또는 조인이 포함되지 않는 한 JDBC 드라이버에서 이러한 명령문을 지원합니다. MERGE 쿼리는 SQLServerParameterMetaData 클래스에서 지원되지 않습니다.
