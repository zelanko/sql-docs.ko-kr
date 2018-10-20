---
title: 2 단계 PowerShell을 사용 하 여 SQL Server로 데이터 가져오기 | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/07/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: f8b90a18c0cdce9c4c2c73db4b599e488570f018
ms.sourcegitcommit: 3cd6068f3baf434a4a8074ba67223899e77a690b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/19/2018
ms.locfileid: "49461869"
---
# <a name="step-2-import-data-to-sql-server-using-powershell"></a>2 단계: PowerShell을 사용 하 여 SQL Server로 데이터 가져오기
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서는 자습서에 일부 [SQL 개발자를 위한 데이터베이스 내 Python 분석](sqldev-in-database-python-for-sql-developers.md)합니다. 

이 단계를 연습에 필요한 데이터베이스 개체를 만드는 다운로드 한 스크립트 중 하나 실행 합니다. 스크립트는 몇 가지 저장된 프로시저도 만들고 지정한 데이터베이스의 테이블에 샘플 데이터를 업로드 합니다.

## <a name="create-database-objects-and-load-data"></a>데이터베이스 개체를 만들고 데이터를 로드 합니다.

PowerShell 스크립트를 다운로드 한 파일 중 표시 `RunSQL_SQL_Walkthrough.ps1`합니다. 이 스크립트의 목적은 연습에 대 한 환경 준비 하는 것입니다.

이 스크립트는 다음 작업을 수행합니다.

- 아직 설치 되지 않은 경우 SQL Native Client 및 SQL 명령줄 유틸리티를 설치 합니다. 이 유틸리티는 **bcp**를 사용하여 데이터베이스에 데이터를 대량 로드하는 데 필요합니다.

- 데이터베이스를 만들고 테이블을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 및 테이블로 데이터를 대량 삽입 합니다.

- 여러 SQL 함수 및 저장된 프로시저를 만듭니다.

문제에 봉착 한 경우에 수동으로 단계를 수행 하려면 참조로 스크립트를 사용할 수 있습니다.

### <a name="modify-the-script-to-use-a-trusted-windows-identity"></a>신뢰할 수 있는 Windows id를 사용 하는 스크립트를 수정 합니다.

스크립트에는 기본적으로 SQL Server 데이터베이스 사용자 로그인 및 암호를 가정합니다. Db_owner Windows 사용자 계정이 있는 경우 Windows id 개체를 만드는 데 사용할 수 있습니다. 이렇게 하려면 엽니다 `RunSQL_SQL_Walkthrough.ps1` 추가할 코드 편집기에서 **`-T`** bcp에 bulk insert 명령:

```text
bcp $db_tb in $csvfilepath -t ',' -S $server -f taxiimportfmt.xml -F 2 -C "RAW" -b 200000 -U $u -P $p -T
```

### <a name="run-the-script"></a>스크립트를 실행 합니다.

1. 관리자 권한으로 PowerShell 명령 프롬프트를 엽니다. 없는 경우 이미 이전 단계에서 만든 폴더에서를 폴더로 이동한 후 다음 명령을 실행 합니다.
  
    ```ps
    .\RunSQL_SQL_Walkthrough.ps1
    ```

2. 스크립트가 다음 정보를 표시 합니다.

    - 이름 또는 주소의 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Python 사용 하 여 Machine Learning Services가 설치 된 인스턴스.
    - 인스턴스의 계정에 대한 사용자 이름 및 암호. 사용 하는 계정에는 데이터베이스, 테이블 및 저장된 프로시저를 만들고 테이블에 부하 데이터를 대량으로 수가 있어야 합니다. 
    - 사용자 이름과 암호를 입력하지 않으면 Windows ID가 SQL Server에 로그인하는 데 사용됩니다.
    - 방금 다운로드한 샘플 데이터 파일의 경로 및 파일 이름. 예를 들어 IPv4 주소를 사용하는 경우 `C:\temp\pysql\nyctaxi1pct.csv`

    > [!NOTE]
    > 데이터를 성공적으로 로드 하려면 라이브러리 xmlrw.dll bcp.exe와 동일한 폴더에 있어야 합니다.

3. 스크립트도 수정 된 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트는 이전에 다운로드 한 데이터베이스 이름 및 사용자를 사용 하 여 자리 표시자 대체 이름을 제공 합니다.
  
4. 스크립트가 완료 되 면 로그인은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스는 데이터베이스 테이블을 확인 하려면 사용자가 지정한 로그인을 사용 하 여 함수 및 저장된 프로시저를 만들었습니다. 다음 이미지에서 개체를 보여 줍니다. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]합니다.

    ![SSMS에서 테이블 찾아보기](media/sqldev-python-browsetables1.png "SSMS에서 테이블 보기")

    > [!NOTE]
    > 데이터베이스 개체가 이미 있는 경우 다시 만들 수 없습니다.
    > 
    > 동일한 이름 및 스키마의 기존 테이블을 발견 되 면 데이터 추가 되며 덮어쓰지 않습니다. 따라서 반드시를 삭제 하거나 스크립트를 실행 하기 전에 기존 테이블을 자릅니다.

