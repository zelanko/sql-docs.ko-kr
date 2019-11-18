---
title: 'Python 자습서: 사용자 분류'
description: 4부로 구성된 이 자습서 시리즈에서는 SQL Server Machine Learning Services와 함께 Python을 사용해서 SQL 데이터베이스에서 K-평균 알고리즘을 사용하여 고객들에 대한 클러스터링을 수행합니다.
ms.prod: sql
ms.technology: machine-learning
ms.devlang: python
ms.date: 08/30/2019
ms.topic: tutorial
author: garyericson
ms.author: garye
ms.reviewer: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 245a1566bfbbf19821323d0b474669eaba1d2e6e
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727077"
---
# <a name="tutorial-categorizing-customers-using-k-means-clustering-with-sql-server-machine-learning-services"></a>자습서: SQL Server Machine Learning Services와 함께 K-평균 클러스터링을 사용하여 고객 분류

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

4부로 구성된 이 자습서 시리즈에서는 고객 데이터를 클러스터링하기 위해 [SQL Server Machine Learning Services](../what-is-sql-server-machine-learning.md)에서 Python을 사용하여 K-평균 클러스터링 모델을 개발 및 배포합니다.

이 시리즈 중 1부에서는 자습서의 사전 요구 사항을 설정한 후 샘플 데이터 세트를 SQL 데이터베이스에 복원합니다. 이 시리즈의 후반부에서는 이 데이터를 사용하여 SQL Server Machine Learning Services와 함께 Python에서 클러스터링 모델을 학습시키고 배포합니다.

이 시리즈의 2부 및 3부에서는 데이터를 분석 및 준비하고 Machine Learning 모델을 학습시키기 위해 Azure Data Studio 노트북에서 일부 Python 스크립트를 개발합니다. 그런 후 4부에서는 이러한 SQL 데이터베이스 내부에서 저장 프로시저를 사용하여 Python 스크립트를 실행합니다.

*클러스터링*은 그룹 구성원이 일정 기준에 따라 유사한 특성을 갖는 그룹으로 데이터를 정리하는 것과 같습니다. 이 자습서 시리즈에서는 사용자가 판매점을 소유하고 있다고 가정합니다. **K-평균** 알고리즘을 사용하여 제품 구매 및 반품 데이터 세트에서 고객에 대한 클러스터링을 수행합니다. 고객을 클러스터링하면 특정 그룹을 대상으로 보다 효과적으로 마케팅 노력을 집중할 수 있습니다.
K-평균 클러스터링은 유사성을 기준으로 데이터의 패턴을 찾는 *자율 학습* 알고리즘입니다.

이 문서에서는 다음과 같은 방법을 알아봅니다.

> [!div class="checklist"]
> * SQL Server 인스턴스로 샘플 데이터베이스 복원

[2부](python-clustering-model-prepare-data.md)에서는 클러스터링을 수행하기 위해 SQL 데이터베이스의 데이터를 준비하는 방법을 알아봅니다.

[3부](python-clustering-model-build.md)에서는 Python에서 K-평균 클러스터링 모델을 만들고 학습시키는 방법을 알아봅니다.

[4부](python-clustering-model-deploy.md)에서는 새 데이터를 기준으로 Python에서 클러스터링을 수행할 수 있는 저장 프로시저를 SQL 데이터베이스에서 만드는 방법을 알아봅니다.

## <a name="prerequisites"></a>사전 요구 사항

