---
title: 입력 및 출력 (SQL Server Machine Learning) R에서 사용 하기 위한 빠른 시작 | Microsoft Docs
description: SQL Server에서 R 스크립트에 대 한이 빠른 시작에서는 입력 및 출력 sp_execute_external_script 시스템 저장 프로시저를 구성 하는 방법에 알아봅니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 07/15/2018
ms.topic: quickstart
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: b41a8c30cd0ecbe040819478c0cadece1b9eb704
ms.sourcegitcommit: c8f7e9f05043ac10af8a742153e81ab81aa6a3c3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/17/2018
ms.locfileid: "39086585"
---
# <a name="quickstart-handle-inputs-and-outputs-using-r-in-sql-server"></a>입력 및 SQL Server에서 R을 사용 하 여 출력을 처리 하는 빠른 시작:
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server에서 R 코드를 실행 하려는 경우 저장된 프로시저에서 R 스크립트를 래핑해야 합니다. 를 작성 하거나 R 스크립트를 전달 수 있습니다 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)합니다. 이 시스템 저장된 프로시저에서 R로 데이터를 통과 하는 SQL Server의 컨텍스트에서 R 런타임을 시작 하는 R 사용자 세션을 안전 하 게 관리 하 고 클라이언트에 결과 반환 합니다.

## <a name="prerequisites"></a>사전 요구 사항

이전 빠른 시작에서는 [Hello World R 및 SQL](rtsql-using-r-code-in-transact-sql-quickstart.md), 정보를 제공 하 고이 빠른 시작에 필요한 R 환경 설정에 대 한 링크입니다.

<a name="bkmk_SSMSBasics"></a>

## <a name="create-some-simple-test-data"></a>몇 가지 간단한 테스트 데이터 만들기

다음 T-SQL 문을 실행 하 여 테스트 데이터의 작은 테이블을 만듭니다.

```sql
CREATE TABLE RTestData ([col1] int not null) ON [PRIMARY]
INSERT INTO RTestData   VALUES (1);
INSERT INTO RTestData   VALUES (10);
INSERT INTO RTestData   VALUES (100) ;
GO
```

테이블을 만들었으면 다음 문을 사용하여 테이블을 쿼리합니다.
  
```sql
SELECT * FROM RTestData
```

**결과**

![RTestData 테이블의 내용](media/quickstart-r-working-input-outputs-results-1.png)


## <a name="get-the-same-data-using-r-script"></a>R 스크립트를 사용하여 동일한 데이터 가져오기

테이블을 만든 후 다음 문을 실행합니다.

```sql
EXECUTE sp_execute_external_script
      @language = N'R'
    , @script = N' OutputDataSet <- InputDataSet;'
    , @input_data_1 = N' SELECT *  FROM RTestData;'
    WITH RESULT SETS (([NewColName] int NOT NULL));
```

테이블에서 데이터를 가져오고, R 런타임을 통해 왕복 하며 열 이름의 값을 반환 합니다 *NewColName*합니다.

**결과**

![rsql_basictut_getsamedataR](media/rsql-basictut-getsamedatar.PNG)


**설명**

+ *@language* 매개 변수는 호출할 언어 확장(이 경우 R)을 정의합니다.
+ *@script* 매개 변수에서 R 런타임에 전달할 명령을 정의합니다. 전체 R 스크립트는 이 인수에 유니코드 텍스트로 포함되어야 합니다. **nvarchar** 형식의 변수에 텍스트를 추가한 다음 변수를 호출할 수도 있습니다.
+ 쿼리에서 반환된 데이터는 R 런타임에 전달되고 R 런타임은 데이터를 SQL Server에 데이터 프레임으로 전달합니다.
+ WITH RESULT SETS 절은 SQL Server에 대한 반환된 데이터 테이블의 스키마를 정의합니다.

## <a name="change-input-or-output-variables"></a>입력 또는 출력 변수 변경

이전 예제에서는 기본 입력 및 출력 변수 이름 _InputDataSet_ 및 _OutputDataSet_을 사용했습니다. _InputDatSet_과 연결된 입력 데이터를 정의하려면 *@input_data_1* 변수를 사용합니다.

이 예제에서는 저장 프로시저에 대한 출력 및 입력 변수의 이름이 *SQL_Out* 및 *SQL_In*으로 변경되었습니다.

