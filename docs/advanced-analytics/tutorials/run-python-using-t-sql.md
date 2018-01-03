---
title: "T-SQL을 사용 하 여 Python 실행 | Microsoft Docs"
ms.custom: 
ms.date: 09/19/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: tutorial
applies_to: SQL Server 2016
dev_langs: Python
caps.latest.revision: "2"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.openlocfilehash: f584f98f5c30e4ca30b4f75748ee173bb2f1a257
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/20/2017
---
# <a name="run-python-using-t-sql"></a>T-SQL을 사용 하 여 Python 실행

이 예제에서는 저장된 프로시저를 사용 하 여 SQL Server의 간단한 Python 스크립트를 실행 하는 방법을 보여 줍니다. [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)

## <a name="step-1-create-the-test-data-table"></a>1단계. 테스트 데이터 테이블 만들기

첫째, 원본 데이터에는 요일 이름을 매핑할 때 사용할 일부 추가 데이터를 만듭니다. 테이블을 만들려면 다음 T-SQL 문을 실행 합니다.

```SQL
CREATE TABLE PythonTest (
    [DayOfWeek] varchar(10) NOT NULL,
    [Amount] float NOT NULL
    )
GO

INSERT INTO PythonTest VALUES
('Sunday', 10.0),
('Monday', 11.1),
('Tuesday', 12.2),
('Wednesday', 13.3),
('Thursday', 14.4),
('Friday', 15.5),
('Saturday', 16.6),
('Friday', 17.7),
('Monday', 18.8),
('Sunday', 19.9)
GO
```

## <a name="step-2-run-the-hello-world-script"></a>2단계. "Hello World" 스크립트를 실행 합니다.

다음 코드 Python 실행 파일을 로드 하 고, 입력된 데이터를 전달, 입력된 데이터의 각 행에 대 한 테이블의 요일 이름이 주 일 인덱스를 나타내는 숫자도 업데이트.

매개 변수를 메모해  *@RowsPerRead* 합니다. 이 매개 변수는 Python 런타임의에 SQL Server에서 전달 되는 행 수를 지정 합니다.

이라고 Python 데이터 분석 라이브러리 **팬더**, SQL server에 데이터를 전달 하기 위한 필수 항목이 며 기본적으로 컴퓨터 학습 서비스 포함 됩니다.

```sql
DECLARE @ParamINT INT = 1234567
DECLARE @ParamCharN VARCHAR(6) = 'INPUT '

print '------------------------------------------------------------------------'
print 'Output parameters (before):'
print FORMATMESSAGE('ParamINT=%d', @ParamINT)
print FORMATMESSAGE('ParamCharN=%s', @ParamCharN)

print 'Dataset (before):'
SELECT * FROM PythonTest

print '------------------------------------------------------------------------'
print 'Dataset (after):'
DECLARE @RowsPerRead INT = 5

execute sp_execute_external_script 
@language = N'Python',
@script = N'
import sys
import os
print("*******************************")
print(sys.version)
print("Hello World")
print(os.getcwd())
print("*******************************")
if ParamINT == 1234567:
       ParamINT = 1
else:
       ParamINT += 1

ParamCharN="OUTPUT"
OutputDataSet = InputDataSet

global daysMap

daysMap = {
       "Monday" : 1,
       "Tuesday" : 2,
       "Wednesday" : 3,
       "Thursday" : 4,
       "Friday" : 5,
       "Saturday" : 6,
       "Sunday" : 7
       }

OutputDataSet["DayOfWeek"] = pandas.Series([daysMap[i] for i in OutputDataSet["DayOfWeek"]], index = OutputDataSet.index, dtype = "int32")
', 
@input_data_1 = N'SELECT * FROM PythonTest', 
@params = N'@r_rowsPerRead INT, @ParamINT INT OUTPUT, @ParamCharN CHAR(6) OUTPUT',
@r_rowsPerRead = @RowsPerRead,
@paramINT = @ParamINT OUTPUT,
@paramCharN = @ParamCharN OUTPUT
with result sets (("DayOfWeek" int null, "Amount" float null))

print 'Output parameters (after):'
print FORMATMESSAGE('ParamINT=%d', @ParamINT)
print FORMATMESSAGE('ParamCharN=%s', @ParamCharN)
GO
```

> [!TIP]
> 이 저장된 프로시저에 대 한 매개 변수는이 빠른 시작에서 자세히 설명 되어: [T-SQL에서 사용 하 여 R 코드](rtsql-using-r-code-in-transact-sql-quickstart.md)합니다.

