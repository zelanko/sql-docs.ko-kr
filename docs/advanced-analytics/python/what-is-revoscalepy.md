---
title: "Revoscalepy 소개 | Microsoft Docs"
ms.custom: 
ms.date: 10/05/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: python
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.openlocfilehash: 3863cb3ec0c50de9d5189927b01cba3f7f4277df
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/20/2017
---
# <a name="introducing-revoscalepy"></a>Revoscalepy 소개

**revoscalepy** 분산 컴퓨팅을 지원 하기 위해 microsoft에서 원격 계산 컨텍스트 및 고성능 알고리즘 Python에 대 한 제공 된 새 라이브러리입니다.

에 따라 결정 된 **RevoScaleR** Microsoft R Server 및 SQL Server R Services와 동일한 기능을 제공 하는 것을 목표로의 제공 된 R에 대 한 패키지:

+ 원격 및 로컬 여러 계산 컨텍스트를 지원합니다.
+ 데이터 변환 및 시각화에 대 한이 RevoScaleR에 해당 하는 함수를 제공합니다.
+ 분산 또는 병렬 처리를 위해 RevoScaleR 기계 학습 알고리즘의 Python 버전을 제공합니다.
+ Intel math 라이브러리의 사용을 포함 하 여 성능 향상된

MicrosoftML 패키지 R 및 Python 모두에 대해 제공 됩니다. 자세한 내용은 참조 [SQL Server에서 사용 하 여 MicrosoftML](../using-the-microsoftml-package.md)

## <a name="versions-and-supported-platforms"></a>버전 및 지원 되는 플랫폼

**revoscalepy** 모듈을 사용할 수만 설치 하면 다음과 같은 Microsoft 제품 중 하나:

+ 기계 학습 서비스에서 SQL Server 2017
+ Microsoft 컴퓨터 학습 서버 9.2.0 이상 버전

Revoscalepy의 최신 버전을 알아보려면 SQL Server 2017에 대 한 누적 업데이트 1을 설치 합니다. Python을 비롯 한 많은 향상 된 기능이 포함 됩니다.

+ 새 Python 함수 `rx_create_col_info`와 같은 SQL Server 데이터 원본에서 스키마 정보를 가져오는 [rxCreateColInfo](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcreatecolinfo) 에 대 한 
+ 향상 된 기능 [rx_exec](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-exec) 를 사용 하 여 병렬 시나리오를 지원 하기는 `RxLocalParallel` 계산 컨텍스트. 

## <a name="supported-functions-and-data-types"></a>지원 되는 함수 및 데이터 형식

이 섹션에서는 Python 데이터 형식 및 지 원하는 새 Python 함수에 대 한 개요를 제공는 **revoscalepy** 모듈, SQL Server 2017 CTP 2.0 릴리스에서부터 시작 합니다. 

출시 된 Python 라이브러리의에서 함수에 최신 목록은 다음이 링크 참조:

+ [Python 용 revoscalepy](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package)

