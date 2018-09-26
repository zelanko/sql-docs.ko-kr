---
title: 포함 된 R 및 Python (SQL Server Machine Learning)에 대 한 NYC Taxi 데이터 및 스크립트 다운로드 | Microsoft Docs
description: 뉴욕 시 택시 샘플 데이터를 다운로드 하 고 데이터베이스를 만들기 위한 지침입니다. R을 포함 하는 방법을 보여 주는 SQL Server 자습서에서 데이터를 사용 하 고 Python에서 SQL Server 저장 프로시저 및 T-SQL 함수입니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/22/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 58a996ae500a27a6878b30fc072bf09a75d4ba43
ms.sourcegitcommit: b7fd118a70a5da9bff25719a3d520ce993ea9def
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/24/2018
ms.locfileid: "46712756"
---
# <a name="nyc-taxi-demo-data-for-sql-server"></a>SQL Server에 대 한 NYC Taxi 데이터
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서에서는 SQL Server에서 데이터베이스 내 분석에 대 한 R 및 Python을 사용 하는 방법에 대 한 자습서에 대 한 시스템을 준비 합니다.

이 연습에서는 샘플 데이터, 환경, 준비에 대 한 PowerShell 스크립트를 다운로드 하 고 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트는 여러 자습서에 사용 되는 파일입니다. 완료 된 경우는 **NYCTaxi_Sample** 데이터베이스가 실습 데모 데이터를 제공 하 고 로컬 인스턴스에에서 사용할 수 있습니다. 

## <a name="prerequisites"></a>사전 요구 사항

인터넷에 연결, PowerShell 및 컴퓨터의 로컬 관리자 권한이 해야 합니다. 있어야 [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) 또는 다른 도구를 개체 만들기를 확인 합니다.

## <a name="download-nyc-taxi-demo-data-and-scripts-from-github"></a>NYC Taxi 데이터 및 스크립트를 Github에서 다운로드

1.  Windows PowerShell 명령 콘솔을 엽니다.
  
    사용 된 **관리자 권한으로 실행** 대상 디렉터리를 만들거나 지정된 된 대상에 파일을 작성 하는 옵션입니다.
  
2.  *DestDir* 매개 변수 값을 로컬 디렉터리로 변경하여 다음 PowerShell 명령을 실행합니다. 여기서 사용한 기본값은 **TempRSQL**입니다.
  
    ```ps
    $source = ‘https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/RSQL/Download_Scripts_SQL_Walkthrough.ps1’  
    $ps1_dest = “$pwd\Download_Scripts_SQL_Walkthrough.ps1”
    $wc = New-Object System.Net.WebClient
    $wc.DownloadFile($source, $ps1_dest)
    .\Download_Scripts_SQL_Walkthrough.ps1 –DestDir ‘C:\tempRSQL’
    ```
  
    *DestDir* 에 지정한 폴더가 존재하지 않을 경우 PowerShell 스크립트를 통해 생성됩니다.
  
    > [!TIP]
    > 오류가 발생 하는 PowerShell 스크립트의 실행 정책을 일시적으로 설정할 수 있습니다 **무제한** Bypass 인수를 사용 하 여 현재 세션에 변경 내용을 범위 지정이 연습에 대해서만 합니다.
    >   
    >````
    > Set\-ExecutionPolicy Bypass \-Scope Process
    >````
    > 이 명령을 실행해도 구성이 변경되지는 않습니다.
  
    인터넷 연결에 따라 다운로드하는 데 시간이 걸릴 수도 있습니다.
  
3.  모든 파일을 다운로드 한 PowerShell 스크립트를 열립니다는 *DestDir* 폴더입니다. PowerShell 명령 프롬프트에서 다음 명령을 실행하고 다운로드된 파일을 검토합니다.
  
    ```
    ls
    ```
  
    **Results:**
  
    ![PowerShell 스크립트로 다운로드한 파일 목록](media/rsql-devtut-filelist.png "PowerShell 스크립트로 다운로드한 파일 목록")

## <a name="create-nyctaxisample-database"></a>NYCTaxi_Sample 데이터베이스 만들기

PowerShell 스크립트를 다운로드 한 파일 중 표시 (**RunSQL_SQL_Walkthrough.ps1**)는 데이터베이스를 만들고 데이터 대량 로드 합니다. 스크립트가 수행하는 작업은 다음과 같습니다.

+ 아직 설치 되지 않은 경우 SQL Native Client 및 SQL 명령줄 유틸리티를 설치 합니다. 이 유틸리티는 **bcp**를 사용하여 데이터베이스에 데이터를 대량 로드하는 데 필요합니다.

