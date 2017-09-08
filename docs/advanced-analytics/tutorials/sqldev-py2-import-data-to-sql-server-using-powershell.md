---
title: "2단계: PowerShell을 사용하여 SQL Server로 데이터 가져오기 | Microsoft 문서"
ms.custom: 
ms.date: 05/25/2017
ms.prod: sql-server-vnext-ctp2
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2017
dev_langs:
- Python
- TSQL
ms.assetid: 
caps.latest.revision: 2
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 62a06d6c442428132f84b3f8e5a665e872a8d361
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="step-2-import-data-to-sql-server-using-powershell"></a>2단계: PowerShell을 사용하여 SQL Server로 데이터 가져오기

이 단계에서는 다운로드한 스크립트 중 하나를 실행하여 연습에 필요한 데이터베이스 개체를 만듭니다. 또한 스크립트는 사용할 대부분의 저장 프로시저를 만들고 지정한 데이터베이스의 테이블에 샘플 데이터를 업로드합니다.

## <a name="create-sql-objects-and-data"></a>SQL 개체 및 데이터 만들기

다운로드한 파일 중에 PowerShell 스크립트가 있어야 합니다. 연습을 위한 환경을 준비하려면 이 스크립트를 실행합니다.  스크립트는 다음과 같은 작업을 수행합니다.

- 아직 설치 되지 않은 경우는 SQL Native Client 및 SQL 명령줄 유틸리티를 설치 합니다. 이 유틸리티는 **bcp**를 사용하여 데이터베이스에 데이터를 대량 로드하는 데 필요합니다.

- 에 데이터베이스와 테이블을 만듭니다는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 및 데이터를 테이블로 대량 삽입 합니다.

- 여러 SQL 함수 및 저장된 프로시저를 만듭니다.

### <a name="run-the-script"></a>스크립트 실행

1. 관리자 권한으로 PowerShell 명령 프롬프트를 열고 다음 명령을 실행합니다.
  
    ```  
    .\RunSQL_SQL_Walkthrough.ps1  
    ```  

    다음 정보를 입력하라는 메시지가 표시됩니다.
    - 이름 또는 주소는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 기계 학습 Python 사용 하 여 서비스를 설치한 인스턴스
    - 인스턴스의 계정에 대한 사용자 이름 및 암호. 사용하는 계정이 데이터베이스를 만들고, 테이블 및 저장 프로시저를 만들고, 테이블에 데이터를 업로드할 수 있어야 합니다. 사용자 이름 및 암호를 제공 하지 않으면 Windows id에 SQL Server 로그인에 사용 됩니다.
    - 방금 다운로드한 샘플 데이터 파일의 경로 및 파일 이름. 예를 들어 IPv4 주소를 사용하는 경우 `C:\tempRSQL\nyctaxi1pct.csv`

    > [!NOTE]
    > 프로그램 xmlrw.dll 프로그램 bcp.exe와 같은 폴더에 있는지 확인 합니다. 그렇지 않으면 위로 복사 하십시오.

2.  이 단계의 일부로, 모든 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트가 자리 표시자를 스크립트 입력으로 제공한 데이터베이스 이름 및 사용자 이름으로 대체하도록 수정됩니다.
  
