---
title: 데이터베이스 메타데이터 사용 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 8b048371-e912-4ed1-afd7-436978f48888
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fce2bf9d72136b303ee3bc974f3aede313233a82
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "69026426"
---
# <a name="using-database-metadata"></a>데이터베이스 메타데이터 사용

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]는 데이터베이스에서 지원하는 사항에 대한 정보를 쿼리하기 위해 [SQLServerDatabaseMetaData](../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md) 클래스를 구현합니다. 이 클래스에는 단일 값 형태 또는 결과 집합으로 정보를 반환하는 다양한 메서드가 들어 있습니다.

SQLServerDatabaseMetaData 개체를 만들려면 [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) 클래스의 [getMetaData](../../connect/jdbc/reference/getmetadata-method-sqlserverconnection.md) 메서드를 사용하여 연결된 데이터베이스에 관한 정보를 가져옵니다.

다음 예제에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 샘플 데이터베이스에 대해 열린 연결을 함수로 전달하고, SQLServerConnection 클래스의 getMetaData 메서드를 사용하여 SQLServerDatabaseMetadata 개체를 반환한 다음, SQLServerDatabaseMetaData 개체의 다양한 메서드를 사용하여 드라이버, 드라이버 버전, 데이터베이스 이름 및 데이터베이스 버전에 관한 정보를 표시합니다.

[!code[JDBC#UsingDBMetaData1](../../connect/jdbc/codesnippet/Java/using-database-metadata_1.java)]

## <a name="see-also"></a>참고 항목

[JDBC 드라이버로 메타데이터 처리](../../connect/jdbc/handling-metadata-with-the-jdbc-driver.md)
