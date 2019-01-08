---
title: R-SQL Server Machine Learning에서에서 입력 및 출력을 사용 하 여 작업에 대 한 빠른 시작
description: SQL Server에서 R 스크립트에 대 한이 빠른 시작에서는 입력 및 출력 sp_execute_external_script 시스템 저장 프로시저를 구성 하는 방법에 알아봅니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/04/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 56d2eb65ca95dd4f153f3c7a6ebb00e926465687
ms.sourcegitcommit: baca29731a1be4f8fa47567888278394966e2af7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/04/2019
ms.locfileid: "54046861"
---
# <a name="quickstart-handle-inputs-and-outputs-using-r-in-sql-server"></a>빠른 시작: 입력 및 SQL Server에서 R을 사용 하 여 출력 처리
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 빠른 시작에는 SQL Server Machine Learning Services에서 R 또는 R Services를 사용 하는 경우 출력 및 입력을 처리 하는 방법을 보여 줍니다.

SQL Server에서 R 코드를 실행 하려는 경우 저장된 프로시저에서 R 스크립트를 래핑해야 합니다. 를 작성 하거나 R 스크립트를 전달 수 있습니다 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)합니다. 이 시스템 저장된 프로시저에서 R로 데이터를 통과 하는 SQL Server의 컨텍스트에서 R 런타임을 시작 하는 R 사용자 세션을 안전 하 게 관리 하 고 클라이언트에 결과 반환 합니다.

기본적으로 [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) 형식의 유효한 SQL 쿼리를 제공 하는 일반적으로 단일 입력된 dataset을 수락 합니다. 다른 유형의 입력 SQL 변수로 전달할 수 있습니다.

저장된 프로시저는 출력으로 단일 R 데이터 프레임을 반환 하지만 스칼라 및 변수로 모델을 출력할 수도 있습니다. 예를 들어 이진 변수 학습된 된 모델 출력 하 고 테이블에 해당 모델을 작성 하는 T-SQL INSERT 문을 전달할 수 있습니다. 이진 형식의 그림 또는 스칼라를 생성할 수도 있습니다 (날짜 및 시간을 같은 개별 값을 시간 경과 됨 모델을 학습 등).

## <a name="prerequisites"></a>사전 요구 사항

이전 빠른 시작에서는 [SQL Server에 있는지 확인 하는 R](quickstart-r-verify.md), 정보를 제공 하 고이 빠른 시작에 필요한 R 환경 설정에 대 한 링크입니다.

## <a name="create-the-source-data"></a>원본 데이터 만들기

다음 T-SQL 문을 실행 하 여 테스트 데이터의 작은 테이블을 만듭니다.

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

기본값에 살펴보겠습니다 sp_execute_external_script의 입력 및 출력 변수: `InputDataSet` 고 `OutputDataSet`입니다.

1. R 스크립트에 대 한 입력으로 테이블에서 데이터를 가져올 수 있습니다. 다음 문을 실행 합니다. 테이블에서 데이터를 가져오고, R 런타임을 통해 왕복 하며 열 이름의 값을 반환 합니다 *NewColName*합니다.

    쿼리에서 반환 되는 데이터를 데이터 프레임으로 SQL Database로 데이터를 반환 하는 R 런타임에 전달 됩니다. WITH RESULT SETS 절을 SQL Database에 대 한 반환된 된 데이터 테이블의 스키마를 정의 합니다.

    ```sql
    EXECUTE sp_execute_external_script
        @language = N'R'
        , @script = N'OutputDataSet <- InputDataSet;'
        , @input_data_1 = N'SELECT * FROM RTestData;'
    WITH RESULT SETS (([NewColName] INT NOT NULL));
    ```

    **결과**

    ![테이블에서 데이터를 반환 하는 R 스크립트의 출력](./media/r-output-rtestdata.png)

2. 입력 또는 출력 변수의 이름을 변경해 보겠습니다. 위의 스크립트 사용 기본 입력 및 출력 변수 이름 _InputDataSet_ 하 고 _OutputDataSet_합니다. 연결 된 입력된 데이터를 정의 하 _InputDatSet_를 사용 합니다 *@input_data_1* 변수.

    이 스크립트를 저장된 프로시저의 출력 및 입력된 변수 이름이 변경 되었습니다 *SQL_out* 하 고 *SQL_in*:

    ```sql
    EXECUTE sp_execute_external_script
      @language = N'R'
      , @script = N' SQL_out <- SQL_in;'
      , @input_data_1 = N'SELECT 12 as Col;'
      , @input_data_1_name  = N'SQL_in'
      , @output_data_1_name =  N'SQL_out'
      WITH RESULT SETS (([NewColName] INT NOT NULL));
    ```

    R은 대/소문자 구분, 하므로 입력 및 출력 변수 사례 `@input_data_1_name` 및 `@output_data_1_name` 에서 R 코드에 있는 이름과 일치 해야 `@script`합니다. 

    또한 매개 변수의 순서가 중요 합니다. 선택적 매개 변수 *@input_data_1_name* 및 *@output_data_1_name*을 사용하기 위해 먼저 필수 매개 변수 *@input_data_1* 및 *@output_data_1*을 지정해야 합니다.

    하나의 입력 데이터 세트만 매개 변수로 전달할 수 있으며 하나의 데이터 세트만 반환할 수 있습니다. 그러나 R 코드 내에서 다른 데이터 세트를 호출할 수 있으며 데이터 세트 외에 다른 유형의 출력을 반환할 수 있습니다. 또한 모든 매개 변수에 OUTPUT 키워드를 추가하여 결과와 함께 매개 변수를 반환할 수도 있습니다. 

    `WITH RESULT SETS` 문은 SQL Server에서 사용 되는 데이터에 대 한 스키마를 정의 합니다. R.에서 반환 하는 각 열에 대 한 SQL 호환 데이터 형식을 제공 해야 합니다. 스키마 정의 사용 하 여 새 열 이름을 너무 R 데이터 프레임에서 열 이름을 사용할 필요가 없습니다.

3. R 스크립트를 사용 하 여 값을 생성 하 고 수도의 입력된 쿼리 문자열 _@input_data_1_ 비어 있습니다.

    ```sql
    EXECUTE sp_execute_external_script
        @language = N'R'
        , @script = N' mytextvariable <- c("hello", " ", "world");
            OutputDataSet <- as.data.frame(mytextvariable);'
        , @input_data_1 = N''
    WITH RESULT SETS (([Col1] CHAR(20) NOT NULL));
    ```

    **결과**

    ![쿼리 결과 사용 하 여 @script 입력으로](./media/r-data-generated-output.png)

## <a name="next-steps"></a>다음 단계

암시적 변환 및 R과 SQL 간 테이블 형식 데이터의 차이 등 R 및 SQL Server 간에 데이터를 전달할 때 발생할 수 있는 문제 중 일부를 검사 합니다.

> [!div class="nextstepaction"]
> [빠른 시작: 데이터 형식 및 개체를 처리 합니다.](quickstart-r-data-types-and-objects.md)