3. 스크립트를 통해 생성된 저장 프로시저 및 함수를 검토합니다.
     
    |**SQL 스크립트 파일 이름**|**함수**|
    |------|------|
    |create-db-tb-upload-data.sql|데이터베이스와 다음 두 개의 테이블을 만듭니다.<br /><br />nyctaxi_sample: 주 NYC Taxi 데이터 집합을 포함합니다. 저장소 및 쿼리 성능 향상을 위해 클러스터형 columnstore 인덱스가 테이블에 추가됩니다. NYC Taxi 데이터 집합의 1% 샘플이 이 테이블에 삽입됩니다.<br /><br />nyc_taxi_models: 학습된 고급 분석 모델을 저장하는 데 사용됩니다.|
    |fnCalculateDistance.sql|승하차 위치 사이의 직접 거리를 계산하는 스칼라 반환 함수를 만듭니다.|
    |fnEngineerFeatures.sql|모델 학습을 위한 새로운 데이터 기능을 만드는 테이블 반환 함수를 만듭니다.|
    |TrainingTestingSplit.sql|Nyctaxi_sample 테이블의에서 데이터를 두 부분으로 분할: nyctaxi_sample_training 및 nyctaxi_sample_testing 합니다.|
    |PredictTipSciKitPy.sql|학습 된 모델을 호출 하는 저장된 프로시저를 만듭니다 (scikit-자세한) 모델을 사용 하 여 예측을 만듭니다. 저장 프로시저는 쿼리를 입력 매개 변수로 사용하고 입력된 행에 대한 점수를 포함하는 숫자 값 열을 반환합니다.|
    |PredictTipRxPy.sql|모델을 사용 하 여 예측을 만들 수는 학습 된 모델 (revoscalepy)를 호출 하는 저장된 프로시저를 만듭니다. 저장 프로시저는 쿼리를 입력 매개 변수로 사용하고 입력된 행에 대한 점수를 포함하는 숫자 값 열을 반환합니다.|
    |PredictTipSingleModeSciKitPy.sql|학습 된 모델을 호출 하는 저장된 프로시저를 만듭니다 (scikit-자세한) 모델을 사용 하 여 예측을 만듭니다. 이 저장 프로시저는 새 관찰을 개별 기능 값이 인라인 매개 변수로 전달되는 입력으로 사용하고 새 관찰의 결과를 예측하는 값을 반환합니다.|
    |PredictTipSingleModeRxPy.sql|모델을 사용 하 여 예측을 만들 수는 학습 된 모델 (revoscalepy)를 호출 하는 저장된 프로시저를 만듭니다. 이 저장 프로시저는 새 관찰을 개별 기능 값이 인라인 매개 변수로 전달되는 입력으로 사용하고 새 관찰의 결과를 예측하는 값을 반환합니다.|
  
4. 이 연습의 뒷부분에서는 몇 개의 저장 프로시저를 추가로 만듭니다.
    
    |**SQL 스크립트 파일 이름**|**함수**|
    |------|------|
    |SerializePlots.sql|데이터 탐색을 위한 저장 프로시저를 만듭니다. 이 저장된 프로시저 Python을 사용 하는 그래픽을 만들고 그래프 개체를 serialize 합니다.|
    |TrainTipPredictionModelSciKitPy.sql|로지스틱 회귀 모델을 학습 하는 저장된 프로시저를 만듭니다 (scikit-자세한). 기울어진 열의 값을 예측 모델과 데이터의 임의로 선택 된 60%를 사용 하 여 학습 됩니다. 저장 프로시저의 출력은 nyc_taxi_models 테이블에 저장된 학습된 모델입니다.|
    |TrainTipPredictionModelRxPy.sql|(Revoscalepy) 로지스틱 회귀 모델을 학습 하는 저장된 프로시저를 만듭니다. 기울어진 열의 값을 예측 모델과 데이터의 임의로 선택 된 60%를 사용 하 여 학습 됩니다. 저장 프로시저의 출력은 nyc_taxi_models 테이블에 저장된 학습된 모델입니다.|
  
3. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 지정한 로그인으로 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 인스턴스에 로그인하여 생성된 데이터베이스, 테이블, 함수 및 저장 프로시저를 볼 수 있는지 확인합니다.

    ![SSMS에서 테이블 찾아보기](media/sqldev-python-browsetables1.png "SSMS의 테이블 보기")

    > [!NOTE]
    > 데이터베이스 개체가 이미 있는 경우에는 다시 만들 수 없습니다. 테이블이 이미 있는 경우 데이터가 추가되며 덮어쓰지 않습니다. 따라서 스크립트를 실행하기 전에 기존 개체를 모두 삭제해야 합니다.
    > 지침에 따라 [여기](https://docs.microsoft.com/en-us/sql/advanced-analytics/r/set-up-sql-server-r-services-in-database#bkmk_enableFeature) 외부 스크립트 서비스를 활성화 합니다.
    


## <a name="next-step"></a>다음 단계

[3단계: 데이터 탐색 및 시각화](sqldev-py3-explore-and-visualize-the-data.md)

## <a name="previous-step"></a>이전 단계

[1단계: 샘플 데이터 다운로드](sqldev-py1-download-the-sample-data.md)

## <a name="see-also"></a>관련 항목:

[기계 학습 Python 사용 하 여 서비스](../python/sql-server-python-services.md)



