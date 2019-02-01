---
title: "\"Hello World\" 기본 Python에 대 한 빠른 시작 코드 T-SQL-SQL Server Machine Learning의 실행"
description: SQL Server의 Python 스크립트에 대 한 빠른 시작입니다. Sp_execute_external_script 시스템 저장 프로시저를 사용 하 여 hello world 연습에서 하는 Python 스크립트를 호출 하는 기본 사항을 알아봅니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/11/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: fb05e3b04fe9d6f33389e249d189baa7cc093016
ms.sourcegitcommit: 032273bfbc240fe22ac6c1f6601a14a6d99573f7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2019
ms.locfileid: "55513773"
---
# <a name="quickstart-hello-world-python-script-in-sql-server"></a>빠른 시작: SQL Server에서 "hello world" Python 스크립트 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 빠른 시작에 알아봅니다 "Hello World" Python을 실행 하 여 주요 개념 소개를 사용 하 여 inT SQL 스크립트를 **sp_execute_external_script** 시스템 저장 프로시저입니다. 

## <a name="prerequisites"></a>사전 요구 사항

이전 빠른 시작에서는 [SQL Server에 있는지 확인 하는 Python](quickstart-python-verify.md), 정보를 제공 하 고이 빠른 시작에 필요한 Python 환경을 설정 하는 것에 대 한 링크입니다.

## <a name="basic-python-interaction"></a>기본 Python 상호 작용

두 가지 방법으로 SQL Server에서 Python 코드를 실행할 수 있습니다.

+ 시스템 저장 프로시저의 인수로 서 Python 스크립트를 추가 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)합니다.

+ [원격 Python 클라이언트](../python/setup-python-client-tools-sql.md)SQL Server에 연결한 후 SQL Server 계산 컨텍스트로 사용 하 여 코드를 실행 합니다. 그러려면 [revoscalepy](../python/ref-py-revoscalepy.md)합니다.

다음 연습에서는 첫 번째 상호 작용 모델에 포커스가: 저장된 프로시저에 Python 코드를 전달 하는 방법입니다.

1. 데이터는 SQL Server와 Python 간에 앞뒤로 전달 하는 방법을 확인 하려면 몇 가지 간단한 코드를 실행 합니다.

    ```sql
    execute sp_execute_external_script 
    @language = N'Python', 
    @script = N'
    a = 1
    b = 2
    c = a/b
    d = a*b
    print(c, d)
    '
    ```

2. 올바르게 설정 완벽 하 게 하 고 서로 Python 및 SQL Server와 통신 하는 경우 올바른 결과 계산 하 고 Python `print` 함수 결과 반환 합니다 **메시지** windows.

    **결과**

    ```text
    STDOUT message(s) from external script: 
    0.5 2
    ```

    가져오는 동안 **stdout** 메시지 코드를 테스트할 때 유용 합니다 더 자주 해야 응용 프로그램에서 사용 하거나 테이블에 쓸 수 있도록 테이블 형식으로 결과 반환 합니다.

이제 이러한 규칙에 유의 하십시오.

+ 내의 모든 항목을 `@script` 인수는 유효한 Python 코드 여야 합니다. 
+ 코드는 들여쓰기, 변수 이름 등 관련 된 모든 Python 규칙을 따라야 합니다. 오류가 발생 하는 경우 공백 및 대/소문자를 확인 합니다.
+ Python은 가장 유연한 중 프로그래밍 언어 중에서 작은따옴표 및 큰따옴표;와 관련 하 여 해당 정책은 거의 서로 바꿔 사용할 수 있습니다. 그러나 T-SQL가 작은따옴표를 사용 하 여 특정 항목에 대 한 및 `@script` 인수 작은따옴표를 사용 하 여 유니코드 문자열로 Python 코드를 묶습니다. 따라서 Python 코드를 검토 하 고 큰따옴표를 작은따옴표로 일부 변경 해야 합니다.
+ 기본적으로 로드 되지 않은 모든 라이브러리를 사용 하는 경우 로드 하는 데 스크립트의 시작 부분에 import 문을 사용 해야 합니다. SQL Server는 여러 제품 관련 라이브러리를 추가합니다. 자세한 내용은 [Python 라이브러리](../python/python-libraries-and-data-types.md)합니다.
+ 라이브러리에 이미 설치 되어 있지 않으면, 중지 하 고 여기에 설명 된 대로 SQL Server 외부 Python 패키지를 설치 합니다. [SQL Server에 새로운 Python 패키지 설치](../python/install-additional-python-packages-on-sql-server.md)

## <a name="run-a-hello-world-script"></a>Hello World 스크립트를 실행 합니다.

다음 연습에서는 다른 간단한 Python 스크립트를 실행합니다.

```sql
EXEC sp_execute_external_script
@language =N'Python',
@script=N'OutputDataSet = InputDataSet',
@input_data_1 =N'SELECT 1 AS hello'
WITH RESULT SETS (([Hello World] int));
GO
```

이 저장된 프로시저에 대 한 입력은 다음과 같습니다.

+ *@language* 이 경우 Python를 호출 하려면 언어 확장을 정의 하는 매개 변수입니다.
+ *@script* 매개 변수는 Python 런타임에 전달 되는 명령을 정의 합니다. 전체 Python 스크립트는 유니코드 텍스트로이 인수에 묶어야 합니다. **nvarchar** 형식의 변수에 텍스트를 추가한 다음 변수를 호출할 수도 있습니다.
+ *@input_data_1* 데이터를 SQL Server 데이터 프레임으로 데이터를 반환 하는 Python 런타임에서 전달할 쿼리에 의해 반환 됩니다.
+ WITH RESULT SETS 절 열 이름으로 "Hello World"를 추가 하 고 SQL Server에 대해 반환된 된 데이터 테이블의 스키마를 정의 **int** 데이터 형식에 대 한 합니다.

**결과**

| 전 세계 여러분 안녕하세요 |
|-------------|
| 1 |

## <a name="next-steps"></a>다음 단계

몇 가지 간단한 Python 스크립트를 실행 하면 했으므로 자세히 살펴보겠습니다에서 입력 및 출력을 구성 합니다.

> [!div class="nextstepaction"]
> [빠른 시작: 입 / 출력 처리](quickstart-python-inputs-and-outputs.md)
