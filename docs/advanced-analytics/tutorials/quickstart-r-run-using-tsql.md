---
title: "\"Hello World\" 기본 R 코드 실행을 T-SQL-SQL Server Machine Learning에에서 대 한 빠른 시작"
description: SQL Server에서 R 스크립트에 대 한 빠른 시작입니다. Sp_execute_external_script 시스템 저장 프로시저를 사용 하 여 hello world 연습에서 R 스크립트를 호출 하는 기본 사항을 알아봅니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/04/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 1ec9580a533e51b7e99ea0ac34c1d322a27da452
ms.sourcegitcommit: 3cfedfeba377560d460ca3e42af1e18824988c07
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/05/2019
ms.locfileid: "59042282"
---
# <a name="quickstart-hello-world-r-script-in-sql-server"></a>빠른 시작: SQL Server에서 R 스크립트의 "hello world" 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 빠른 시작에 알아봅니다 "Hello World" R을 실행 하 여 주요 개념 소개를 사용 하 여 inT SQL 스크립트를 **sp_execute_external_script** 시스템 저장 프로시저입니다. 

## <a name="prerequisites"></a>사전 요구 사항

이전 빠른 시작에서는 [SQL Server에 있는지 확인 하는 R](quickstart-r-verify.md), 정보를 제공 하 고이 빠른 시작에 필요한 R 환경 설정에 대 한 링크입니다.

## <a name="basic-r-interaction"></a>기본 R 상호 작용

두 가지 방법으로 SQL Database에서 R 코드를 실행할 수 있습니다.

+ 시스템 저장 프로시저의 인수로 R 스크립트를 추가 [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)합니다.
+ [원격 R 클라이언트](https://docs.microsoft.com/sql/advanced-analytics/r/set-up-a-data-science-client)SQL 데이터베이스에 연결한 후 SQL Database를 사용 하 여 계산 컨텍스트로 코드를 실행 합니다.

다음 연습에서는 첫 번째 상호 작용 모델에 포커스가: 저장된 프로시저에 R 코드를 전달 하는 방법입니다.

1. SQL database에서 R 스크립트를 실행 하는 방법을 참조 하세요. 간단한 스크립트를 실행 합니다.

    ```sql
    EXECUTE sp_execute_external_script
    @language = N'R',
    @script = N'
    a <- 1
    b <- 2
    c <- a/b
    d <- a*b
    print(c(c, d))'
    '
    ```

2. 있다고 간주 되며 올바른 결과 올바르게 설정 하는 모든 계산 및 R `print` 함수는 결과 반환 합니다 **메시지** 창입니다.

    **결과**

    ```text
    STDOUT message(s) from external script: 
    0.5 2
    ```

    가져오는 동안 **stdout** 메시지 코드를 테스트할 때 유용 합니다 더 자주 해야 응용 프로그램에서 사용 하거나 테이블에 쓸 수 있도록 테이블 형식으로 결과 반환 합니다. 참조 [빠른 시작: 핸들 입력 및 SQL Server에서 R을 사용 하 여 출력](rtsql-working-with-inputs-and-outputs.md) 자세한 내용은 합니다.

내부의 모든 항목이 기억 합니다 `@script` 인수에 유효한 R 코드 여야 합니다.

## <a name="run-a-hello-world-script"></a>Hello World 스크립트를 실행 합니다.

다음 연습에서는 다른 간단한 R 스크립트를 실행합니다.

```sql
EXEC sp_execute_external_script
  @language =N'R',
  @script=N'OutputDataSet<-InputDataSet',
  @input_data_1 =N'SELECT 1 AS hello'
  WITH RESULT SETS (([Hello World] int));
GO
```

이 저장된 프로시저에 대 한 입력은 다음과 같습니다.

+ *@language* 이 경우 R.를 호출 하려면 언어 확장을 정의 하는 매개 변수
+ *@script* 매개 변수를 R 런타임에 전달할 명령을 정의 합니다. 전체 R 스크립트는 이 인수에 유니코드 텍스트로 포함되어야 합니다. **nvarchar** 형식의 변수에 텍스트를 추가한 다음 변수를 호출할 수도 있습니다.
+ *@input_data_1* 데이터를 SQL Server 데이터 프레임으로 데이터를 반환 하는 R 런타임에 전달할 쿼리에 의해 반환 됩니다.
+ WITH RESULT SETS 절 열 이름으로 "Hello World"를 추가 하 고 SQL Server에 대해 반환된 된 데이터 테이블의 스키마를 정의 **int** 데이터 형식에 대 한 합니다.

**결과**

| 전 세계 여러분 안녕하세요 |
|-------------|
| 1 |

## <a name="next-steps"></a>다음 단계

몇 가지 간단한 R 스크립트를 실행 하면 이제는 살펴볼에서 입력 및 출력을 구성 합니다.

> [!div class="nextstepaction"]
> [빠른 시작: 입력 및 출력 처리](quickstart-r-inputs-and-outputs.md)