* [SQL Server Machine Learning Services](../what-is-sql-server-machine-learning.md) 및 Python 언어 옵션 - [Windows 설치 가이드](../install/sql-machine-learning-services-windows-install.md) 또는 [Linux 설치 가이드](https://docs.microsoft.com/sql/linux/sql-server-linux-setup-machine-learning?toc=%2fsql%2fadvanced-analytics%2ftoc.json&view=sql-server-linux-ver15)의 설치 지침을 따릅니다.

* Python IDE - 이 자습서에서는 [Azure Data Studio](../../azure-data-studio/what-is.md)의 Python 노트북을 사용합니다. 자세한 내용은 [Azure Data Studio에서 노트북을 사용하는 방법](../../azure-data-studio/sql-notebooks.md)을 참조하세요. 또한 Jupyter 노트북이나 [Python 확장 기능](https://marketplace.visualstudio.com/items?itemName=ms-python.python) 및 [mssql 확장 기능](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql)이 포함된 [Visual Studio Code](https://code.visualstudio.com/docs)와 같은 고유한 Python IDE를 사용할 수도 있습니다.

* [revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) 패키지 - **revoscalepy** 패키지는 SQL Server Machine Learning Services에 포함되어 있습니다. 클라이언트 컴퓨터에서 패키지를 사용하려면 [Python 개발을 위한 데이터 과학 클라이언트 설정](../python/setup-python-client-tools-sql.md)에서 이 패키지를 로컬로 설치하기 위한 옵션을 참조하세요.

  Azure Data Studio에서 Python 노트북을 사용하는 경우 **revoscalepy** 사용을 위한 다음 추가 단계를 수행합니다.

  1. Azure Data Studio 열기
  1. **파일** 메뉴에서 **기본 설정**을 선택한 후 **설정**을 선택합니다.
  1. **확장**을 확장하고 **노트북 구성**을 선택합니다.
  1. **Python 경로** 아래에 라이브러리를 설치한 경로를 입력합니다(예: `C:\path-to-python-for-mls`).
  1. **기존 Python 사용**이 선택되었는지 확인합니다.
  1. Azure Data Studio 다시 시작

  다른 Python IDE를 사용하는 경우 해당 IDE에 대해 비슷한 단계를 수행합니다.

* SQL 쿼리 도구 - 이 자습서에서는 [Azure Data Studio](../../azure-data-studio/what-is.md)를 사용한다고 가정합니다. 또한 [SQL Server Management Studio](../../ssms/sql-server-management-studio-ssms.md)(SSMS)를 사용할 수도 있습니다.

* 추가 Python 패키지 - 이 자습서 시리즈의 예제에서는 사용자가 설치했거나 설치하지 않았을 수 있는 Python 패키지가 사용됩니다. 필요한 경우 다음 **pip** 명령을 사용하여 패키지를 설치하세요.

  ```console
  pip install matplotlib
  pip install scipy
  pip install sklearn
  ```

## <a name="restore-the-sample-database"></a>샘플 데이터베이스 복원

이 자습서에 사용되는 샘플 데이터 세트는 **.bak** 데이터베이스 백업 파일로 저장되었으며, 사용자가 다운로드하여 사용할 수 있습니다. 이 데이터 세트는 [Transaction Processing Performance Council(TPC)](http://www.tpc.org/default.asp)에서 제공되는 [tpcx-bb](http://www.tpc.org/tpcx-bb/default.asp) 데이터 세트에서 파생됩니다.

1. [tpcxbb_1gb.bak](https://sqlchoice.blob.core.windows.net/sqlchoice/static/tpcxbb_1gb.bak) 파일을 다운로드하세요.

1. Azure Data Studio에서 다음 세부 정보를 사용하여 [백업 파일에서 데이터베이스 복원](../../azure-data-studio/tutorial-backup-restore-sql-server.md#restore-a-database-from-a-backup-file)의 지침을 따릅니다.

   * 다운로드한 **tpcxbb_1gb.bak** 파일에서 가져옵니다.
   * 대상 데이터베이스 이름을 "tpcxbb_1gb"로 지정합니다.

1. **dbo.customer** 테이블을 쿼리하여 데이터베이스를 복원한 후 데이터 세트가 존재하는지 확인할 수 있습니다.

    ```sql
    USE tpcxbb_1gb;
    SELECT * FROM [dbo].[customer];
    ```

## <a name="clean-up-resources"></a>리소스 정리

이 자습서를 계속 진행하지 않으려면 SQL Server에서 tpcxbb_1gb 데이터베이스를 삭제하세요.

## <a name="next-steps"></a>다음 단계

이 자습서 시리즈의 1부에서 다음 단계를 완료했습니다.

* SQL Server 인스턴스로 샘플 데이터베이스 복원

Machine Learning 모델을 위해 데이터를 준비하려면 이 자습서 시리즈의 2부를 진행합니다.

> [!div class="nextstepaction"]
> [자습서: SQL Server Machine Learning Services와 함께 Python에서 클러스터링을 수행하기 위해 데이터 준비](python-clustering-model-prepare-data.md)
