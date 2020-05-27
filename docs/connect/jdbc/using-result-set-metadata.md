---
title: 결과 집합 메타데이터 사용 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 5e37529a-30db-48c8-b90a-ae9657d0f6b0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0ed0b1eedcafa1fab59d17f756523fc0fc189200
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "69026119"
---
# <a name="using-result-set-metadata"></a>결과 집합 메타데이터 사용

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]는 결과 집합에 포함된 열 관련 정보를 쿼리하기 위해 [SQLServerResultSetMetaData](../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md) 클래스를 구현합니다. 이 클래스에는 단일 값 형태로 정보를 반환하는 다양한 메서드가 들어 있습니다.

SQLServerResultSetMetaData 개체를 만들려면 [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) 클래스의 [getMetaData](../../connect/jdbc/reference/getmetadata-method-sqlserverresultset.md) 메서드를 사용하면 됩니다.

다음 예제에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 샘플 데이터베이스에 대한 열린 연결을 함수로 전달하고, SQLServerResultSet 클래스의 getMetaData 메서드를 사용하여 SQLServerResultSetMetaData 개체를 반환한 다음, SQLServerResultSetMetaData 개체의 다양한 메서드를 사용하여 결과 집합에 포함된 열의 이름 및 데이터 형식에 관한 정보를 표시합니다.

[!code[JDBC#UsingResultSetMetaData1](../../connect/jdbc/codesnippet/Java/using-result-set-metadata_1.java)]

## <a name="see-also"></a>참고 항목

[JDBC 드라이버로 메타데이터 처리](../../connect/jdbc/handling-metadata-with-the-jdbc-driver.md)
