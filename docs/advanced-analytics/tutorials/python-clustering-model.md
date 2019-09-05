---
title: K를 사용 하 여 고객 분류 클러스터링 이란 클러스터링
description: 이 네 부분으로 구성 된 자습서 시리즈에서는 SQL Server Machine Learning Services와 함께 Python을 사용 하는 SQL database에서 K 수단 알고리즘을 사용 하 여 고객의 클러스터링을 수행 합니다.
ms.prod: sql
ms.technology: machine-learning
ms.devlang: python
ms.date: 08/30/2019
ms.topic: tutorial
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 78a5999bc0c00a72edcc631877fdfed647024bc5
ms.sourcegitcommit: 26715b4dbef95d99abf2ab7198a00e6e2c550243
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70294368"
---
# <a name="tutorial-categorizing-customers-using-k-means-clustering-with-sql-server-machine-learning-services"></a>자습서: K를 사용 하 여 고객 분류 SQL Server Machine Learning Services

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

이 네 부분으로 구성 된 자습서 시리즈에서는 Python을 사용 하 여 [SQL Server Machine Learning Services](../what-is-sql-server-machine-learning.md) 클러스터링 모델을 개발 하 고 배포 하 여 고객 데이터를 클러스터링 합니다.

이 시리즈의 1 부에서는 자습서에 대 한 필수 구성 요소를 설정한 다음 SQL database에 샘플 데이터 집합을 복원 합니다. 이 시리즈의 뒷부분에서이 데이터를 사용 하 여 SQL Server Machine Learning Services으로 Python에서 클러스터링 모델을 학습 하 고 배포 합니다.

이 시리즈의 2 ~ 3 부에서는 데이터를 분석 하 고 준비 하 고 기계 학습 모델을 학습 하기 위해 Azure Data Studio 노트북에서 몇 가지 Python 스크립트를 개발 합니다. 그런 다음, 4 부에서는 저장 프로시저를 사용 하 여 SQL database 내에서 Python 스크립트를 실행 합니다.

*클러스터링* 은 그룹의 멤버가 특정 방식으로 유사한 그룹으로 데이터를 구성 하는 것으로 설명할 수 있습니다. 이 자습서 시리즈의 경우 소매 비즈니스를 담당 하 고 있다고 가정 합니다. **K** 를 사용 하 여 제품 구매의 데이터 집합에서 고객의 클러스터링을 수행 하 고를 반환 합니다. 고객을 클러스터링 하면 특정 그룹을 대상으로 하 여 마케팅 활동에 더 효과적으로 집중할 수 있습니다.
K-클러스터링은 유사성을 기준으로 데이터의 패턴을 찾는 *자율 학습* 알고리즘입니다.

이 문서에서는 다음 방법을 설명합니다.

> [!div class="checklist"]
> * 예제 데이터베이스를 SQL Server 인스턴스로 복원

[2 부](python-clustering-model-prepare-data.md)에서는 클러스터링을 수행 하기 위해 SQL database에서 데이터를 준비 하는 방법을 배웁니다.

[3 부](python-clustering-model-build.md)에서는 Python에서 K 의미의 클러스터링 모델을 만들고 학습 하는 방법에 대해 알아봅니다.

[4 부](python-clustering-model-deploy.md)에서는 새 데이터를 기반으로 Python에서 클러스터링을 수행할 수 있는 SQL 데이터베이스에 저장 프로시저를 만드는 방법에 대해 알아봅니다.

## <a name="prerequisites"></a>사전 요구 사항

* Python 언어 옵션을 사용 하 여 [Machine Learning Services SQL Server](../what-is-sql-server-machine-learning.md) - [Windows 설치 가이드](../install/sql-machine-learning-services-windows-install.md) 또는 [Linux 설치 가이드](https://docs.microsoft.com/sql/linux/sql-server-linux-setup-machine-learning?toc=%2fsql%2fadvanced-analytics%2ftoc.json&view=sql-server-linux-ver15)의 설치 지침을 따릅니다.

* Python IDE-이 자습서는 [Azure Data Studio](../../azure-data-studio/what-is.md)에서 Python 노트북을 사용 합니다. 자세한 내용은 [Azure Data Studio에서 노트북을 사용 하는 방법](../../azure-data-studio/sql-notebooks.md)을 참조 하세요. Jupyter 노트북 또는 [python 확장](https://marketplace.visualstudio.com/items?itemName=ms-python.python) 및 [mssql 확장](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql)을 사용 하 여 [VISUAL STUDIO CODE](https://code.visualstudio.com/docs) 같은 사용자 고유의 python IDE를 사용할 수도 있습니다.

* [revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) package- **revoscalepy** 패키지는 SQL Server Machine Learning Services에 포함 되어 있습니다. 클라이언트 컴퓨터에서 패키지를 사용 하려면 로컬로이 패키지를 설치 하는 옵션을 사용 하 여 [Python 개발을 위한 데이터 과학 클라이언트 설정](../python/setup-python-client-tools-sql.md) 을 참조 하세요.

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
  pip install matplotlib
  pip install scipy
  pip install sklearn
  ```

## <a name="restore-the-sample-database"></a>예제 데이터베이스 복원

이 자습서에서 사용 된 샘플 데이터 집합은 다운로드 하 여 사용할 수 있도록 **.bak** 데이터베이스 백업 파일에 저장 되었습니다. 이 데이터 집합은 [TPC (Transaction Processing Performance Council)](http://www.tpc.org/default.asp)에서 제공 하는 [tpcx-bb](http://www.tpc.org/tpcx-bb/default.asp) 데이터 집합에서 파생 됩니다.

1. [Tpcxbb_1gb](https://sqlchoice.blob.core.windows.net/sqlchoice/static/tpcxbb_1gb.bak)파일을 다운로드 합니다.

1. 다음 세부 정보를 사용 하 여 Azure Data Studio [백업 파일에서 데이터베이스 복원](../../azure-data-studio/tutorial-backup-restore-sql-server.md#restore-a-database-from-a-backup-file) 의 지시를 따릅니다.

   * 다운로드 한 **tpcxbb_1gb** 파일에서 가져오기
   * 대상 데이터베이스 이름 "tpcxbb_1gb"

1. **Dbo. customer** 테이블을 쿼리하여 데이터베이스를 복원한 후에 데이터 집합이 있는지 확인할 수 있습니다.

    ```sql
    USE tpcxbb_1gb;
    SELECT * FROM [dbo].[customer];
    ```

## <a name="clean-up-resources"></a>리소스 정리

이 자습서를 계속 진행 하지 않으려면 SQL Server에서 tpcxbb_1gb 데이터베이스를 삭제 하세요.

## <a name="next-steps"></a>다음 단계

이 자습서 시리즈의 1 부에서는 다음 단계를 완료 했습니다.

* 예제 데이터베이스를 SQL Server 인스턴스로 복원

Machine learning 모델에 대 한 데이터를 준비 하려면이 자습서 시리즈의 2 부를 따르세요.

> [!div class="nextstepaction"]
> [자습서: SQL Server Machine Learning Services를 사용 하 여 Python에서 클러스터링을 수행 하기 위해 데이터 준비](python-clustering-model-prepare-data.md)