+ 데이터베이스 및 테이블 만들기는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 및 데이터 소스를.csv 파일 로부터 대량 삽입 합니다.

+ 여러 SQL 함수 및 여러 자습서에 사용 되는 저장된 프로시저를 만듭니다.

### <a name="modify-the-script-to-use-a-trusted-windows-identity"></a>신뢰할 수 있는 Windows id를 사용 하는 스크립트를 수정 합니다.

스크립트에는 기본적으로 SQL Server 데이터베이스 사용자 로그인 및 암호를 가정합니다. Db_owner Windows 사용자 계정이 있는 경우 Windows id 개체를 만드는 데 사용할 수 있습니다. 이렇게 하려면 엽니다 `RunSQL_SQL_Walkthrough.ps1` 코드 편집기에서 추가 **`-T`** bcp에 bulk insert 명령 (줄 238):

```text
bcp $db_tb in $csvfilepath -t ',' -S $server -f taxiimportfmt.xml -F 2 -C "RAW" -b 200000 -U $u -P $p -T
```

### <a name="run-the-script-to-create-objects"></a>개체를 만드는 스크립트를 실행 합니다.

관리자 PowerShell 명령 프롬프트를 사용 하 여 C:\tempRSQL에서, 다음 명령을 실행 합니다.
  
```ps
.\RunSQL_SQL_Walkthrough.ps1
```
다음 정보를 입력 하 라는 메시지가 표시 됩니다.

- 서버 인스턴스의 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 가 설치 되었습니다. 기본 인스턴스의 경우에서 컴퓨터 이름으로 간단히이 수 있습니다.

- 데이터베이스 이름입니다. 이 자습서에서는 스크립트 가정 `NYCTaxi_Sample`합니다.

- 사용자 이름 및 사용자 암호입니다. 이러한 값에 대 한 SQL Server 데이터베이스 로그인을 입력 합니다. 또는 신뢰할 수 있는 Windows id를 수락 하는 스크립트를 수정한 경우 이러한 값을 비어 두려면 Enter 키를 누릅니다. Windows id 연결에 사용 됩니다.

- 이전 단원에서 다운로드 한 샘플 데이터에 대 한 정규화 된 파일 이름입니다. 예: `C:\tempRSQL\nyctaxi1pct.csv`

이러한 값을 제공한 후 스크립트를 즉시 실행 됩니다. 스크립트 실행의 모든 자리 표시자 이름 중는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트는 사용자의 입력을 사용 하도록 업데이트 됩니다.

## <a name="review-database-objects"></a>데이터베이스 개체를 검토 합니다.
   
스크립트 실행이 완료 되 면 데이터베이스 개체의 존재를 확인 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 사용 하 여 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]입니다. 데이터베이스, 테이블, 함수 및 저장된 프로시저 표시 됩니다.
  
   ![rsql_devtut_BrowseTables](media/rsql-devtut-browsetables.png "rsql_devtut_BrowseTables")

> [!NOTE]
> 데이터베이스 개체가 이미 있는 경우에는 다시 만들 수 없습니다.
>   
> 테이블이 이미 있는 경우 데이터가 추가되며 덮어쓰지 않습니다. 따라서 스크립트를 실행하기 전에 기존 개체를 모두 삭제해야 합니다.

### <a name="objects-in-nyctaxisample-database"></a>NYCTaxi_Sample 데이터베이스의 개체

다음 표에서 NYC Taxi 데모 데이터베이스에서 생성 되는 개체를 보여 줍니다. 만 한 PowerShell 스크립트를 실행 하면 되지만 (`RunSQL_SQL_Walkthrough.ps1`), 해당 스크립트에 개체를 만들 데이터베이스의 다른 SQL 스크립트를 호출 합니다. 각 개체를 만드는 데 사용 되는 스크립트에 대 한 설명에 언급 된 합니다.

