---
title: PowerShell (SQL Server 기계 학습)를 사용 하 여 2 단원 준비 R 자습서 환경 | Microsoft Docs
description: SQL Server에서 R을 포함 하는 방법을 보여 주는 자습서 저장 프로시저 및 T-SQL 함수
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/07/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 1280d7c82d48c8ed596271cd7a73fa13ec1664c7
ms.sourcegitcommit: b52b5d972b1a180e575dccfc4abce49af1a6b230
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/08/2018
ms.locfileid: "35249746"
---
# <a name="lesson-2-set-up-the-tutorial-environment-using-powershell"></a>2 단원: PowerShell을 사용 하 여 자습서 환경 설정
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서는 SQL Server에서 R을 사용 하는 방법에 대 한 SQL 개발자를 위한 자습서의 일부입니다.

이 단계에서는 연습에 필요한 데이터베이스 개체를 만드는 PowerShell 스크립트를 실행 합니다. 스크립트를 만들고 이전 단계에서 가져온 예제 데이터를 사용 하 여 데이터베이스를 로드 합니다. 또한 함수 및 자습서 전체에서 사용 되는 저장된 프로시저를 만듭니다.

## <a name="create-and-load-database-objects"></a>만들기 및 데이터베이스 개체를 로드 합니다.

PowerShell 스크립트를 다운로드 한 파일 중에서 표시 됩니다 (`RunSQL_SQL_Walkthrough.ps1`) 연습에 대 한 환경 준비를 합니다. 스크립트가 수행하는 작업은 다음과 같습니다.

- 아직 설치 되지 않은 경우는 SQL Native Client 및 SQL 명령줄 유틸리티를 설치 합니다. 이 유틸리티는 **bcp**를 사용하여 데이터베이스에 데이터를 대량 로드하는 데 필요합니다.

- 에 데이터베이스 및 테이블 만들기는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 선택한 데이터 소스는.csv 파일 로부터 대량 삽입 합니다.

- 여러 SQL 함수 및 저장된 프로시저를 만듭니다.

### <a name="modify-the-script-to-use-a-trusted-windows-identity"></a>신뢰할 수 있는 Windows id를 사용 하는 스크립트를 수정 합니다.

기본적으로 스크립트는 SQL Server 데이터베이스 사용자 로그인 및 암호를 가정합니다. 인 경우 db_owner Windows 사용자 계정에 개체를 만들 Windows id를 사용할 수 있습니다. 이렇게 하려면 열고 `RunSQL_SQL_Walkthrough.ps1` 코드 편집기에서 및 추가 **`-T`** bcp에 bulk insert 명령 (라인 238):

```text
bcp $db_tb in $csvfilepath -t ',' -S $server -f taxiimportfmt.xml -F 2 -C "RAW" -b 200000 -U $u -P $p -T
```

### <a name="run-the-script-to-create-objects"></a>개체를 만드는 스크립트를 실행 합니다.

관리자 권한으로 PowerShell 명령 프롬프트를 열고 다음 명령을 실행합니다.
  
```ps
.\RunSQL_SQL_Walkthrough.ps1
```
다음 정보를 입력 하 라는 메시지가 표시 됩니다.

- 서버 인스턴스를 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 가 설치 되어 있습니다. 기본 인스턴스의 경우이 컴퓨터 이름 처럼 간단할 수 있습니다.

- 데이터베이스 이름입니다. 스크립트에서는이 자습서에서는 다음을 가정 합니다. `TaxiNYC_Sample`합니다.

- 사용자 이름 및 사용자 암호입니다. 이러한 값에 대 한 SQL Server 데이터베이스 로그인을 입력 합니다. 또는 신뢰할 수 있는 Windows id를 수락 하는 스크립트를 수정한 경우 이러한 값을 비워 두 게 Enter 키를 누릅니다. Windows id는 연결에 사용 됩니다.

- 이전 단원에서 다운로드 한 샘플 데이터에 대 한 정규화 된 파일 이름입니다. 예: `C:\tempRSQL\nyctaxi1pct.csv`

이러한 값을 입력 한 후 스크립트 즉시 실행 됩니다. 스크립트 실행의 모든 자리 표시자 이름 중에서 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트 제공한 입력을 사용 하도록 업데이트 됩니다.

## <a name="review-database-objects"></a>데이터베이스 개체를 검토 합니다.
   
데이터베이스 개체에 있는 스크립트 실행이 완료 되 면 확인는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 사용 하 여 인스턴스 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]합니다. 데이터베이스, 테이블, 함수 및 저장된 프로시저 표시 됩니다.
  
   ![rsql_devtut_BrowseTables](media/rsql-devtut-browsetables.png "rsql_devtut_BrowseTables")

> [!NOTE]
> 데이터베이스 개체가 이미 있는 경우에는 다시 만들 수 없습니다.
>   
> 테이블이 이미 있는 경우 데이터가 추가되며 덮어쓰지 않습니다. 따라서 스크립트를 실행하기 전에 기존 개체를 모두 삭제해야 합니다.

## <a name="objects-used-in-this-tutorial"></a>이 자습서에 사용 되는 개체

