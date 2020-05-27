---
title: 큰 데이터 읽기 샘플 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 6c986144-3854-4352-8331-e79eccbefc28
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 260666488a21b02c0c318d3277b72fc576b0ab08
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "69027818"
---
# <a name="reading-large-data-sample"></a>대규모 데이터 읽기 샘플

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

이 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 샘플 애플리케이션은 [getCharacterStream](../../connect/jdbc/reference/getcharacterstream-method-sqlserverresultset.md) 메서드를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에서 큰 단일 열 값을 검색하는 방법을 보여 줍니다.

이 샘플의 코드 파일 이름은 ReadLargeData.java이며 다음 위치에 있습니다.

```bash
\<installation directory>\sqljdbc_<version>\<language>\samples\adaptive
```

## <a name="requirements"></a>요구 사항

이 샘플 애플리케이션을 실행하려면 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 샘플 데이터베이스에 대한 액세스 권한이 필요합니다. 또한 mssql-jdbc jar 파일을 포함하도록 클래스 경로를 설정해야 합니다. 클래스 경로를 설정하는 방법에 대한 자세한 내용은 [JDBC 드라이버 사용](../../connect/jdbc/using-the-jdbc-driver.md)을 참조하세요.

> [!NOTE]  
> [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]는 기본 설정된 JRE(Java Runtime Environment)에 따라 사용할 수 있는 mssql-jdbc 클래스 라이브러리 파일을 제공합니다. 선택할 JAR 파일에 대한 자세한 내용은 [System Requirements for the JDBC Driver](../../connect/jdbc/system-requirements-for-the-jdbc-driver.md)(JDBC Driver 시스템 요구 사항)를 참조하세요.

## <a name="example"></a>예제

다음 예제의 샘플 코드에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 데이터베이스에 연결합니다. 그런 다음 샘플 데이터를 만들고 매개 변수가 있는 쿼리를 사용하여 Production.Document 테이블을 업데이트합니다.

또한 이 샘플 코드는 [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) 클래스의 [getResponseBuffering](../../connect/jdbc/reference/getresponsebuffering-method-sqlserverstatement.md) 메서드를 사용하여 적응 버퍼링 모드를 가져오는 방법도 보여 줍니다. JDBC 드라이버 버전 2.0 릴리스 이상에서는 기본적으로 responseBuffering 연결 속성이 "adaptive"로 설정됩니다.

그런 다음 [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) 개체와 함께 SQL 문을 사용하여 SQL 문을 실행하고 반환되는 데이터를 [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) 개체에 배치합니다.

끝으로 샘플 코드는 결과 집합에 있는 데이터 행을 반복하며, [getCharacterStream](../../connect/jdbc/reference/getcharacterstream-method-sqlserverresultset.md) 메서드를 사용하여 일부 데이터에 액세스합니다.

[!code[JDBC#UsingAdaptiveBuffering1](../../connect/jdbc/codesnippet/Java/reading-large-data-sample_1.java)]

## <a name="see-also"></a>참고 항목

[대규모 데이터 작업](../../connect/jdbc/working-with-large-data.md)
