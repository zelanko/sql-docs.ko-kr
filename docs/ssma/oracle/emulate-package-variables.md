---
title: Oracle 패키지 변수 에뮬레이트
description: Oracle 용 SSMA (SQL Server Migration Assistant)에서 SQL Server의 Oracle 패키지 변수를 에뮬레이트하는 방법에 대해 설명 합니다.
authors: nahk-ivanov
ms.service: ssma
ms.devlang: sql
ms.topic: article
ms.date: 1/22/2020
ms.author: alexiva
ms.openlocfilehash: 9a8ca5c7dfdda98e1c005c3851d061957cf67449
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "76762827"
---
# <a name="emulating-oracle-package-variables"></a>Oracle 패키지 변수 에뮬레이트

Oracle은 패키지에 변수, 형식, 저장 프로시저 및 함수를 캡슐화 하는 것을 지원 합니다. Oracle 패키지를 변환 하는 경우 다음을 변환 해야 합니다.

* 프로시저 및 함수-공용 및 개인
* variables
* 커서
* 초기화 루틴

이 문서에서는 Oracle 용 SSMA (SQL Server Migration Assistant)에서 패키지 변수를 SQL Server으로 변환 하는 방법을 설명 합니다.

## <a name="conversion-basics"></a>변환 기본 사항

패키지 변수를 저장 하기 위해 Oracle 용 SSMA는 `ssma_oracle` `ssma_oracle.db_storage` 테이블과 함께 특수 스키마에 상주 하는 저장 프로시저를 사용 합니다. 이 테이블은 (세션 `SPID` 식별자)와 로그인 시간을 기준으로 필터링 됩니다. 이 필터링을 사용 하면 서로 다른 세션의 변수를 구분할 수 있습니다.

각 변환 된 패키지의 시작 부분에서 SSMA는 `ssma_oracle.db_check_init_package` 특수 프로시저를 호출 합니다 .이 프로시저는 패키지가 초기화 되었는지 확인 하 고 필요한 경우 초기화 합니다. 각 초기화 프로시저는 저장소 테이블을 정리 하 고 각 패키지 변수에 대 한 기본값을 설정 합니다.

## <a name="example"></a>예제

여러 패키지 변수를 변환 하는 경우 다음 예제를 참조 하세요.

```sql
CREATE OR REPLACE PACKAGE MY_PACKAGE
IS
    space varchar(1) := ' ';
    unitname varchar(128) := 'My Simple Package';
    ts date := sysdate;
END;
```

SSMA는 다음 Transact-sql 코드로 변환 합니다.

```sql
CREATE PROCEDURE dbo.MY_PACKAGE$SSMA_Initialize_Package
AS
BEGIN
    EXECUTE ssma_oracle.db_clean_storage

    EXECUTE ssma_oracle.set_pv_varchar
        DB_NAME(),
        'DBO',
        'MY_PACKAGE',
        'SPACE',
        ' '

    EXECUTE ssma_oracle.set_pv_varchar
        DB_NAME(),
        'DBO',
        'MY_PACKAGE',
        'UNITNAME',
        'My Simple Package'

    DECLARE
        @temp datetime2

    SET @temp = sysdatetime()

    EXECUTE sysdb.ssma_oracle.set_pv_datetime2
      DB_NAME(),
      'DBO',
      'MY_PACKAGE',
      'TS',
      @temp
END
```

## <a name="emulating-get-and-set-methods-for-package-variables"></a>패키지 변수에 대 한 Get 및 Set 메서드 에뮬레이트

Oracle은 `Get` 패키지 `Set` 변수에 대해 및 메서드를 사용 하 여 다른 subprograms 읽기 및 쓰기를 직접 허용 하지 않도록 합니다. 동일한 세션에서 subprogram 호출 사이에 일부 변수를 사용할 수 있도록 해야 하는 요구 사항이 있는 경우 이러한 변수는 전역 변수와 같은 방식으로 처리 됩니다.

이 범위 지정 규칙을 해결 하기 위해 Oracle 용 SSMA는 각 `ssma_oracle.set_pv_varchar` 변수 형식에 대해와 같은 저장 프로시저를 사용 합니다. 이러한 변수에 액세스 하기 위해 SSMA는 트랜잭션 독립적인 `get_*` 및 `set_*` 프로시저와 함수 집합을 사용 합니다.

| Oracle의 데이터 형식 | SSMA `Set` 프로시저           |
| ------------------- | ------------------------------ |
| VARCHAR             | `ssma_oracle.set_pv_varchar`   |
| DATE                | `ssma_oracle.set_pv_datetime2` |
| CHAR                | `ssma_oracle.set_pv_varchar`   |
| INT                 | `ssma_oracle.set_pv_float`     |
| FLOAT               | `ssma_oracle.set_pv_float`     |

다른 세션의 변수를 구분 하기 위해 SSMA는 해당 `SPID` (세션 식별자) 및 세션의 로그인 시간과 함께 변수를 저장 합니다. 따라서 및 `get_*` `set_*` 프로시저는 변수를 실행 하는 세션과 독립적인 변수를 유지 합니다.
