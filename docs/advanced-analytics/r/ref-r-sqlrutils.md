---
title: sqlrutils 도우미 함수-SQL Server Machine Learning 서비스
description: R 스크립트를 포함 하는 저장된 프로시저를 생성 하려면 R을 사용 하 여 SQL Server 2016 R Services 및 SQL Server 2017의 Machine Learning Services sqlrutils 함수 라이브러리를 사용 합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 7ccc3ad494658fc7a8f9c67472aecb1c4cddb7da
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58512240"
---
# <a name="sqlrutils-r-library-in-sql-server"></a>sqlrutils (SQL Server의 R 라이브러리)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

**sqlrutils** 패키지는 R 사용자가 T-SQL 저장 프로시저에 R 스크립트를 입력하고, 데이터베이스에 해당 저장 프로시저를 등록하며, R 개발 환경에서 저장 프로시저를 실행하는 메커니즘을 제공합니다. 

단일 저장 프로시저 내에서 실행되도록 R 코드를 변환하면 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)에 대한 매개 변수로 R 스크립트를 포함해야 하는 SQL Server R Services를 보다 효과적으로 사용할 수 있습니다. **sqlrutils** 패키지를 사용하면 이 포함된 R 스크립트를 작성하고 관련 매개 변수를 적절히 설정할 수 있습니다.

**sqlrutils** 패키지는 다음과 같은 작업을 수행합니다.

- 생성된 T-SQL 스크립트를 R 데이터 구조 내에 문자열로 저장합니다.
- 필요에 따라 T-SQL 스크립트에 대한 .sql 파일을 생성하고 편집하거나 실행하여 저장 프로시저를 만들 수 있습니다.
- 새로 만든 저장 프로시저를 R 개발 환경에서 SQL Server 인스턴스에 등록합니다.

잘 구성된(Well-Formed) 매개 변수를 전달하고 결과를 처리하여 R 환경에서 저장 프로시저를 실행할 수도 있습니다. 또는 SQL Server의 저장 프로시저를 사용하여 ETL, 모델 학습 및 고용량 점수 매기기 같은 일반적인 데이터베이스 통합 시나리오를 지원할 수 있습니다.

  > [!NOTE]
  > R 환경에서 *executeStoredProcedure* 함수를 호출하여 저장 프로시저를 실행하려는 경우 SQL Server용 ODBC 드라이버 13과 같은 ODBC 3.8 공급자를 사용해야 합니다.  
  
## <a name="full-reference-documentation"></a>전체 참조 설명서

합니다 **sqlrutils** 라이브러리는 여러 Microsoft 제품을 배포 하지만 SQL Server 또는 다른 제품에서 라이브러리를 표시 하는지 여부를 사용량은 동일 합니다. 함수는 동일 하므로 [개별 sqlrutils 함수에 대 한 설명서](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) 아래에 있는 하나의 위치에 게시 되는 [R 참조](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference) Microsoft Machine Learning Server에 대 한 합니다. 모든 제품별 해야 동작 존재, 불일치 함수 도움말 페이지에 표시 됩니다.

## <a name="functions-list"></a>함수 목록

다음 섹션에서 호출할 수 있는 함수의 개요를 제공 합니다 **sqlrutils** 포함 하는 저장된 프로시저를 개발 하는 패키지는 R 코드를 포함 합니다. 각 메서드 또는 함수에 대 한 매개 변수의 세부 정보를 패키지에 대 한 R 도움말을 참조 하세요. `help(package="sqlrutils")`

|기능 | Description |
|------|-------------|
|[executeStoredProcedure](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/executestoredprocedure)| SQL 저장 프로시저를 실행 합니다.|
|[getInputParameters](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/getinputparameters)| 저장된 프로시저에 입력된 매개 변수의 목록을 가져옵니다.| 
|[InputData](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/inputdata)| R 데이터 프레임에서 사용할 데이터의 원본을 SQL Server에 정의합니다. 입력 데이터를 저장할 data.frame의 이름 및 데이터 또는 기본값을 가져오는 쿼리를 지정합니다. 간단한 SELECT 쿼리만 지원됩니다. | 
|[InputParameter](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/inputparameter)| T-SQL 스크립트에 포함될 단일 입력 매개 변수를 정의합니다. 매개 변수와 해당 R 데이터 형식의 이름을 제공해야 합니다.| 
|[OutputData](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/outputdata)| R 함수가 data.frame을 포함하는 목록을 반환하는 경우 필요한 중간 데이터 개체를 생성합니다. *OutputData* 개체는 목록에서 가져온 단일 data.frame의 이름을 저장하는 데 사용됩니다.| 
|[OutputParameter](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/outputparameter) | R 함수가 목록을 반환하는 경우 필요한 중간 데이터 개체를 생성합니다. *OutputParameter* 개체는 멤버가 데이터 프레임이 **아니라고** 가정하고 목록에서 단일 멤버의 이름과 데이터 형식을 저장합니다. |
|[registerStoredProcedure](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/registerstoredprocedure) | 데이터베이스를 사용 하 여 저장된 프로시저를 등록 합니다.|
|[setInputDataQuery](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/setinputdataquery)| 쿼리 저장된 프로시저의 입력된 데이터 매개 변수에 할당 합니다.| 
|[setInputParameterValue](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/setinputparametervalue)| 저장된 프로시저의 입력 매개 변수 값을 할당 합니다.| 
|[StoredProcedure](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/storedprocedure)| 저장된 프로시저 개체입니다.|


