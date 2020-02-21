---
title: 저장 프로시저로 대규모 데이터 읽기 샘플 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 58c76635-a117-4661-8781-d6cb231c5809
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 924bcf388ddf74f3be3f4bb13f83e00789fb8777
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "69028302"
---
# <a name="reading-large-data-with-stored-procedures-sample"></a>저장 프로시저에서 대규모 데이터 읽기 샘플

[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

이 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 샘플 애플리케이션은 저장 프로시저에서 큰 OUT 매개 변수를 검색하는 방법을 보여 줍니다.

이 샘플의 코드 파일 이름은 ExecuteStoredProcedure.java이며 다음 위치에 있습니다.

```bash
\<installation directory>\sqljdbc_<version>\<language>\samples\adaptive
```

## <a name="requirements"></a>요구 사항

이 샘플 애플리케이션을 실행하려면 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] 샘플 데이터베이스에 대한 액세스 권한이 필요합니다. 또한 mssql-jdbc jar 파일을 포함하도록 클래스 경로를 설정해야 합니다. 클래스 경로를 설정하는 방법에 대한 자세한 내용은 [JDBC 드라이버 사용](../../../connect/jdbc/using-the-jdbc-driver.md)을 참조하세요.

> [!NOTE]  
> [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]는 기본 설정된 JRE(Java Runtime Environment)에 따라 사용할 수 있는 mssql-jdbc 클래스 라이브러리 파일을 제공합니다. 선택할 JAR 파일에 대한 자세한 내용은 [JDBC 드라이버 시스템 요구 사항](../../../connect/jdbc/system-requirements-for-the-jdbc-driver.md)을 참조하세요.

[!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] 샘플 데이터베이스에 다음 저장 프로시저를 만듭니다.

```sql
CREATE PROCEDURE GetLargeDataValue
  (@Document_ID int,
   @Document_ID_out int OUTPUT,
   @Document_Title varchar(50) OUTPUT,  
   @Document_Summary nvarchar(max) OUTPUT)  

AS
BEGIN
   SELECT @Document_ID_out = DocumentID,
          @Document_Title = Title,  
          @Document_Summary = DocumentSummary
    FROM  Production.Document  
    WHERE DocumentID = @Document_ID  
END  
```

## <a name="example"></a>예제

다음 예제의 샘플 코드에서는 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] 데이터베이스에 연결합니다. 그런 다음 샘플 데이터를 만들고 매개 변수가 있는 쿼리를 사용하여 Production.Document 테이블을 업데이트합니다. 그런 다음, [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 클래스의 [getResponseBuffering](../../../connect/jdbc/reference/getresponsebuffering-method-sqlserverstatement.md) 메서드를 사용하여 선택 버퍼링 모드를 가져오고 GetLargeDataValue 저장 프로시저를 실행합니다. JDBC 드라이버 버전 2.0 릴리스 이상에서는 기본적으로 responseBuffering 연결 속성이 "adaptive"로 설정됩니다.

마지막으로 샘플 코드는 OUT 매개 변수로 반환된 데이터를 표시하고 스트림에서 `mark` 및 `reset` 메서드를 사용하여 데이터의 부분을 다시 읽는 방법도 보여 줍니다.

[!code[JDBC#UsingAdaptiveBuffering2](../../../connect/jdbc/codesnippet/Java/reading-large-data-with-_1_1.java)]

## <a name="see-also"></a>참고 항목

[대규모 데이터 작업](../../../connect/jdbc/code-samples/working-with-large-data.md)