|**개체 이름**|**개체 유형**|**설명**|
|----------|------------------------|---------------|
|**NYCTaxi_Sample** | database |만들기-db-tb-업로드-data.sql 스크립트에 의해 생성 됩니다. 데이터베이스와 다음 두 개의 테이블을 만듭니다.<br /><br />dbo.nyctaxi_sample 테이블: 주 NYC Taxi 데이터 집합을 포함 합니다. 저장소 및 쿼리 성능 향상을 위해 클러스터형 columnstore 인덱스가 테이블에 추가됩니다. NYC Taxi 데이터 집합의 1% 샘플이이 테이블에 삽입 됩니다.<br /><br />dbo.nyc_taxi_models 테이블: 고급 분석 학습 된 모델을 유지 하는 데 사용 합니다.|
|**fnCalculateDistance** |스칼라 반환 함수(scalar-valued function) | FnCalculateDistance.sql 스크립트에 의해 생성 됩니다. 승차 및 하 차 위치 사이의 직접 거리를 계산합니다. 이 함수는 [데이터 기능 만들기](sqldev-create-data-features-using-t-sql.md), [학습 모델을 저장 하 고](../r/sqldev-train-and-save-a-model-using-t-sql.md) 하 고 [R 모델 운영 화](sqldev-operationalize-the-model.md)합니다.|
|**fnEngineerFeatures** |테이블 반환 함수(table-valued function) | FnEngineerFeatures.sql 스크립트에 의해 생성 됩니다. 모델 학습을 위한 새로운 데이터 기능을 만듭니다. 이 함수는 [데이터 기능 만들기](sqldev-create-data-features-using-t-sql.md) 하 고 [R 모델 운영 화](sqldev-operationalize-the-model.md)합니다.|
|**PlotHistogram** |저장 프로시저 | PlotHistogram.sql 스크립트에 의해 생성 됩니다. 변수 히스토그램을 그린에 R 함수를 호출 하 고 그림을 이진 개체로 반환 합니다. 이 저장된 프로시저는 [데이터 탐색 및 시각화](sqldev-explore-and-visualize-the-data.md)합니다.|
|**PlotInOutputFiles** |저장 프로시저| PlotInOutputFiles.sql 스크립트에 의해 생성 됩니다. R 함수를 사용 하 여 그래픽을 만든 다음 로컬 PDF 파일로 출력을 저장 합니다. 이 저장된 프로시저는 [데이터 탐색 및 시각화](sqldev-explore-and-visualize-the-data.md)합니다.|
|**PersistModel** |저장 프로시저 | PersistModel.sql 스크립트에 의해 생성 됩니다. Varbinary 데이터 형식으로 직렬화 된 지정된 된 테이블에 기록 하는 모델을 사용 합니다. |
|**PredictTip**  |저장 프로시저 |PredictTip.sql 스크립트에 의해 생성 됩니다. 모델을 사용 하 여 예측을 만들려면 학습된 된 모델을 호출 합니다. 저장 프로시저는 쿼리를 입력 매개 변수로 사용하고 입력된 행에 대한 점수를 포함하는 숫자 값 열을 반환합니다. 이 저장된 프로시저는 [R 모델 운영 화](sqldev-operationalize-the-model.md)합니다.|
|**PredictTipSingleMode**  |저장 프로시저| PredictTipSingleMode.sql 스크립트에 의해 생성 됩니다. 모델을 사용 하 여 예측을 만들려면 학습된 된 모델을 호출 합니다. 이 저장 프로시저는 새 관찰을 개별 기능 값이 인라인 매개 변수로 전달되는 입력으로 사용하고 새 관찰의 결과를 예측하는 값을 반환합니다. 이 저장된 프로시저는 [R 모델 운영 화](sqldev-operationalize-the-model.md)합니다.|
|**TrainTipPredictionModel**  |저장 프로시저|TrainTipPredictionModel.sql 스크립트에 의해 생성 됩니다. R 패키지를 호출 하 여 로지스틱 회귀 모델을 학습 합니다. 모델은 tipped 열의 값을 예측하며 임의로 선택된 70%의 데이터를 사용하여 학습됩니다. 저장 프로시저의 출력은 nyc_taxi_models 테이블에 저장된 학습된 모델입니다. 이 저장된 프로시저는 [학습 모델을 저장 하 고](../r/sqldev-train-and-save-a-model-using-t-sql.md)입니다.|

## <a name="query-data-for-verification"></a>확인에 대 한 데이터를 쿼리 합니다.

유효성 검사 단계로, 데이터가 업로드 되었는지 확인 하는 쿼리를 실행 합니다.

1. 데이터베이스에서 개체 탐색기에서 확장을 **NYCTaxi_Sample** 데이터베이스를 백업할, 테이블 폴더를 엽니다.

2. 마우스 오른쪽 단추로 클릭 합니다 **dbo.nyctaxi_sample** 선택한 **상위 1000 개의 행 선택** 일부 데이터를 반환 합니다.

## <a name="next-steps"></a>다음 단계

NYC Taxi 샘플 데이터 실습에 대 한 출시 되었습니다.

+ [SQL Server에서 R을 사용 하 여 데이터베이스 내 분석에 알아봅니다.](sqldev-in-database-r-for-sql-developers.md)