## <a name="step-3-view-the-results"></a>3단계. 결과 보기

저장된 프로시저는 원래 데이터를 가져옵니다 Python 스크립트를 적용 하 고 다음에 수정된 된 데이터를 반환 된 **결과** Management Studio 또는 다른 SQL 쿼리 도구 창입니다.


|DayOfWeek (이전)| Amount|DayOfWeek (이후) |
|-----|-----|-----|
|일요일|10|7|
|월요일|11.1|1|
|화요일|12.2|2|
|수요일|13.3|3|
|목요일|14.4|4|
|금요일|15.5|5|
|토요일|16.6|6|
|금요일|17.7|5|
|월요일|18.8|1|
|일요일|19.9|7|

상태 메시지 또는 Python 콘솔에 반환 되는 오류 메시지의로 반환 되는 **쿼리** 창. 표시 될 수는 출력의 발췌 한 구문을 다음과 같습니다.

*예제 결과*

```
Output parameters (before):
ParamINT=1234567
ParamCharN=INPUT 
Dataset (before):

(10 rows affected)

Dataset (after):
STDOUT message(s) from external script: 
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib\site-packages\revoscalepy

3.5.2 |Anaconda 4.2.0 (64-bit)| (default, Jul  5 2016, 11:41:13) [MSC v.1900 64 bit (AMD64)]
Hello World
C:\PROGRA~1\MICROS~2\MSSQL1~1.MSS\MSSQL\EXTENS~1\MSSQLSERVER01\7A70B3FB-FBA2-4C52-96D6-8634DB843229

3.5.2 |Anaconda 4.2.0 (64-bit)| (default, Jul  5 2016, 11:41:13) [MSC v.1900 64 bit (AMD64)]
Hello World
C:\PROGRA~1\MICROS~2\MSSQL1~1.MSS\MSSQL\EXTENS~1\MSSQLSERVER01\7A70B3FB-FBA2-4C52-96D6-8634DB843229

(10 rows affected)
Output parameters (after):
ParamINT=2
ParamCharN=OUTPUT
```

+ **메시지** 출력 스크립트 실행에 사용 되는 작업 디렉터리에 포함 됩니다. 이 예제에서는 작업을 관리 하려면 SQL Server에서 할당 된 작업자 계정이 MSSQLSERVER01 참조 합니다. 

    GUID에는 데이터와 스크립트 아티팩트 저장 스크립트 실행 중에 만들어진 임시 폴더의 이름입니다. 이러한 임시 폴더 SQL Server를 통해 보안이 유지 되 고 정리 됩니다 Windows 작업 개체에서 스크립트 종료 된 후입니다.

+ "Hello World" 라는 메시지가 포함 된 섹션에는 두 번 출력 합니다. 이 문제가 발생 하기 때문에 값  *@RowsPerRead*  5로 설정 된 테이블에 10 개의 행이 하 고 따라서 Python에 대 한 두 호출 테이블의 모든 행을 처리 하는 데 필요한 합니다.

    프로덕션, 실행에서는 각 일괄 처리에서 전달 되어야 하는 행의 최대 수를 확인 하려면 다른 값을 실험할 하는 것이 좋습니다. 행 수가 최적의 데이터에 따라 달라을 전달 하는 데이터의 형식과 데이터 집합의 열 수에 영향을 합니다.

## <a name="resources"></a>리소스

이러한 추가 Python 샘플 및 고급 팁 및 종단 간 데모에 대 한 자습서를 참조 하십시오.

+ [Python revoscalepy를 사용 하 여 모델을 만들려면](use-python-revoscalepy-to-create-model.md)
+ [SQL 개발자를 위해 데이터베이스에서 Python](sqldev-in-database-python-for-sql-developers.md)
+ [Python 및 SQL Server를 사용 하 여 예상 모델을 작성](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/)

## <a name="troubleshooting"></a>문제 해결

저장된 프로시저를 찾을 수 없는 경우 `sp_execute_external_script`, 아마도 완료 하지 않았습니다 외부 스크립트 실행을 지원 하도록 인스턴스 구성 것을 의미 합니다. SQL Server 2017 설치 프로그램을 실행 하 기계 학습 언어도 Python을 선택한 후 명시적으로 설정 해야 사용 하 여 기능 `sp_configure`, 한 다음 인스턴스를 다시 시작 합니다. 자세한 내용은 참조 [python 설치 컴퓨터 학습 서비스](../python/setup-python-machine-learning-services.md)합니다.