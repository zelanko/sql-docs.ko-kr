---
title: T-sql에서 "Hello World" 기본 Python 코드 실행에 대 한 빠른 시작
description: SQL Server의 Python 스크립트에 대 한 빠른 시작입니다. Hello 세계의 sp_execute_external_script 시스템 저장 프로시저를 사용 하 여 Python 스크립트를 호출 하는 기본 사항에 대해 알아봅니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/10/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: a170bd2ee3e893a83ebb9d3201ee117321e7562b
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/01/2019
ms.locfileid: "68714819"
---
# <a name="quickstart-hello-world-python-script-in-sql-server"></a>빠른 시작: SQL Server에서 "Hello 세계" Python 스크립트 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

이 빠른 시작에서는 **sp_execute_external_script** 시스템 저장 프로시저를 소개 하 고 "Hello World" Python 스크립트 INT-SQL을 실행 하 여 주요 개념을 알아봅니다. 

## <a name="prerequisites"></a>사전 요구 사항

이전 퀵 스타트 인 [SQL Server에 python이 있는지 확인](quickstart-python-verify.md)하 고,이 빠른 시작에 필요한 python 환경을 설정 하기 위한 정보 및 링크를 제공 합니다.

## <a name="basic-python-interaction"></a>기본 Python 상호 작용

SQL Server에서 Python 코드를 실행 하는 방법에는 두 가지가 있습니다.

+ 시스템 저장 프로시저 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)의 인수로 Python 스크립트를 추가 합니다.

+ [원격 Python 클라이언트](../python/setup-python-client-tools-sql.md)에서 SQL Server에 연결 하 고 SQL Server를 계산 컨텍스트로 사용 하 여 코드를 실행 합니다. 이렇게 하려면 [revoscalepy](../python/ref-py-revoscalepy.md)가 필요 합니다.

다음 연습은 첫 번째 상호 작용 모델: Python 코드를 저장 프로시저에 전달 하는 방법에 중점을 두었습니다.

1. 몇 가지 간단한 코드를 실행 하 여 SQL Server와 Python 간에 데이터가 전달 되는 방식을 확인 합니다.

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

2. 모든 것이 올바르게 설정 되어 있고 python과 SQL Server가 서로 통신 하 고 있는 것으로 가정 하면 올바른 결과가 계산 되며 python `print` 함수는 결과를 **메시지** 창에 반환 합니다.

    **결과**

    ```text
    STDOUT message(s) from external script: 
    0.5 2
    ```

    코드를 테스트할 때 **stdout** 메시지를 사용 하는 것이 편리 하지만 응용 프로그램에서 사용 하거나 테이블에 쓸 수 있도록 결과를 테이블 형식으로 반환 해야 하는 경우가 더 많습니다.

지금은 다음 규칙을 염두에 두어야 합니다.

+ `@script` 인수 내의 모든 항목은 유효한 Python 코드 여야 합니다. 
+ 코드는 들여쓰기, 변수 이름 등에 대 한 모든 Python 규칙을 따라야 합니다. 오류가 발생 하면 공백과 대/소문자를 확인 합니다.
+ 프로그래밍 언어 중에서 Python은 작은따옴표와 큰따옴표를 고려 하 여 가장 유연한 방법 중 하나입니다. 매우 다양 한 상호 교환이 가능 합니다. 그러나 t-sql은 특정 작업에 대해서만 작은따옴표를 사용 하 고 인수는 `@script` 작은따옴표를 사용 하 여 Python 코드를 유니코드 문자열로 묶습니다. 따라서 Python 코드를 검토 하 고 일부 작은따옴표를 큰따옴표로 변경 해야 할 수 있습니다.
+ 기본적으로 로드 되지 않는 라이브러리를 사용 하는 경우 스크립트의 시작 부분에 import 문을 사용 하 여 로드 해야 합니다. SQL Server 여러 제품별 라이브러리를 추가 합니다. 자세한 내용은 [Python 라이브러리](../python/python-libraries-and-data-types.md)를 참조 하세요.
+ 라이브러리가 아직 설치 되지 않은 경우 여기에 설명 된 대로 SQL Server 외부에서 Python 패키지를 중지 하 고 설치 합니다. [SQL Server에 새로운 Python 패키지 설치](../python/install-additional-python-packages-on-sql-server.md)

## <a name="run-a-hello-world-script"></a>Hello World 스크립트 실행

다음 연습은 또 다른 간단한 Python 스크립트를 실행 합니다.

```sql
EXEC sp_execute_external_script
@language =N'Python',
@script=N'OutputDataSet = InputDataSet',
@input_data_1 =N'SELECT 1 AS hello'
WITH RESULT SETS (([Hello World] int));
GO
```

이 저장 프로시저에 대 한 입력은 다음과 같습니다.

+ *@language* 매개 변수는 호출할 언어 확장 (이 경우 Python)을 정의 합니다.
+ *@script* 매개 변수는 Python 런타임으로 전달 되는 명령을 정의 합니다. 전체 Python 스크립트는이 인수에 유니코드 텍스트로 묶어야 합니다. **nvarchar** 형식의 변수에 텍스트를 추가한 다음 변수를 호출할 수도 있습니다.
+ *@input_data_1* 쿼리에서 반환 되는 데이터로, Python 런타임으로 전달 되며 SQL Server 데이터를 데이터 프레임으로 반환 합니다.
+ WITH RESULT SETS 절은 SQL Server에 대해 반환 된 데이터 테이블의 스키마를 정의 하 고 데이터 형식 **에 대해 열** 이름으로 "Hello World"를 추가 합니다.

**결과**

| Hello World |
|-------------|
| 1 |

## <a name="next-steps"></a>다음 단계

몇 가지 간단한 Python 스크립트를 실행 했으므로 이제 입력 및 출력 구조를 자세히 살펴보겠습니다.

> [!div class="nextstepaction"]
> [빠른 시작: 입력 및 출력 처리](quickstart-python-inputs-and-outputs.md)
