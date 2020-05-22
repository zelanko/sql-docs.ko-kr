---
title: '자습서: R에서 예측 모델 개발'
titleSuffix: SQL machine learning
description: 4부로 구성된 이 자습서 시리즈에서는 R에서 SQL 기계 학습을 사용하여 예측 모델을 학습시키기 위한 데이터를 개발합니다.
ms.prod: sql
ms.technology: machine-learning
ms.topic: tutorial
author: cawrites
ms.author: chadam
ms.reviewer: garye, davidph
ms.date: 05/04/2020
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 237b8d5ac797b6e17a48bde2fff12de55844755e
ms.sourcegitcommit: dc965772bd4dbf8dd8372a846c67028e277ce57e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/19/2020
ms.locfileid: "83607146"
---
# <a name="tutorial-prepare-data-to-train-a-predictive-model-in-r-with-sql-machine-learning"></a>자습서: R에서 SQL 기계 학습을 사용하여 예측 모델을 학습시키기 위한 데이터 준비

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
4부로 구성된 이 자습서 시리즈에서는 [SQL Server Machine Learning Services](../sql-server-machine-learning-services.md) 또는 [빅 데이터 클러스터](../../big-data-cluster/machine-learning-services.md)에서 R 및 기계 학습 모델을 사용하여 스키 대여 수량을 예측합니다.
::: moniker-end

::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
4부로 구성된 이 자습서 시리즈에서는 [SQL Server Machine Learning Services](../sql-server-machine-learning-services.md)에서 R 및 기계 학습 모델을 사용하여 스키 대여 수량을 예측합니다.
::: moniker-end

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
4부로 구성된 이 자습서 시리즈에서는 [SQL Server R Services](../r/sql-server-r-services.md)에서 R 및 기계 학습 모델을 사용하여 스키 대여 수량을 예측합니다.
::: moniker-end

스키 대여 업체 소유자로서 향후 날짜의 대여 건수를 예측하려는 경우를 가정해 보겠습니다. 이 정보는 재고, 직원 및 시설을 준비하는 데 도움이 됩니다.

이 시리즈의 첫 번째 부분에서는 필수 구성 요소를 설정합니다. 2부 및 3부에서는 데이터를 준비하고 기계 학습 모델을 학습시키기 위해 Notebook에서 R 스크립트를 개발합니다. 그런 다음, 3부에서는 SQL Server 내부에서 T-SQL 저장 프로시저를 사용하여 R 스크립트를 실행합니다.

이 문서에서는 다음을 수행하는 방법을 알아봅니다.

> [!div class="checklist"]
> * 샘플 데이터베이스를 SQL Server에 복원 

[2부](r-predictive-model-prepare-data.md)에서는 데이터베이스의 데이터를 Python 데이터 프레임에 로드하고, R에서 데이터를 준비하는 방법을 배웁니다.

[3부](r-predictive-model-train.md)에서는 R에서 기계 학습 모델을 학습시키는 방법을 알아봅니다.

[4부](r-predictive-model-deploy.md)에서는 모델을 데이터베이스에 저장한 다음, 2부와 3부에서 개발한 R 스크립트에서 저장 프로시저를 만드는 방법을 알아봅니다. 저장 프로시저는 서버에서 실행되어 새 데이터를 기반으로 미래를 예측합니다.

## <a name="prerequisites"></a>사전 요구 사항

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
* SQL Server Machine Learning Services - Machine Learning Services을 설치하는 방법은 [Windows 설치 가이드](../install/sql-machine-learning-services-windows-install.md) 또는 [Linux 설치 가이드](../../linux/sql-server-linux-setup-machine-learning.md?toc=%2Fsql%2Fmachine-learning%2Ftoc.json)를 참조하세요. [SQL Server 빅 데이터 클러스터에서 Machine Learning Services를 사용하도록 설정](../../big-data-cluster/machine-learning-services.md)할 수도 있습니다.
::: moniker-end

::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
* SQL Server Machine Learning Services - Machine Learning Services를 설치하는 방법은 [Windows 설치 가이드](../install/sql-machine-learning-services-windows-install.md)를 참조하세요. 
::: moniker-end

* R IDE - 이 자습서에서는 [RStudio Desktop](https://www.rstudio.com/products/rstudio/download/)을 사용합니다.

* RODBC - 이 드라이버는 이 자습서에서 개발할 R 스크립트에 사용됩니다. 아직 설치하지 않았으면 R 명령 `install.packages("RODBC")`를 사용하여 설치합니다. RODBC에 대한 자세한 내용은 [CRAN - Package RODBC](https://CRAN.R-project.org/package=RODBC)를 참조하세요.

* SQL 쿼리 도구 - 이 자습서에서는 [Azure Data Studio](../../azure-data-studio/what-is.md)를 사용한다고 가정합니다. 자세한 내용은 [Azure Data Studio에서 Notebook을 사용하는 방법](../../azure-data-studio/sql-notebooks.md)을 참조하세요.

## <a name="restore-the-sample-database"></a>샘플 데이터베이스 복원

이 자습서에 사용되는 샘플 데이터베이스는 **.bak** 데이터베이스 백업 파일로 저장되었으며, 사용자가 다운로드하여 사용할 수 있습니다.

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
> [!NOTE]
> 빅 데이터 클러스터에서 Machine Learning Services를 사용하는 경우 [SQL Server 빅 데이터 클러스터 마스터 인스턴스에 데이터베이스 복원](../../big-data-cluster/data-ingestion-restore-database.md)을 참조하세요.
::: moniker-end

1. [TutorialDB.bak](https://sqlchoice.blob.core.windows.net/sqlchoice/static/TutorialDB.bak) 파일을 다운로드합니다.

1. Azure Data Studio에서 다음 세부 정보를 사용하여 [백업 파일에서 데이터베이스 복원](../../azure-data-studio/tutorial-backup-restore-sql-server.md#restore-a-database-from-a-backup-file)의 지침을 따릅니다.

   * 다운로드한 **TutorialDB.bak** 파일에서 가져옵니다.
   * 대상 데이터베이스 이름을 "TutorialDB"로 지정합니다.

1. **dbo.rental_data** 테이블을 쿼리하여 복원된 데이터베이스가 있는지 확인할 수 있습니다.

   ```sql
   USE TutorialDB;
   SELECT * FROM [dbo].[rental_data];
   ```

1. 다음 SQL 명령을 실행하여 외부 스크립트를 사용하도록 설정합니다.

    ```sql
    sp_configure 'external scripts enabled', 1;
    RECONFIGURE WITH override;
    ```

## <a name="next-steps"></a>다음 단계

이 자습서 시리즈의 1부에서 다음 단계를 완료했습니다.

* 필수 구성 요소 설치
* 샘플 데이터베이스를 SQL Server에 복원함

Machine Learning 모델을 위해 데이터를 준비하려면 이 자습서 시리즈의 2부를 진행합니다.

> [!div class="nextstepaction"]
> [R에서 예측 모델을 학습하기 위한 데이터 준비](r-predictive-model-prepare-data.md)
