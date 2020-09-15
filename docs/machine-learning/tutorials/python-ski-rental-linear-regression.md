---
title: 'Python 자습서: 스키 대여'
titleSuffix: SQL machine learning
description: 4부로 구성된 이 자습서 시리즈에서는 SQL 기계 학습을 사용하여 스키 대여 수요를 예측하도록 Python에서 선형 회귀 모델을 빌드합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/26/2020
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions'
ms.openlocfilehash: 8436564dc7e4aff17b280c136bf45040e18e583b
ms.sourcegitcommit: 9b41725d6db9957dd7928a3620fe4db41eb51c6e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/13/2020
ms.locfileid: "88180374"
---
# <a name="python-tutorial-predict-ski-rental-with-linear-regression-with-sql-machine-learning"></a>Python 자습서: SQL 기계 학습에서 선형 회귀를 사용하여 스키 대여 수량 예측
[!INCLUDE [SQL Server 2017 SQL MI](../../includes/applies-to-version/sqlserver2017-asdbmi.md)]

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
4부로 구성된 이 자습서 시리즈에서는 [SQL Server Machine Learning Services](../sql-server-machine-learning-services.md) 또는 [빅 데이터 클러스터](../../big-data-cluster/machine-learning-services.md)에서 Python 및 선형 회귀를 사용하여 스키 대여 수량을 예측합니다. 이 자습서에서는 [Azure Data Studio의 Python Notebook](../../azure-data-studio/sql-notebooks.md)을 사용합니다.
::: moniker-end
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
네 부분으로 구성된 이 자습서 시리즈에서는 [SQL Server Machine Learning Services](../sql-server-machine-learning-services.md)에서 Python 및 선형 회귀를 사용하여 스키 대여 건수를 예측합니다. 이 자습서에서는 [Azure Data Studio의 Python Notebook](../../azure-data-studio/sql-notebooks.md)을 사용합니다.
::: moniker-end
::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"
4부로 구성된 이 자습서 시리즈에서는 [Azure SQL Managed Instance Machine Learning Services](/azure/azure-sql/managed-instance/machine-learning-services-overview)에서 Python 및 선형 회귀를 사용하여 스키 대여 건수를 예측합니다. 이 자습서에서는 [Azure Data Studio의 Python Notebook](../../azure-data-studio/sql-notebooks.md)을 사용합니다.
::: moniker-end

스키 대여 업체 소유자로서 향후 날짜의 대여 건수를 예측하려는 경우를 가정해 보겠습니다. 이 정보는 재고, 직원 및 시설을 준비하는 데 도움이 됩니다.

이 시리즈의 첫 번째 부분에서는 필수 구성 요소를 설정합니다. 2부 및 3부에서는 데이터를 준비하고 기계 학습 모델을 학습시키기 위해 Notebook에서 Python 스크립트를 개발합니다. 그런 다음 3부에서는 데이터베이스 내부에서 T-SQL 저장 프로시저를 사용하여 Python 스크립트를 실행합니다.

이 문서에서는 다음을 수행하는 방법을 알아봅니다.

> [!div class="checklist"]
> * 샘플 데이터베이스 가져오기

[2부](python-ski-rental-linear-regression-prepare-data.md)에서는 데이터베이스의 데이터를 Python 데이터 프레임에 로드하고, Python에서 데이터를 준비하는 방법을 배웁니다.

[3부](python-ski-rental-linear-regression-train-model.md)에서는 Python에서 선형 회귀 모델을 학습시키는 방법을 알아봅니다.

[4부](python-ski-rental-linear-regression-deploy-model.md)에서는 모델을 데이터베이스에 저장한 다음, 2부와 3부에서 개발한 Python 스크립트에서 저장 프로시저를 만드는 방법을 알아봅니다. 저장 프로시저는 서버에서 실행되어 새 데이터를 기반으로 미래를 예측합니다.

## <a name="prerequisites"></a>사전 요구 사항

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
* SQL Server Machine Learning Services - Machine Learning Services을 설치하는 방법은 [Windows 설치 가이드](../install/sql-machine-learning-services-windows-install.md) 또는 [Linux 설치 가이드](../../linux/sql-server-linux-setup-machine-learning.md?toc=%2Fsql%2Fmachine-learning%2Ftoc.json)를 참조하세요. [SQL Server 빅 데이터 클러스터에서 Machine Learning Services를 사용하도록 설정](../../big-data-cluster/machine-learning-services.md)할 수도 있습니다.
::: moniker-end
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
* SQL Server Machine Learning Services - Machine Learning Services를 설치하는 방법은 [Windows 설치 가이드](../install/sql-machine-learning-services-windows-install.md)를 참조하세요. 
::: moniker-end
::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"
* Azure SQL Managed Instance Machine Learning Services. 등록 방법은 [Azure SQL Managed Instance Machine Learning Services 개요](/azure/azure-sql/managed-instance/machine-learning-services-overview)를 참조하세요.

