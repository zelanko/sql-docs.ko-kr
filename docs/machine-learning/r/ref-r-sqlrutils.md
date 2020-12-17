---
title: sqlrutils 도우미 함수
description: sqlrutils는 R 사용자가 T-SQL 저장 프로시저에 R 스크립트를 입력하고, 데이터베이스에 해당 저장 프로시저를 등록하며, R 개발 환경에서 저장 프로시저를 실행하는 메커니즘을 제공하는 Microsoft의 R 패키지입니다. 이 패키지는 SQL Server Machine Learning Services 및 SQL Server 2016 R Services에 포함되어 있습니다.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 07/14/2020
ms.topic: how-to
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15'
ms.openlocfilehash: ac81810036e4159843142cb419deb3d06c57848c
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97470794"
---
# <a name="sqlrutils-r-package-in-sql-server-machine-learning-services"></a>sqlrutils(SQL Server Machine Learning Services의 R 패키지)
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

**sqlrutils** 는 R 사용자가 T-SQL 저장 프로시저에 R 스크립트를 입력하고, 데이터베이스에 해당 저장 프로시저를 등록하며, R 개발 환경에서 저장 프로시저를 실행하는 메커니즘을 제공하는 Microsoft의 R 패키지입니다. 이 패키지는 [SQL Server Machine Learning Services](../sql-server-machine-learning-services.md) 및 [SQL Server 2016 R Services](sql-server-r-services.md)에 포함되어 있습니다.

단일 저장 프로시저 내에서 실행되도록 R 코드를 변환하면 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)에 대한 매개 변수로 R 스크립트를 포함해야 하는 SQL Server R Services를 보다 효과적으로 사용할 수 있습니다. **sqlrutils** 패키지를 사용하면 이 포함된 R 스크립트를 작성하고 관련 매개 변수를 적절히 설정할 수 있습니다.

**sqlrutils** 패키지는 다음과 같은 작업을 수행합니다.

- 생성된 T-SQL 스크립트를 R 데이터 구조 내에 문자열로 저장합니다.
- 필요에 따라 T-SQL 스크립트에 대한 .sql 파일을 생성하고 편집하거나 실행하여 저장 프로시저를 만들 수 있습니다.
- 새로 만든 저장 프로시저를 R 개발 환경에서 SQL Server 인스턴스에 등록합니다.

잘 구성된(Well-Formed) 매개 변수를 전달하고 결과를 처리하여 R 환경에서 저장 프로시저를 실행할 수도 있습니다. 또는 SQL Server의 저장 프로시저를 사용하여 ETL, 모델 학습 및 고용량 점수 매기기 같은 일반적인 데이터베이스 통합 시나리오를 지원할 수 있습니다.

> [!NOTE]
> R 환경에서 *executeStoredProcedure* 함수를 호출하여 저장 프로시저를 실행하려는 경우 SQL Server용 ODBC 드라이버 13과 같은 ODBC 3.8 공급자를 사용해야 합니다.  
  
## <a name="full-reference-documentation"></a>전체 참조 설명서

**sqlrutils** 패키지는 여러 Microsoft 제품에 배포되지만, 패키지를 SQL Server에서 가져오든 다른 제품에서 가져오든 사용 방식은 동일합니다. 함수는 동일하기 때문에 [개별 sqlrutils 함수에 대한 설명서](/machine-learning-server/r-reference/revoscaler/revoscaler)는 Microsoft Machine Learning Server에 대한 [R 참조](/machine-learning-server/r-reference/introducing-r-server-r-package-reference) 아래의 한 위치에만 게시됩니다. 제품별로 고유한 동작이 있는 경우 함수 도움말 페이지에 차이점이 표시됩니다.

## <a name="functions-list"></a>함수 목록

다음 섹션에서는 포함된 R 코드를 포함하는 저장 프로시저를 개발하기 위해 **sqlrutils** 패키지에서 호출할 수 있는 함수에 대한 개요를 제공합니다. 각 메서드 또는 함수의 매개 변수에 대한 자세한 내용은 패키지에 대한 R 도움말을 참조하세요. `help(package="sqlrutils")`

