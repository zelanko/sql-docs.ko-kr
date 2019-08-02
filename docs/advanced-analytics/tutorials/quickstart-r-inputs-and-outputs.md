---
title: R에서 입력 및 출력 작업에 대 한 빠른 시작
description: SQL Server에서 R 스크립트에 대 한이 빠른 시작에서는 sp_execute_external_script 시스템 저장 프로시저에 대 한 입력 및 출력 구조를 구성 하는 방법에 대해 알아봅니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/04/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 75de63ef960c205545db5229f22a437c70b350b9
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/01/2019
ms.locfileid: "68714790"
---
# <a name="quickstart-handle-inputs-and-outputs-using-r-in-sql-server"></a>빠른 시작: SQL Server에서 R을 사용 하 여 입력 및 출력 처리
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

이 빠른 시작에서는 SQL Server Machine Learning Services 또는 R Services에서 R을 사용할 때 입력 및 출력을 처리 하는 방법을 보여 줍니다.

SQL Server에서 R 코드를 실행 하려는 경우에는 저장 프로시저에서 R 스크립트를 래핑해야 합니다. 하나를 작성 하거나 R 스크립트를 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)에 전달할 수 있습니다. 이 시스템 저장 프로시저는 데이터를 R로 전달 하 고, R 사용자 세션을 안전 하 게 관리 하 고, 결과를 클라이언트에 반환 하는 SQL Server 컨텍스트에서 R 런타임을 시작 하는 데 사용 됩니다.

기본적으로 [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) 는 단일 입력 데이터 집합을 허용 합니다 .이 데이터 집합은 일반적으로 유효한 SQL 쿼리 형식으로 제공 됩니다. 다른 형식의 입력은 SQL 변수로 전달 될 수 있습니다.

저장 프로시저는 단일 R 데이터 프레임을 출력으로 반환 하지만 스칼라 및 모델을 변수로 출력할 수도 있습니다. 예를 들어 학습 된 모델을 이진 변수로 출력 하 고 T-sql INSERT 문에 전달 하 여 해당 모델을 테이블에 쓸 수 있습니다. 플롯 (이진 형식) 또는 스칼라 (날짜 및 시간, 모델 학습에 경과 된 시간 등)를 생성할 수도 있습니다.

## <a name="prerequisites"></a>사전 요구 사항

이전 퀵 스타트 인 [r이 SQL Server에 있는지 확인](quickstart-r-verify.md)하 고,이 빠른 시작에 필요한 r 환경을 설정 하기 위한 정보 및 링크를 제공 합니다.

## <a name="create-the-source-data"></a>원본 데이터 만들기

다음 T-sql 문을 실행 하 여 작은 테스트 데이터 테이블을 만듭니다.

```sql
CREATE TABLE RTestData (col1 INT NOT NULL)
INSERT INTO RTestData VALUES (1);
INSERT INTO RTestData VALUES (10);
INSERT INTO RTestData VALUES (100);
GO
```

테이블을 만들었으면 다음 문을 사용하여 테이블을 쿼리합니다.
  
```sql
SELECT * FROM RTestData
```

**결과**

![RTestData 테이블의 내용](./media/select-rtestdata.png)

## <a name="inputs-and-outputs"></a>입/출력

Sp_execute_external_script: `InputDataSet` 및 `OutputDataSet`의 기본 입력 및 출력 변수를 살펴보겠습니다.

1. R 스크립트에 대 한 입력으로 테이블에서 데이터를 가져올 수 있습니다. 아래 문을 실행 합니다. 테이블에서 데이터를 가져오고, R 런타임을 통해 라운드트립 하 고, 열 이름이 *NewColName*인 값을 반환 합니다.

    쿼리에서 반환 되는 데이터는 R 런타임으로 전달 되며 데이터 프레임으로 SQL Database 데이터를 반환 합니다. WITH RESULT SETS 절은 SQL Database에 대해 반환 된 데이터 테이블의 스키마를 정의 합니다.

    ```sql
    EXECUTE sp_execute_external_script
        @language = N'R'
        , @script = N'OutputDataSet <- InputDataSet;'
        , @input_data_1 = N'SELECT * FROM RTestData;'
    WITH RESULT SETS (([NewColName] INT NOT NULL));
    ```

    **결과**

    ![테이블에서 데이터를 반환 하는 R 스크립트의 출력](./media/r-output-rtestdata.png)

2. 입력 또는 출력 변수의 이름을 변경해 보겠습니다. 위의 스크립트는 기본 입력 및 출력 변수 이름, _inputdataset_ 및 _outputdataset_을 사용 했습니다. _Inputdatset_와 연결 된 입력 데이터를 정의 하려면 *@input_data_1* 변수를 사용 합니다.

    이 스크립트에서 저장 프로시저에 대 한 output 및 input 변수의 이름이 *SQL_out* 및 *SQL_in*로 변경 되었습니다.

    ```sql
    EXECUTE sp_execute_external_script
      @language = N'R'
      , @script = N' SQL_out <- SQL_in;'
      , @input_data_1 = N'SELECT 12 as Col;'
      , @input_data_1_name  = N'SQL_in'
      , @output_data_1_name =  N'SQL_out'
      WITH RESULT SETS (([NewColName] INT NOT NULL));
    ```

    R은 대/소문자를 구분 하므로 및 `@input_data_1_name` `@output_data_1_name` 의 입력 및 출력 변수는의 r 코드 `@script`와 일치 해야 합니다. 

    하나의 입력 데이터 세트만 매개 변수로 전달할 수 있으며 하나의 데이터 세트만 반환할 수 있습니다. 그러나 R 코드 내에서 다른 데이터 세트를 호출할 수 있으며 데이터 세트 외에 다른 유형의 출력을 반환할 수 있습니다. 또한 모든 매개 변수에 OUTPUT 키워드를 추가하여 결과와 함께 매개 변수를 반환할 수도 있습니다. 

    `WITH RESULT SETS` 문은 SQL Server에 사용 되는 데이터에 대 한 스키마를 정의 합니다. R에서 반환 하는 각 열에 대해 SQL 호환 데이터 형식을 제공 해야 합니다. R 데이터 프레임에서 열 이름을 사용할 필요가 없으므로 스키마 정의를 사용 하 여 새 열 이름을 제공할 수도 있습니다.

3. R 스크립트를 사용 하 여 값을 생성 하 고 입력 쿼리 문자열 _@input_data_1_ 을 비워 둘 수도 있습니다.

    ```sql
    EXECUTE sp_execute_external_script
        @language = N'R'
        , @script = N' mytextvariable <- c("hello", " ", "world");
            OutputDataSet <- as.data.frame(mytextvariable);'
        , @input_data_1 = N''
    WITH RESULT SETS (([Col1] CHAR(20) NOT NULL));
    ```

    **결과**

    ![입력으로를 @script 사용 하 여 쿼리 결과](./media/r-data-generated-output.png)

## <a name="next-steps"></a>다음 단계

R과 SQL Server 간에 데이터를 전달할 때 발생할 수 있는 몇 가지 문제를 검토 합니다. 예를 들어 R과 SQL 간에 테이블 형식 데이터의 암시적 변환과 차이가 있습니다.

> [!div class="nextstepaction"]
> [빠른 시작: 데이터 형식 및 개체 처리](quickstart-r-data-types-and-objects.md)