## <a name="list-of-stored-procedures-and-functions"></a>저장된 프로시저 및 함수 목록

다음 SQL Server 개체를 스크립트에 의해 생성 됩니다.

|**SQL 스크립트 파일 이름**|**함수**|
|------|------|
|create-db-tb-upload-data.sql|데이터베이스와 다음 두 개의 테이블을 만듭니다.<br /><br />nyctaxi_sample: 주 NYC Taxi 데이터 집합을 포함합니다. 저장소 및 쿼리 성능 향상을 위해 클러스터형 columnstore 인덱스가 테이블에 추가됩니다. NYC Taxi 데이터 집합의 1% 샘플이 이 테이블에 삽입됩니다.<br /><br />nyc_taxi_models: 학습된 고급 분석 모델을 저장하는 데 사용됩니다.|
|fnCalculateDistance.sql|승하차 위치 사이의 직접 거리를 계산하는 스칼라 반환 함수를 만듭니다.|
|fnEngineerFeatures.sql|모델 학습을 위한 새로운 데이터 특성을 만드는 테이블 반환 함수를 만듭니다.|
|TrainingTestingSplit.sql|Nyctaxi_sample 테이블의에서 데이터를 두 부분으로 분할: nyctaxi_sample_training 및 nyctaxi_sample_testing 합니다.|
|PredictTipSciKitPy.sql|학습된 된 모델을 호출 하는 저장된 프로시저를 만듭니다 (scikit-알아봅니다) 모델을 사용 하 여 예측을 만듭니다. 저장 프로시저는 쿼리를 입력 매개 변수로 사용하고 입력된 행에 대한 점수를 포함하는 숫자 값 열을 반환합니다.|
|PredictTipRxPy.sql|모델을 사용 하 여 예측을 만들려면 학습된 된 모델 (revoscalepy)를 호출 하는 저장된 프로시저를 만듭니다. 저장 프로시저는 쿼리를 입력 매개 변수로 사용하고 입력된 행에 대한 점수를 포함하는 숫자 값 열을 반환합니다.|
|PredictTipSingleModeSciKitPy.sql|학습된 된 모델을 호출 하는 저장된 프로시저를 만듭니다 (scikit-알아봅니다) 모델을 사용 하 여 예측을 만듭니다. 이 저장 프로시저는 새 관찰을 개별 기능 값이 인라인 매개 변수로 전달되는 입력으로 사용하고 새 관찰의 결과를 예측하는 값을 반환합니다.|
|PredictTipSingleModeRxPy.sql|모델을 사용 하 여 예측을 만들려면 학습된 된 모델 (revoscalepy)를 호출 하는 저장된 프로시저를 만듭니다. 이 저장 프로시저는 새 관찰을 개별 기능 값이 인라인 매개 변수로 전달되는 입력으로 사용하고 새 관찰의 결과를 예측하는 값을 반환합니다.|

이 연습의 뒷부분에서는 이러한 추가 저장된 프로시저를 만듭니다.
    
|**SQL 스크립트 파일 이름**|**함수**|
|------|------|
|SerializePlots.sql||데이터 탐색을 위한 저장 프로시저를 만듭니다. 이 저장된 프로시저 Python을 사용 하 여 그래픽을 만들고 그래프 개체를 serialize 합니다.|
|TrainTipPredictionModelSciKitPy.sql|로지스틱 회귀 모델을 학습 하는 저장된 프로시저를 만듭니다 (scikit-알아보기). Tipped 열의 값을 예측 모델과 데이터를 임의로 선택 된 60%를 사용 하 여 학습 됩니다. 저장 프로시저의 출력은 nyc_taxi_models 테이블에 저장된 학습된 모델입니다.|
|TrainTipPredictionModelRxPy.sql|(Revoscalepy) 로지스틱 회귀 모델을 학습 하는 저장된 프로시저를 만듭니다. Tipped 열의 값을 예측 모델과 데이터를 임의로 선택 된 60%를 사용 하 여 학습 됩니다. 저장 프로시저의 출력은 nyc_taxi_models 테이블에 저장된 학습된 모델입니다.|

## <a name="next-step"></a>다음 단계

[3단계: 데이터 탐색 및 시각화](sqldev-py3-explore-and-visualize-the-data.md)

## <a name="previous-step"></a>이전 단계

[1단계: 샘플 데이터 다운로드](demo-data-nyctaxi-in-sql.md)

