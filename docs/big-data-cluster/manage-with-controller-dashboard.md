---
title: 컨트롤러 대시보드를 사용 하 여 SQL Server 빅 데이터 클러스터 관리
titleSuffix: Manage SQL Server big data cluster with controller dashboard
description: Azure Data Studio에서 Notebook을 사용하여 빅 데이터 클러스터를 관리하고 문제를 해결합니다.
author: yualan
ms.author: alanyu
ms.reviewer: mikeray
ms.date: 08/29/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 5fadb9b069e6f70cb780e6dc69295f63330a683a
ms.sourcegitcommit: 71fac5fee00e0eca57e555f44274dd7e08d47e1e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2019
ms.locfileid: "70160726"
---
# <a name="manage-big-data-clusters-for-sql-server-controller-dashboard"></a>SQL Server 컨트롤러 대시보드에 대 한 빅 데이터 클러스터 관리

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

**Azdata** 및 클러스터 상태 노트북 외에도 SQL Server 빅 데이터 클러스터의 상태를 볼 수 있는 다른 방법이 있습니다. 이제 **연결** viewlet을 통해 SQL Server 빅 데이터 클러스터 컨트롤러를 추가할 수 있습니다. 이렇게 하면 대시보드를 사용 하 여 클러스터 상태를 볼 수 있습니다.

![대시보드](media/manage-with-controller-dashboard/controller-dashboard.png)
## <a name="prerequisites"></a>사전 요구 사항

노트북을 시작 하려면 다음 필수 구성 요소가 필요 합니다.

* 최신 버전의 [Azure Data Studio 참가자 빌드](https://docs.microsoft.com/sql/big-data-cluster/deploy-big-data-tools?view=sqlallproducts-download-and-install-azure-data-studio-sql-server-2019-release-candidate-rc)
* Azure Data Studio에 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 확장이 설치됨

위의 외에도 SQL Server 2019 빅 데이터 클러스터에는 다음이 필요 합니다.

* **azdata**
    - [Linux 패키지 관리자](deploy-install-azdata-linux-package.md)
* [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-native-package-management)
* [Azure CLI](/cli/azure/install-azure-cli)


## <a name="add-sql-server-big-data-cluster-controller"></a>빅 데이터 클러스터 컨트롤러 SQL Server 추가

1. 왼쪽 창에서 연결 보기를 클릭 합니다.
2. 연결 보기의 맨 아래에서 **빅 데이터 클러스터 SQL Server** 를 클릭 하 여 확장 합니다.
3. **SQL Server 빅 데이터 클러스터 컨트롤러 추가**를 클릭 하면 새 대화 상자가 시작 됩니다.

## <a name="add-new-controller"></a>새 컨트롤러 추가

1. 클러스터 이름을 추가 합니다.
2. 클러스터 관리 서비스 URL을 추가 합니다. 이는 BDC 대시보드의 서비스 끝점 테이블에서 찾을 수 있으며 클러스터 관리자에 게 요청할 수 있습니다.
3. 사용자 이름 및 암호를 추가 합니다.

## <a name="launch-controller-dashboard"></a>컨트롤러 대시보드 시작

1. 컨트롤러를 성공적으로 추가 하면 SQL Server 빅 데이터 클러스터에서 볼 수 있습니다.
2. 대시보드를 시작 하려면 컨트롤러를 마우스 오른쪽 단추로 클릭 하 고 **관리**를 클릭 합니다.

## <a name="controller-dashboard"></a>컨트롤러 대시보드

1. 컨트롤러 대시보드에는 다음과 같은 세 가지 주요 구성 요소가 있습니다.

    - 대시보드의 동작을 포함 하는 위쪽의 **도구 모음** 입니다.
    - 왼쪽에 있는 **탐색 창** -대시보드의 여러 보기를 변경 합니다.
    - 페이지의 과반수를 다루는 **뷰입니다** .

2. **빅 데이터 클러스터 개요** 페이지에서 다음을 확인할 수 있습니다.

    - 클러스터 **속성** 을 통해 클러스터에 대 한 정보를 볼 수 있습니다.
    - **클러스터 개요** 를 참조 하 여 모든 클러스터 구성 요소에 대 한 개략적인 개요와 비정상 상태를 확인 합니다.
    - SQL Server 빅 데이터 클러스터 내의 서로 다른 서비스를 복사 하거나 액세스 하기 위한 **서비스 끝점** 입니다.

3. **탐색 창** 에서 서비스 목록을 확인 하 고 하나를 클릭 하 여 추가 클러스터 세부 정보를 볼 수 있습니다. 이는 **클러스터 개요** 에서 서비스를 클릭 했을 때와 동일한 뷰입니다.

4. **클러스터 세부 정보** 아래의 각 보기는 동일한 UI 구성 요소로 구성 됩니다.

    - 구성 요소의 상태 및 상태를 공유 하는 상태 **세부 정보** 입니다.
    - **메트릭 및 로그** 를 통해 Grafana 및 Kibana를 통해 추가 메트릭과 로그를 볼 수 있습니다.

1. 비정상 상태인 구성 요소를 확인 하는 경우 도구 모음에서 **문제 해결** 을 클릭 하 여 문제를 진단 하는 데 도움이 되는 노트북을 포함 하는 Jupyter 책을 시작 합니다.

## <a name="next-steps"></a>다음 단계

컨트롤러에 대 한 자세한 내용은 [컨트롤러 설명서](concept-controller.md)를 참조 하세요.