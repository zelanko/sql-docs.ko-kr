---
title: T-sql에서 "Hello World" 기본 R 코드 실행에 대 한 빠른 시작
description: SQL Server의 R 스크립트에 대 한 빠른 시작입니다. Hello 세계의 sp_execute_external_script 시스템 저장 프로시저를 사용 하 여 R 스크립트를 호출 하는 기본 사항에 대해 알아봅니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/04/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
ms.openlocfilehash: ab73e0231f462504652e0e1af62fed80c706f061
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/24/2019
ms.locfileid: "68469033"
---
# <a name="quickstart-hello-world-r-script-in-sql-server"></a>빠른 시작: SQL Server에서 "Hello 세계" R 스크립트 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

이 빠른 시작에서는 **sp_execute_external_script** 시스템 저장 프로시저를 소개 하 고 "Hello World" R 스크립트 INT-SQL을 실행 하 여 주요 개념에 대해 알아봅니다. 

## <a name="prerequisites"></a>사전 요구 사항

이전 퀵 스타트 인 [r이 SQL Server에 있는지 확인](quickstart-r-verify.md)하 고,이 빠른 시작에 필요한 r 환경을 설정 하기 위한 정보 및 링크를 제공 합니다.

## <a name="basic-r-interaction"></a>기본 R 상호 작용

SQL Database에서 R 코드를 실행 하는 방법에는 두 가지가 있습니다.

+ [Sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)시스템 저장 프로시저의 인수로 R 스크립트를 추가 합니다.
+ [원격 R 클라이언트](https://docs.microsoft.com/sql/advanced-analytics/r/set-up-a-data-science-client)에서 SQL database에 연결 하 고 SQL Database를 계산 컨텍스트로 사용 하 여 코드를 실행 합니다.

다음 연습은 첫 번째 상호 작용 모델에 초점을 맞추고 있습니다. 저장 프로시저에 R 코드를 전달 하는 방법입니다.

1. 간단한 스크립트를 실행 하 여 SQL 데이터베이스에서 R 스크립트를 실행 하는 방법을 확인 합니다.

    ```sql
    EXECUTE sp_execute_external_script
    @language = N'R',
    @script = N'
    a <- 1
    b <- 2
    c <- a/b
    d <- a*b
    print(c(c, d))
    '
    ```

2. 모든 것이 올바르게 설정 되었다고 가정 하면 올바른 결과가 계산 되며 R `print` 함수는 결과를 **메시지** 창에 반환 합니다.

    **결과**

    ```text
    STDOUT message(s) from external script: 
    0.5 2
    ```

    **Stdout** 메시지를 가져오는 것은 코드를 테스트할 때 유용 하지만, 응용 프로그램에서 사용 하거나 테이블에 쓸 수 있도록 결과를 테이블 형식으로 반환 해야 하는 경우가 더 많습니다. [빠른 시작: 자세한 내용은 SQL Server](rtsql-working-with-inputs-and-outputs.md) 에서 R을 사용 하 여 입력 및 출력을 처리 합니다.

`@script` 인수 내의 모든 항목은 유효한 R 코드 여야 합니다.

## <a name="run-a-hello-world-script"></a>Hello World 스크립트 실행

다음 연습은 또 다른 간단한 R 스크립트를 실행 합니다.

```sql
EXEC sp_execute_external_script
  @language =N'R',
  @script=N'OutputDataSet<-InputDataSet',
  @input_data_1 =N'SELECT 1 AS hello'
  WITH RESULT SETS (([Hello World] int));
GO
```

이 저장 프로시저에 대 한 입력은 다음과 같습니다.

+ *@language* 매개 변수는 호출할 언어 확장 (이 경우 R)을 정의 합니다.
+ *@script* 매개 변수는 R 런타임으로 전달 되는 명령을 정의 합니다. 전체 R 스크립트는 이 인수에 유니코드 텍스트로 포함되어야 합니다. **nvarchar** 형식의 변수에 텍스트를 추가한 다음 변수를 호출할 수도 있습니다.
+ *@input_data_1* 쿼리에서 반환 되는 데이터로, R 런타임으로 전달 되며 SQL Server 데이터를 데이터 프레임으로 반환 합니다.
+ WITH RESULT SETS 절은 SQL Server에 대해 반환 된 데이터 테이블의 스키마를 정의 하 고 데이터 형식 **에 대해 열** 이름으로 "Hello World"를 추가 합니다.

**결과**

| Hello World |
|-------------|
| 1 |

## <a name="next-steps"></a>다음 단계

몇 가지 간단한 R 스크립트를 실행 했으므로 입력 및 출력 구조를 좀 더 자세히 살펴보겠습니다.

> [!div class="nextstepaction"]
> [빠른 시작: 입력 및 출력 처리](quickstart-r-inputs-and-outputs.md)