다음 표에서이 단원에서 만든 개체를 요약 합니다. PowerShell 스크립트를 하나씩만 실행할 수도 있지만 (`RunSQL_SQL_Walkthrough.ps1`), 해당 스크립트에 개체를 만들 데이터베이스의 다른 SQL 스크립트를 호출 합니다. 각 개체를 만드는 사용 되는 스크립트는 설명에 언급 됩니다.

|**개체 이름**|**개체 유형**|**설명**|
|----------|------------------------|---------------|
|**TaxiNYC_Sample** | database |스크립트 만들기-db-t b-업로드-data.sql 만들어집니다. 데이터베이스와 다음 두 개의 테이블을 만듭니다.<br /><br />dbo.nyctaxi_sample 테이블: 주 NYC 택시 데이터 집합을 포함 합니다. 저장소 및 쿼리 성능 향상을 위해 클러스터형 columnstore 인덱스가 테이블에 추가됩니다. NYC 택시 데이터 집합의 1% 샘플은이 테이블에 삽입 됩니다.<br /><br />dbo.nyc_taxi_models 테이블: 고급 분석 학습 된 모델을 유지 하는 데 사용 합니다.|
|**fnCalculateDistance** |스칼라 반환 함수(scalar-valued function) | FnCalculateDistance.sql 스크립트 만들어집니다. 픽업 및 dropoff 위치 간에 직접 거리를 계산합니다. 이 함수는 사용 [데이터 기능을 만드는](../tutorials/sqldev-create-data-features-using-t-sql.md), [학습 모델 저장 및](sqldev-train-and-save-a-model-using-t-sql.md) 및 [R 모델을 운용](../tutorials/sqldev-operationalize-the-model.md)합니다.|
|**fnEngineerFeatures** |테이블 반환 함수(table-valued function) | FnEngineerFeatures.sql 스크립트 만들어집니다. 모델 학습을 위해 새로운 데이터 기능을 만듭니다. 이 함수는 사용 [데이터 기능을 만드는](../tutorials/sqldev-create-data-features-using-t-sql.md) 및 [R 모델을 운용](../tutorials/sqldev-operationalize-the-model.md)합니다.|
|**PlotHistogram** |저장 프로시저 | PlotHistogram.sql 스크립트 만들어집니다. 변수 histogram을 그리는 데 R 함수를 호출 하 고 이진 개체로 플롯을 반환 합니다. 이 저장된 프로시저는 [탐색 하 고 데이터를 시각화](../tutorials/sqldev-explore-and-visualize-the-data.md)합니다.|
|**PlotInOutputFiles** |저장 프로시저| PlotInOutputFiles.sql 스크립트 만들어집니다. R 함수를 사용 하 여 그래픽을 만들고 로컬 PDF 파일로 출력을 저장 합니다. 이 저장된 프로시저는 [탐색 하 고 데이터를 시각화](../tutorials/sqldev-explore-and-visualize-the-data.md)합니다.|
|**PersistModel** |저장 프로시저 | PersistModel.sql 스크립트 만들어집니다. Varbinary 데이터 형식으로 serialize 된 지정된 된 테이블에 기록 되는 모델을 사용 합니다. |
|**PredictTip**  |저장 프로시저 |PredictTip.sql 스크립트 만들어집니다. 모델을 사용 하 여 예측을 만들 수는 학습 된 모델을 호출 합니다. 저장 프로시저는 쿼리를 입력 매개 변수로 사용하고 입력된 행에 대한 점수를 포함하는 숫자 값 열을 반환합니다. 이 저장된 프로시저는 [R 모델을 운용](../tutorials/sqldev-operationalize-the-model.md)합니다.|
|**PredictTipSingleMode**  |저장 프로시저| PredictTipSingleMode.sql 스크립트 만들어집니다. 모델을 사용 하 여 예측을 만들 수는 학습 된 모델을 호출 합니다. 이 저장 프로시저는 새 관찰을 개별 기능 값이 인라인 매개 변수로 전달되는 입력으로 사용하고 새 관찰의 결과를 예측하는 값을 반환합니다. 이 저장된 프로시저는 [R 모델을 운용](../tutorials/sqldev-operationalize-the-model.md)합니다.|
|**TrainTipPredictionModel**  |저장 프로시저|TrainTipPredictionModel.sql 스크립트 만들어집니다. R 패키지를 호출 하 여 로지스틱 회귀 모델을 학습 합니다. 모델은 tipped 열의 값을 예측하며 임의로 선택된 70%의 데이터를 사용하여 학습됩니다. 저장 프로시저의 출력은 nyc_taxi_models 테이블에 저장된 학습된 모델입니다. 이 저장된 프로시저는 [학습 모델 저장 및](sqldev-train-and-save-a-model-using-t-sql.md)합니다.|

## <a name="next-lesson"></a>다음 단원

[3 단원: 데이터를 탐색하고 시각화하기](../tutorials/sqldev-explore-and-visualize-the-data.md)

## <a name="previous-lesson"></a>이전 단원

[1 단원: 예제 데이터 다운로드](../tutorials/sqldev-download-the-sample-data.md)