+ [Python 용 microsoftml](https://docs.microsoft.com/r-server/python-reference/microsoftml/microsoftml-package)

### <a name="data-types-data-sources-and-compute-contexts"></a>데이터 형식, 데이터 원본 및 계산 컨텍스트

SQL Server 및 Python에 따라서는 다른 데이터 형식을 사용합니다. SQL 또는 Python 데이터 형식 매핑 목록에 대 한 참조 [Python 라이브러리 및 데이터 형식](python-libraries-and-data-types.md)합니다.

기계 학습 python SQL Server에서 지원 되는 데이터 원본에는 ODBC 데이터 원본, SQL Server 데이터베이스 및 XDF 파일을 포함 하 여 로컬 파일을 포함 합니다.

다음 표에 나열 된 함수를 사용 하 여 데이터 원본 개체를 만듭니다. 데이터 소스를 정의한 후 로드 하거나 적절 한 사용 하 여 데이터를 변환 [ETL 함수](#bkmk_etl)합니다.

> [!IMPORTANT]
> 많은 함수 이름을 CTP 2.0에서 Python의 초기 릴리스 이후 변경 되었습니다.

**SQL Server 데이터**

+ 사용 하 여 [RxSqlServerData](https://docs.microsoft.com/r-server/python-reference/revoscalepy/rxsqlserverdata) 쿼리 또는 테이블에서 데이터 원본을 정의 하려면
+ 사용 하 여 [RxInSqlServer](https://docs.microsoft.com/r-server/python-reference/revoscalepy/rxinsqlserver) SQL Server 계산 컨텍스트를 만들려면
+ 사용 하 여 [RxOdbcData](https://docs.microsoft.com/r-server/python-reference/revoscalepy/rxodbcdata) ODBC 연결에서 데이터 소스를 만들려면

**revoscalepy** 도 지원는 [XDF 데이터 원본](https://docs.microsoft.com/r-server/python-reference/revoscalepy/rxxdfdata), 메모리 및 기타 데이터 소스 간의 데이터 이동에 사용 합니다.

> [!TIP]
> 데이터 원본의 아이디어에 익숙하지 않거나 계산 컨텍스트, 기계 학습에 대 한 분산된 컴퓨팅 작동 하는 방법에 대 한 읽기 여 시작 하는 것이 좋습니다 [RevoScaleR](https://msdn.microsoft.com/microsoft-r/scaler-user-guide-introduction)합니다.


### <a name="bkmk_algorithms"></a>기계 학습 및 요약 함수

다음 기계 학습 알고리즘 및 요약 RevoScaleR 함수는 SQL Server 2017 년 1 CTP 2.0 이후부터에 포함 됩니다.

| 함수| Description|참고|
| ------ | ------ |------ |
|`rx_btrees` | 적합된 한 추계 그라데이션 승격 된 의사 결정 트리|`rx_btrees_ex`CTP 2.0|
|`rx_dforest` | 적합된 한 분류 및 회귀 의사 결정 포리스트|`rx_dforest_ex`CTP 2.0|
|`rx_dtree` | 적합된 한 분류 및 회귀 트리 |`rx_dtree_ex`CTP 2.0|
|`rx_lin_mod` | 선형 모델 만들기|`rx_lin_mod_ex`CTP 2.0|
|`rx_logit` | 로지스틱 회귀 모델 만들기|`rx_logit_ex`CTP 2.0|
|`rx_predict` | 학습된 된 모델에서 예측을 생성 합니다.|`rx_predict_ex`CTP 2.0|
|`rx_summary` | 모델의 요약을 생성 합니다.||

새 기계 학습 알고리즘의 Python 버전도 제공 됩니다 [MicrosoftML](https://docs.microsoft.com/r-server/python-reference/microsoftml/microsoftml-package):

| 함수| Description|
| ------ | ------ |
|`rx_fast_forest` |의사 결정 포리스트 모델 만들기|
|`rx_fast_linear` | 추계 이중 좌표 상승 된 선형 회귀|
|`rx_fast_trees` | 승격된 된 트리 모델 만들기 |
|`rx_logistic_regression` | 로지스틱 회귀 모델 만들기|
|`rx_neural_network` | 사용자 지정 가능한 신경망 모델 만들기 |
|`rx_oneclass_svm` | 이상 탐지에 사용 하기 위해는 불균형 데이터 집합에 대해 SVM 모델을 만듭니다.|

> [!TIP]
> 이러한 알고리즘 중 대부분은 Azure 기계 학습에서 모듈로 이미 제공 됩니다.

Python 용 MicrosoftML도 다양 한 변환 및 도우미 함수를 같은 포함:

+ `rx_predict`학습된 된 모델에서 예측을 생성 하 고 실시간 점수 매기기에 사용할 수 있습니다
+ 이미지 기능 생성 함수
+ 텍스트 처리 및 정서 추출에 대 한 함수

자세한 내용은 참조 [MicrosoftML 소개](https://docs.microsoft.com/r-server/r/concept-what-is-the-microsoftml-package)


> [!NOTE]
> Python 커뮤니티 기능에 사용한, 모든 소문자 및 밑줄이 아닌 매개 변수 이름에 카멜식 대/소문자를 포함 하 여 보다 다를 수 있습니다는 코딩 규칙을 사용 합니다. 또한 가득 한 사실을 알게 하는 **revoscalepy** 라이브러리는 항상 소문자로 표시 합니다. 맞아요! 다른 Python 규칙입니다.
> 
> Microsoft r: [Python 함수 도움말]에 대 한 Python 참조 설명서에 대 한 팁을 확인해[Python 함수 도움말](https://docs.microsoft.com/r-server/python-reference/introducing-python-package-reference)

## <a name="examples"></a>예

포함 하는 코드를 실행할 수 있습니다 **revoscalepy** 로컬 또는 원격 계산 컨텍스트에서 작동 합니다. 또한 저장된 프로시저에서 Python 코드를 포함 하 여 SQL Server 내부 Python을 실행할 수 있습니다.

로컬로 실행 하는 경우 일반적으로 실행 하는 Python 스크립트 명령줄 또는 Python 개발 환경에서 고 지정 중 하나를 사용 하 여 SQL Server 계산 컨텍스트는 **revoscalepy** 함수입니다. 전체 코드에 대 한 또는 개별 함수에 대 한 원격 계산 컨텍스트를 사용할 수 있습니다. 예를 들어 다음 모델을 학습 데이터 이동을 방지 하 고 최신 데이터를 사용 하 여 서버를 오프 로드 하는 것이 좋습니다.

저장 프로시저는 완전 한 Python 스크립트를 설정 하려면 [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql), 코드 입 / 출력 명확 하 게 정의 단일 함수로 다시 작성 하는 것이 좋습니다. 입 / 출력 해야 **팬더** 데이터 프레임입니다. 이 도구를 실행 하는 경우 T-SQL을 지 원하는 모든 클라이언트에서 저장된 프로시저를 호출, 쉽게 입력으로 SQL 쿼리를 전달 하 고 수 SQL 테이블에 결과 저장 합니다. 예를 들어 참조 [SQL 개발자를 위해 데이터베이스에서 Python 분석](../tutorials/sqldev-in-database-python-for-sql-developers.md)합니다.

### <a name="using-remote-compute-contexts"></a>원격 계산 컨텍스트를 사용 하 여

+ [Revoscalepy를 사용 하 여 모델 만들기](../tutorials/use-python-revoscalepy-to-create-model.md)

  이 예제에서는 SQL Server의 인스턴스를 사용 하 여 계산 컨텍스트로 써 Python을 실행 하는 방법을 보여 줍니다.

### <a name="using-a-stored-procedure"></a>저장된 프로시저를 사용 하 여

+ [T-SQL을 사용 하 여 Python 실행](../tutorials/run-python-using-t-sql.md)

  이 예제는 저장된 프로시저에 포함 된 Python 스크립트 호출의 기본 메커니즘입니다.

### <a name="using-revoscalepy-with-microsoftml"></a>MicrosoftML revoscalepy 사용

MicrosoftML에 대 한 Python 함수는 계산 컨텍스트 및 revoscalepy에 제공 되는 데이터 소스와 통합 됩니다. 따라서 MicrosoftML 알고리즘을 사용 하 여 정의 하 고, Python에서 모델을 학습 하 고 revoscalepy 함수를 사용 하 여 로컬 또는 SQl Server 계산 컨텍스트에서 Python 코드를 실행 수 없습니다.

Python 코드의 모듈에서는 가져와 다음 필요한 개별 함수를 참조 합니다.

```Python
from microsoftml.modules.logistic_regression.rx_logistic_regression import rx_logistic_regression
from revoscalepy.functions.RxSummary import rx_summary
from revoscalepy.etl.RxImport import rx_import_datasource
```

### <a name="requirements"></a>요구 사항

SQL Server에서 Python 코드를 실행 하려면 먼저 설치 해야 SQL Server 2017를 기능과 함께 **컴퓨터 학습 서비스**, Python 언어를 사용 하도록 설정 합니다. 이전 버전의 SQL Server는 Python 통합을 지원 하지 않습니다.

> [!NOTE]
> Python의 오픈 소스 배포에서 SQL Server 계산 컨텍스트를 지원 하지 않습니다. 그러나 게시 하 고 Windows에서 Python 응용 프로그램을 사용 해야 할 경우 SQL Server를 설치 하지 않고 Microsoft 컴퓨터 학습 서버를 설치할 수 있습니다. 자세한 내용은 참조 [독립 실행형 R Server 만들기](../r/create-a-standalone-r-server.md)

## <a name="get-more-help"></a>자세한 도움말 보기

이러한 Api에 대 한 전체 설명서는 제품 해제 될 때 사용할 수 있습니다. 한편, RevoScaleR 또는 MicrosoftML 라이브러리에는 해당 함수가 참조 하는 것이 좋습니다.

+ [RevoScaleR](https://msdn.microsoft.com/microsoft-r/scaler/scaler)합니다.
+ [MicrosoftML](https://msdn.microsoft.com/microsoft-r/microsoftml/microsoftml)

모듈을 내보내고 다음 호출 하는 모든 Python 함수에 도움말을 가져와서 `help()`합니다. 예를 들면 `help(revoscalepy)` Python IDE에서 모든 함수 목록이 revoscalepy 모듈 서명으로 반환 합니다.

Visual Studio 용 Python 도구를 사용 하는 경우에 구문 및 인수 도움말을 보려면 IntelliSense를 사용할 수 있습니다. 자세한 내용은 참조 [Visual Studio에서 Python 지원](http://docs.microsoft.com/visualstudio/python/installation), Visual Studio 버전에 일치 하는 확장을 다운로드 하 고 있습니다. Visual Studio 2015 및 2017, Python 또는 이전 버전을 사용할 수 있습니다.

## <a name="see-also"></a>관련 항목:

[Python 자습서](../tutorials/sql-server-python-tutorials.md)
