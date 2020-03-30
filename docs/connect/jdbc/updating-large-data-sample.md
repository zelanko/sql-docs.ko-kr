---
title: 큰 데이터 업데이트 샘플 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 76ecc05f-a77d-40a2-bab9-91a7fcf17347
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 231125f60ec0c5791e55a10cff56b3b93339fb91
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "69027067"
---
# <a name="updating-large-data-sample"></a>큰 데이터 업데이트 샘플

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

이 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 샘플 애플리케이션에서는 데이터베이스의 큰 열을 업데이트하는 방법을 보여 줍니다.

이 샘플의 코드 파일 이름은 updateLargeData.java이며 다음 위치에 있습니다.

```bash
\<installation directory>\sqljdbc_<version>\<language>\samples\adaptive
```

## <a name="requirements"></a>요구 사항

이 샘플 애플리케이션을 실행하려면 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 샘플 데이터베이스에 대한 액세스 권한이 필요합니다. 또한 sqljdbc4.jar 파일을 포함하도록 클래스 경로를 설정해야 합니다. 클래스 경로에 sqljdbc4.jar 파일에 대한 항목이 없으면 샘플 애플리케이션에서 일반적인 &quot;클래스를 찾을 수 없습니다.&quot; 예외가 발생합니다. 클래스 경로를 설정하는 방법에 대한 자세한 내용은 [JDBC 드라이버 사용](../../connect/jdbc/using-the-jdbc-driver.md)을 참조하세요.

> [!NOTE]  
> [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]는 기본 설정된 JRE(Java Runtime Environment)에 따라 사용할 수 있는 sqljdbc.jar, sqljdbc4.jar, sqljdbc41.jar 또는 sqljdbc42.jar 클래스 라이브러리 파일을 제공합니다. 이 샘플에서는 JDBC 4.0 API에 도입된 [isWrapperFor](../../connect/jdbc/reference/iswrapperfor-method-sqlserverstatement.md) 및 [unwrap](../../connect/jdbc/reference/unwrap-method-sqlserverstatement.md) 메서드를 사용하여 드라이버 관련 응답 버퍼링 메서드에 액세스합니다. 이 샘플을 컴파일하고 실행하려면 JDBC 4.0을 지원하는 sqljdbc4.jar 클래스 라이브러리가 있어야 합니다. 선택할 JAR 파일에 대한 자세한 내용은 [System Requirements for the JDBC Driver](../../connect/jdbc/system-requirements-for-the-jdbc-driver.md)(JDBC Driver 시스템 요구 사항)를 참조하세요.

## <a name="example"></a>예제

다음 예제의 샘플 코드에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 데이터베이스에 연결합니다. 그런 다음, Statement 개체를 만들고 [isWrapperFor](../../connect/jdbc/reference/iswrapperfor-method-sqlserverstatement.md) 메서드를 사용하여 Statement 개체가 지정된 [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) 클래스의 래퍼인지 확인합니다. [unwrap](../../connect/jdbc/reference/unwrap-method-sqlserverstatement.md) 메서드는 드라이버 관련 응답 버퍼링 메서드에 액세스하는 데 사용됩니다.

다음으로, 샘플 코드는 **SQLServerStatement** 클래스의 [setResponseBuffering](../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md) 메서드를 사용하여 응답 버퍼링 모드를 “[adaptive](../../connect/jdbc/reference/sqlserverstatement-class.md)”로 설정하고 적응 버퍼링 모드를 가져오는 방법도 보여 줍니다.

그런 다음, SQL 문을 실행하고 반환된 데이터를 업데이트 가능한 [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) 개체에 배치합니다.

마지막으로 샘플 코드는 결과 집합에 있는 데이터 행을 반복합니다. 빈 문서 요약이 발견되면 [updateString](../../connect/jdbc/reference/updatestring-method-sqlserverresultset.md) 및 [updateRow](../../connect/jdbc/reference/updaterow-method-sqlserverresultset.md) 메서드 조합을 사용하여 데이터 행을 업데이트하고 데이터베이스에 다시 보관합니다. 이미 데이터가 있으면 [getString](../../connect/jdbc/reference/getstring-method-sqlserverresultset.md) 메서드를 사용하여 포함된 데이터 일부를 표시합니다.

드라이버의 기본 동작은 “**adaptive**”입니다. 그러나 정방향 전용 업데이트 가능 결과 집합의 경우 및 결과 집합의 데이터가 애플리케이션 메모리보다 큰 경우에는 애플리케이션에서 [SQLServerStatement](../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md) 클래스의 [setResponseBuffering](../../connect/jdbc/reference/sqlserverstatement-class.md) 메서드를 사용하여 명시적으로 적응 버퍼링 모드를 설정해야 합니다.

[!code[JDBC#UsingAdaptiveBuffering3](../../connect/jdbc/codesnippet/Java/updating-large-data-sample_1.java)]

## <a name="see-also"></a>참고 항목

[대규모 데이터 작업](../../connect/jdbc/working-with-large-data.md)