## <a name="how-to-use-sqlrutils"></a>Sqlrutils를 사용 하는 방법

합니다 **sqlrutils** 라이브러리 함수는 R. 사용 하 여 SQL Server Machine Learning을 가진 컴퓨터에서 실행 해야 합니다 클라이언트 워크스테이션에서 작업 하는 경우 SQL Server에 shift 실행 원격 계산 컨텍스트를 설정 합니다. 이 패키지를 사용 하 여 워크플로 다음 단계가 포함 됩니다.

+ 저장된 프로시저 매개 변수 (입력, 출력 또는 둘 다)를 정의 합니다. 
+ 생성 및 저장된 프로시저를 등록 합니다.    
+ 저장 프로시저 실행  

R 세션에 로드 **sqlrutils** 입력 하 여 명령줄에서 `library(sqlrutils)`합니다.

> [!Note]
> 없는 SQL Server (예: R 클라이언트 인스턴스)에서 SQL server 계산 컨텍스트를 변경 하 고 해당 계산 컨텍스트에서 코드를 실행 하는 경우 컴퓨터에서이 라이브러리를 로드할 수 있습니다.


### <a name="define-stored-procedure-parameters-and-inputs"></a>저장된 프로시저 매개 변수 및 입력 정의

`StoredProcedure` 는 저장 프로시저를 작성하는 데 사용되는 기본 생성자입니다. 이 생성자는 *SQL Server 저장 프로시저* 개체를 생성하고, 필요에 따라 T-SQL 명령을 사용하여 저장 프로시저를 생성하는 데 사용할 수 있는 쿼리를 포함하는 텍스트 파일을 만듭니다. 

필요에 따라 *StoredProcedure* 함수는 지정된 인스턴스 및 데이터베이스에 저장 프로시저를 등록할 수도 있습니다.

+ `func` 인수를 사용하여 유효한 R 함수를 지정합니다. 함수에서 사용하는 모든 변수는 함수 내부에 정의되거나 입력 매개 변수로 제공되어야 합니다. 이러한 매개 변수는 최대 한 개의 데이터 프레임을 포함할 수 있습니다.

+ R 함수는 데이터 프레임, 명명된 목록 또는 NULL을 반환해야 합니다. 함수가 목록을 반환하는 경우 목록에는 최대 하나의 data.frame이 포함될 수 있습니다.

+ 인수 `spName` 을 사용하여 만들려는 저장 프로시저의 이름을 지정합니다.

+ `setInputData`, `setInputParameter`및 `setOutputParameter`같은 도우미 함수로 만든 개체를 사용하여 선택적인 입력 및 출력 매개 변수를 전달할 수 있습니다.

+  필요에 따라 `filePath` 를 사용하여 만들려는 .sql 파일의 이름과 경로를 제공합니다. SQL Server 인스턴스에서 이 파일을 실행하면 T-SQL을 사용하여 저장 프로시저를 생성할 수 있습니다.

+ 저장 프로시저가 저장될 서버 및 데이터베이스를 정의하려면 `dbName` 및  `connectionString`인수를 사용합니다.

+ 특정 *StoredProcedure* 개체를 만드는 데 사용된 *InputData* 및 *InputParameter* 개체의 목록을 가져오려면 `getInputParameters`를 호출합니다. 

+ 지정된 데이터베이스에 저장 프로시저를 등록하려면 `registerStoredProcedure`를 사용합니다.

기본값을 지정하지 않는 한 일반적으로 저장 프로시저 개체에는 연결된 데이터나 값이 없습니다. 데이터는 저장 프로시저가 실행된 다음에야 검색됩니다. 

### <a name="specify-inputs-and-execute"></a>입력을 지정 하 고 실행

+ `setInputDataQuery` 를 사용하여 *InputParameter* 개체에 쿼리를 할당합니다. 예를 들어 R에서 저장 프로시저 개체를 만든 경우 원하는 입력으로 저장 프로시저를 실행하려면 `setInputDataQuery` 를 사용하여 *StoredProcedure* 함수에 인수를 전달할 수 있습니다.

+ `setInputValue` 를 사용하여 *InputParameter* 개체로 저장된 매개 변수에 특정 값을 할당합니다. 그런 다음 매개 변수 개체와 해당 값 할당을 *StoredProcedure* 함수에 전달하여 설정된 값으로 저장 프로시저를 실행합니다.

+ `executeStoredProcedure` 를 사용하여 *StoredProcedure* 개체로 정의된 저장 프로시저를 실행합니다. R 코드에서 저장 프로시저를 실행하는 경우에만 이 함수를 호출합니다. SQL Server에서 T-SQL을 사용하여 저장 프로시저를 실행하는 경우에는 사용하지 마세요.

> [!NOTE]
> *executeStoredProcedure* 함수에는 SQL Server용 ODBC 드라이버 13과 같은 ODBC 3.8 공급자가 필요합니다.  

## <a name="see-also"></a>참고자료

[sqlrutils를 사용하여 저장 프로시저를 만드는 방법](how-to-create-a-stored-procedure-using-sqlrutils.md)