* 샘플 데이터베이스를 Azure SQL Managed Instance로 복원하기 위한 [SQL Server Management Studio](../../ssms/download-sql-server-management-studio-ssms.md).
::: moniker-end

* Python IDE - 이 자습서에서는 [Azure Data Studio](../../azure-data-studio/what-is.md)의 Python Notebook을 사용합니다. 자세한 내용은 [Azure Data Studio에서 Notebook을 사용하는 방법](../../azure-data-studio/sql-notebooks.md)을 참조하세요.

* SQL 쿼리 도구 - 이 자습서에서는 [Azure Data Studio](../../azure-data-studio/what-is.md)를 사용한다고 가정합니다.

* 추가 Python 패키지 - 이 자습서 시리즈의 예제에서는 기본적으로 설치되지 않았을 수 있는 Python 패키지가 사용됩니다.

  * pandas
  * pyodbc
  * sklearn

  이러한 패키지를 설치하려면
  1. Azure Data Studio Notebook에서 **패키지 관리**를 선택합니다.
  2. **패키지 관리** 창에서 **새로 추가** 탭을 선택합니다.
  3. 다음 패키지 각각에 대해 패키지 이름을 입력하고 **검색**을 클릭한 다음 **설치**를 클릭합니다.

  또는 **명령 프롬프트**를 열고 Azure Data Studio에서 사용하는 Python 버전의 설치 경로(예: `cd %LocalAppData%\Programs\Python\Python37-32`)로 변경한 다음 각 패키지에 대해 `pip install`을 실행할 수 있습니다.

## <a name="restore-the-sample-database"></a>샘플 데이터베이스 복원

이 자습서에 사용되는 샘플 데이터베이스는 **.bak** 데이터베이스 백업 파일로 저장되었으며, 사용자가 다운로드하여 사용할 수 있습니다.

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
> [!NOTE]
> 빅 데이터 클러스터에서 Machine Learning Services를 사용하는 경우 [SQL Server 빅 데이터 클러스터 마스터 인스턴스에 데이터베이스 복원](../../big-data-cluster/data-ingestion-restore-database.md)을 참조하세요.
::: moniker-end

::: moniker range=">=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions"
1. [TutorialDB.bak](https://sqlchoice.blob.core.windows.net/sqlchoice/static/TutorialDB.bak) 파일을 다운로드합니다.

1. Azure Data Studio에서 다음 세부 정보를 사용하여 [백업 파일에서 데이터베이스 복원](../../azure-data-studio/tutorial-backup-restore-sql-server.md#restore-a-database-from-a-backup-file)의 지침을 따릅니다.

   * 다운로드한 **TutorialDB.bak** 파일에서 가져옵니다.
   * 대상 데이터베이스 이름을 "TutorialDB"로 지정합니다.

1. **dbo.rental_data** 테이블을 쿼리하여 복원된 데이터베이스가 있는지 확인할 수 있습니다.

   ```sql
   USE TutorialDB;
   SELECT * FROM [dbo].[rental_data];
   ```
::: moniker-end
::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"
1. [TutorialDB.bak](https://sqlchoice.blob.core.windows.net/sqlchoice/static/TutorialDB.bak) 파일을 다운로드합니다.

1. 다음 세부 정보를 사용하여 SQL Server Management Studio에서 [데이터베이스를 관리되는 인스턴스로 복원](/azure/sql-database/sql-database-managed-instance-get-started-restore)의 지침을 따릅니다.

   * 다운로드한 **TutorialDB.bak** 파일에서 가져옵니다.
   * 대상 데이터베이스 이름을 "TutorialDB"로 지정합니다.

1. **dbo.rental_data** 테이블을 쿼리하여 복원된 데이터베이스가 있는지 확인할 수 있습니다.

   ```sql
   USE TutorialDB;
   SELECT * FROM [dbo].[rental_data];
   ```
::: moniker-end

## <a name="clean-up-resources"></a>리소스 정리

이 자습서를 계속 진행할 생각이 없으면 TutorialDB 데이터베이스를 삭제하세요.

## <a name="next-steps"></a>다음 단계

이 자습서 시리즈의 1부에서 다음 단계를 완료했습니다.

* 필수 구성 요소 설치
* 샘플 데이터베이스 가져오기

TutorialDB 데이터베이스의 데이터를 준비하려면 이 자습서 시리즈의 2부를 진행합니다.

> [!div class="nextstepaction"]
> [Python 자습서: 선형 회귀 모델을 학습시키는 데 사용할 데이터 준비](python-ski-rental-linear-regression-prepare-data.md)