```sql
EXECUTE sp_execute_external_script
  @language = N'R'
  , @script = N' SQL_out <- SQL_in;'
  , @input_data_1 = N' SELECT 12 as Col;'
  , @input_data_1_name  = N'SQL_In'
  , @output_data_1_name =  N'SQL_Out'
  WITH RESULT SETS (([NewColName] int NOT NULL));
```

오류가 발생 하면 "SQL 개체\_에서 찾을 수 없음"? 원인은 R는 대/소문자를 구분하기 때문입니다. 예제에서 R 스크립트는 변수 *SQL_in* 및 *SQL_out*을 사용하지만 저장 프로시저에 대한 매개 변수는 변수 *SQL_In* 및 *SQL_Out*을 사용합니다.

수정 **만** 는 *SQL_In* 변수를 *@script* 다시 저장된 프로시저를 실행 합니다.

이제 표시 된 **다른** 오류:

```Error
EXECUTE statement failed because its WITH RESULT SETS clause specified 1 result set(s), but the statement only sent 0 result set(s) at run time.
```

표시 하면이 오류 되므로 새 R 코드를 테스트 하는 경우에 종종 표시 될 수 있습니다. 즉, R 스크립트를 성공적으로 실행 되었지만 SQL Server가 없는 데이터를 받거나 잘못 되거나 예기치 않은 데이터를 수신 합니다.

이 경우 출력 스키마(**WITH**로 시작하는 줄)는 정수 데이터의 열 하나가 반환되도록 지정하지만, R은 데이터를 다른 변수에 넣기 때문에 SQL Server에 아무것도 반환되지 않으므로 오류가 발생합니다. 오류를 해결 하려면 두 번째 변수 이름을 수정 합니다.

**이러한 요구 사항을 잊지 말고 하세요!**

- 변수 이름은 유효한 SQL 식별에 대한 규칙을 따라야 합니다.
- 매개 변수의 순서가 중요합니다. 선택적 매개 변수 *@input_data_1_name* 및 *@output_data_1_name*을 사용하기 위해 먼저 필수 매개 변수 *@input_data_1* 및 *@output_data_1*을 지정해야 합니다.
- 하나의 입력 데이터 집합만 매개 변수로 전달할 수 있으며 하나의 데이터 집합만 반환할 수 있습니다. 그러나 R 코드 내에서 다른 데이터 집합을 호출할 수 있으며 데이터 집합 외에 다른 유형의 출력을 반환할 수 있습니다. 또한 모든 매개 변수에 OUTPUT 키워드를 추가하여 결과와 함께 매개 변수를 반환할 수도 있습니다. 이 자습서의 뒷부분에 간단한 예제가 있습니다.
- `WITH RESULT SETS` 문은 SQL Server를 위해 데이터에 대한 스키마를 정의합니다. R에서 반환하는 각 열에 대한 SQL 호환 데이터 형식을 제공해야 합니다. 스키마 정의를 사용하여 새 열 이름도 제공할 수 있고 R data.frame의 열 이름을 사용할 필요가 없습니다. 경우에 따라이 절은 선택 사항입니다. 생략 하 고 어떻게 되는지 확인 합니다.

## <a name="generate-results-using-r"></a>R을 사용하여 결과 생성

R 스크립트를 사용하여 값을 생성하고 _@input_data_1_의 입력 쿼리 문자열은 비워 둘 수도 있습니다. 또는 유효한 SQL SELECT 문을 자리 표시자로 사용하고 R 스크립트에는 SQL 결과를 사용하지 마세요.

```sql
EXECUTE sp_execute_external_script
    @language = N'R'
   , @script = N' mytextvariable <- c("hello", " ", "world");
       OutputDataSet <- as.data.frame(mytextvariable);'
   , @input_data_1 = N' SELECT 1 as Temp1'
   WITH RESULT SETS (([Col1] char(20) NOT NULL));
```

**결과**

![쿼리 결과 사용 하 여 @script 입력으로](media/quickstart-r-working-input-outputs-results-3.png)

## <a name="next-steps"></a>다음 단계

암시적 변환 및 R과 SQL 간 테이블 형식 데이터의 차이 등 R 및 SQL Server 간에 데이터를 전달할 때 발생할 수 있는 문제 중 일부를 검사 합니다.

> [!div class="nextstepaction"]
> [빠른 시작: 데이터 형식 및 개체를 처리 합니다.](../tutorials/rtsql-r-and-sql-data-types-and-data-objects.md)