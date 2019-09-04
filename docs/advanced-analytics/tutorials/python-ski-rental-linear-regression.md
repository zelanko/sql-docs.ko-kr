---
title: 'Python 자습서: Ski 대 여 (선형 회귀)'
description: 이 자습서에서는 SQL Server Machine Learning Services에서 Python 및 선형 회귀를 사용 하 여 ski 대 여의 수를 예측 합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/03/2019
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 718487ba55b2b8db8f16b59df5785cf78ff501f1
ms.sourcegitcommit: ecb19d0be87c38a283014dbc330adc2f1819a697
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70242511"
---
# <a name="python-tutorial-predict-ski-rental-with-linear-regression-in-sql-server-machine-learning-services"></a>Python 자습서: SQL Server Machine Learning Services에서 선형 회귀를 사용 하 여 ski 임대 예측
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

이 네 부분으로 구성 된 자습서 시리즈에서는 [SQL Server Machine Learning Services](../what-is-sql-server-machine-learning.md) 에서 Python 및 선형 회귀를 사용 하 여 ski 대 여의 수를 예측 합니다. 이 자습서에서는 [Azure Data Studio에서 python 노트북](../../azure-data-studio/sql-notebooks.md)을 사용 하지만 사용자 고유의 python IDE (통합 개발 환경)를 사용할 수도 있습니다.

Ski 임대 비즈니스를 소유 하 고 있으며 향후 날짜에 대 여 수를 예측 하려는 경우를 가정해 보겠습니다. 이 정보는 재고, 직원 및 시설을 준비 하는 데 도움이 됩니다.

이 시리즈의 첫 번째 부분에서는 필수 구성 요소를 설정 합니다. 2-3 부에서는 Jupyter 노트북에서 일부 Python 스크립트를 개발 하 여 데이터를 준비 하 고 기계 학습 모델을 학습 합니다. 그런 다음, 3 부에서는 T-sql 저장 프로시저를 사용 하 여 SQL Server 내에서 Python 스크립트를 실행 합니다.

이 문서에서는 다음 방법을 설명합니다.

> [!div class="checklist"]
> * 예제 데이터베이스를 SQL Server으로 가져오기 

[2 부](python-ski-rental-linear-regression-prepare-data.md)에서는 SQL Server에서 python 데이터 프레임으로 데이터를 로드 하 고 python에서 데이터를 준비 하는 방법을 알아봅니다.

[3 부](python-ski-rental-linear-regression-train-model.md)에서는 Python에서 선형 회귀 모델을 학습 하는 방법을 배웁니다.

[4 부](python-ski-rental-linear-regression-deploy-model.md)에서는 SQL Server에 모델을 저장 한 다음 2 단계와 3 부에서 개발한 Python 스크립트에서 저장 프로시저를 만드는 방법에 대해 알아봅니다. 저장 프로시저는 새 데이터를 기반으로 예측을 수행 하기 위해 SQL Server에서 실행 됩니다.

## <a name="prerequisites"></a>사전 요구 사항

* SQL Server Machine Learning Services-Machine Learning Services을 설치 하는 방법에 대 한 자세한 내용은 [Windows 설치 가이드](../install/sql-machine-learning-services-windows-install.md) 또는 [Linux 설치 가이드](../../linux/sql-server-linux-setup-machine-learning.md?toc=%2Fsql%2Fadvanced-analytics%2Ftoc.json)를 참조 하세요.

* Python IDE-이 자습서는 [Azure Data Studio](../../azure-data-studio/what-is.md)에서 Python 노트북을 사용 합니다. 자세한 내용은 [Azure Data Studio에서 노트북을 사용 하는 방법](../../azure-data-studio/sql-notebooks.md)을 참조 하세요. 

    Jupyter 노트북 또는 [python 확장](https://marketplace.visualstudio.com/items?itemName=ms-python.python) 및 [mssql 확장](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql)을 사용 하 여 [VISUAL STUDIO CODE](https://code.visualstudio.com/docs) 같은 사용자 고유의 python IDE를 사용할 수도 있습니다. 

* [revoscalepy](../python/ref-py-revoscalepy.md) package- **revoscalepy** 패키지는 SQL Server Machine Learning Services에 포함 되어 있습니다. 클라이언트 컴퓨터에서 패키지를 사용 하려면 로컬로이 패키지를 설치 하는 옵션을 사용 하 여 [Python 개발을 위한 데이터 과학 클라이언트 설정](../python/setup-python-client-tools-sql.md) 을 참조 하세요.

    Azure Data Studio에서 Python 노트북을 사용 하는 경우 다음과 같은 추가 단계를 수행 하 여 **revoscalepy**를 사용 합니다.

    1. Azure Data Studio 열기
    1. **파일** 메뉴에서 **기본 설정** 및 **설정** 을 차례로 선택 합니다.
    1. **확장** 확장 및 **노트북 구성** 선택
    1. **Python 경로**아래에서 라이브러리를 설치한 경로를 입력 합니다 (예: `C:\path-to-python-for-mls`).
    1. **기존 Python 사용** 이 선택 되어 있는지 확인 합니다.
    1. 다시 시작 Azure Data Studio

    다른 Python IDE를 사용 하는 경우 IDE에 대해 비슷한 단계를 따릅니다.

* SQL 쿼리 도구-이 자습서에서는 [Azure Data Studio](../../azure-data-studio/what-is.md)사용 하 고 있다고 가정 합니다. SSMS ( [SQL Server Management Studio](../../ssms/sql-server-management-studio-ssms.md) )를 사용할 수도 있습니다.

* 추가 Python 패키지-이 자습서 시리즈의 예제에서는 사용자가 설치 하거나 설치할 수 없는 Python 패키지를 사용 합니다. 필요한 경우 다음 **pip** 명령을 사용 하 여 이러한 패키지를 설치 합니다.

    ```console
    pip install pandas
    pip install sklearn
    pip install pickle
    ```

## <a name="restore-the-sample-database"></a>예제 데이터베이스 복원

이 자습서에서 사용 된 샘플 데이터 집합은 다운로드 하 여 사용할 수 있도록 **.bak** 데이터베이스 백업 파일에 저장 되었습니다.

1. [TutorialDB](https://sqlchoice.blob.core.windows.net/sqlchoice/static/TutorialDB.bak)파일을 다운로드 합니다.

1. 다음 세부 정보를 사용 하 여 Azure Data Studio [백업 파일에서 데이터베이스 복원](../../azure-data-studio/tutorial-backup-restore-sql-server.md#restore-a-database-from-a-backup-file) 의 지시를 따릅니다.

   * 다운로드 한 **TutorialDB** 파일에서 가져오기
   * 대상 데이터베이스 이름 "TutorialDB"

1. **Rental_data** 테이블을 쿼리하여 데이터베이스를 복원한 후에 데이터 집합이 있는지 확인할 수 있습니다.

    ```sql
    USE TutorialDB;
    SELECT * FROM [dbo].[rental_data];
    ```

## <a name="next-steps"></a>다음 단계

이 자습서 시리즈의 1 부에서는 다음 단계를 완료 했습니다.

* 필수 구성 요소 설치
* 예제 데이터베이스를 SQL Server으로 가져오기

TutorialDB 데이터베이스에서 데이터를 준비 하려면이 자습서 시리즈의 2 부를 따르세요.

> [!div class="nextstepaction"]
> [Python 자습서: 선형 회귀 모델을 학습 하는 데이터 준비](python-ski-rental-linear-regression-prepare-data.md)