|기능 | 설명 |
|------|-------------|
|[executeStoredProcedure](/machine-learning-server/r-reference/sqlrutils/executestoredprocedure)| SQL 저장 프로시저를 실행합니다.|
|[getInputParameters](/machine-learning-server/r-reference/sqlrutils/getinputparameters)| 저장 프로시저에 대한 입력 매개 변수 목록을 가져옵니다.| 
|[InputData](/machine-learning-server/r-reference/sqlrutils/inputdata)| R 데이터 프레임에서 사용할 데이터의 원본을 SQL Server에 정의합니다. 입력 데이터를 저장할 data.frame의 이름 및 데이터 또는 기본값을 가져오는 쿼리를 지정합니다. 간단한 SELECT 쿼리만 지원됩니다. | 
|[InputParameter](/machine-learning-server/r-reference/sqlrutils/inputparameter)| T-SQL 스크립트에 포함될 단일 입력 매개 변수를 정의합니다. 매개 변수와 해당 R 데이터 형식의 이름을 제공해야 합니다.| 
|[OutputData](/machine-learning-server/r-reference/sqlrutils/outputdata)| R 함수가 data.frame을 포함하는 목록을 반환하는 경우 필요한 중간 데이터 개체를 생성합니다. *OutputData* 개체는 목록에서 가져온 단일 data.frame의 이름을 저장하는 데 사용됩니다.| 
|[OutputParameter](/machine-learning-server/r-reference/sqlrutils/outputparameter) | R 함수가 목록을 반환하는 경우 필요한 중간 데이터 개체를 생성합니다. *OutputParameter* 개체는 멤버가 데이터 프레임이 **아니라고** 가정하고 목록에서 단일 멤버의 이름과 데이터 형식을 저장합니다. |
|[registerStoredProcedure](/machine-learning-server/r-reference/sqlrutils/registerstoredprocedure) | 저장 프로시저를 데이터베이스에 등록합니다.|
|[setInputDataQuery](/machine-learning-server/r-reference/sqlrutils/setinputdataquery)| 저장 프로시저의 입력 데이터 매개 변수에 쿼리를 할당합니다.| 
|[setInputParameterValue](/machine-learning-server/r-reference/sqlrutils/setinputparametervalue)| 저장 프로시저의 입력 매개 변수에 값을 할당합니다.| 
|[StoredProcedure](/machine-learning-server/r-reference/sqlrutils/storedprocedure)| 저장 프로시저 개체|


## <a name="how-to-use-sqlrutils"></a>sqlrutils 사용 방법

**sqlrutils** 패키지 함수는 R을 포함하는 SQL Server Machine Learning이 있는 컴퓨터에서 실행해야 합니다. 클라이언트 워크스테이션에서 작업하는 경우 실행을 SQL Server으로 전환하도록 원격 컴퓨팅 컨텍스트를 설정합니다. 이 패키지를 사용하기 위한 워크플로에는 다음 단계가 포함됩니다.

+ 저장 프로시저 매개 변수(입력, 출력 또는 둘 다)를 정의합니다. 
+ 저장 프로시저 생성 및 등록    
+ 저장 프로시저 실행  

R 세션에서 `library(sqlrutils)`를 입력하여 명령줄에서 **sqlrutils** 를 로드합니다.

> [!Note]
> 컴퓨팅 컨텍스트를 SQL Server로 변경하고 해당 컴퓨팅 컨텍스트에서 코드를 실행하는 경우에는 SQL Server가 없는 컴퓨터(예: R Client 인스턴스)에서 이 패키지를 로드할 수 있습니다.


### <a name="define-stored-procedure-parameters-and-inputs"></a>저장 프로시저 매개 변수 및 입력 정의

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

### <a name="specify-inputs-and-execute"></a>입력 지정 및 실행

+ `setInputDataQuery` 를 사용하여 *InputParameter* 개체에 쿼리를 할당합니다. 예를 들어 R에서 저장 프로시저 개체를 만든 경우 원하는 입력으로 저장 프로시저를 실행하려면 `setInputDataQuery` 를 사용하여 *StoredProcedure* 함수에 인수를 전달할 수 있습니다.

+ `setInputValue` 를 사용하여 *InputParameter* 개체로 저장된 매개 변수에 특정 값을 할당합니다. 그런 다음 매개 변수 개체와 해당 값 할당을 *StoredProcedure* 함수에 전달하여 설정된 값으로 저장 프로시저를 실행합니다.

+ `executeStoredProcedure` 를 사용하여 *StoredProcedure* 개체로 정의된 저장 프로시저를 실행합니다. R 코드에서 저장 프로시저를 실행하는 경우에만 이 함수를 호출합니다. SQL Server에서 T-SQL을 사용하여 저장 프로시저를 실행하는 경우에는 사용하지 마세요.

> [!NOTE]
> *executeStoredProcedure* 함수에는 SQL Server용 ODBC 드라이버 13과 같은 ODBC 3.8 공급자가 필요합니다.  

## <a name="see-also"></a>참고 항목

[sqlrutils를 사용하여 저장 프로시저를 만드는 방법](how-to-create-a-stored-procedure-using-sqlrutils.md)