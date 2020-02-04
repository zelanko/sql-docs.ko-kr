---
title: 컨트롤러 대시보드를 사용하여 SQL Server 빅 데이터 클러스터 관리
titleSuffix: Manage SQL Server big data cluster with controller dashboard
description: Azure Data Studio에서 Notebook을 사용하여 빅 데이터 클러스터를 관리하고 문제를 해결합니다.
author: yualan
ms.author: alanyu
ms.reviewer: mikeray
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: a78074b7e32df18de1308d2354d98079d074f9bf
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "73531935"
---
# <a name="manage-big-data-clusters-for-sql-server-controller-dashboard"></a>SQL Server 컨트롤러 대시보드의 빅 데이터 클러스터 관리

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

**azdata** 및 클러스터 상태 Notebook 외에도 SQL Server 빅 데이터 클러스터의 상태를 보는 또 다른 방법이 있습니다. 이제 **연결** 뷰렛을 통해 SQL Server 빅 데이터 클러스터 컨트롤러를 추가할 수 있습니다. 이렇게 하면 대시보드를 추가하여 클러스터 상태를 볼 수 있습니다.

![dashboard](media/manage-with-controller-dashboard/controller-dashboard.png)
## <a name="prerequisites"></a>사전 요구 사항

Notebook을 시작하는 데 필요한 필수 조건은 다음과 같습니다.

* 최신 버전의 [Azure Data Studio 참가자 빌드](https://docs.microsoft.com/sql/big-data-cluster/deploy-big-data-tools?view=sqlallproducts-download-and-install-azure-data-studio-sql-server-2019-release-candidate-rc)
* Azure Data Studio에 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 확장이 설치됨

이 밖에도 SQL Server 2019 빅 데이터 클러스터에는 다음이 필요합니다.

* **azdata**
    - [Windows Installer](deploy-install-azdata-installer.md)
    - [Linux 패키지 관리자](deploy-install-azdata-linux-package.md)
* [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-native-package-management)
* [Azure CLI](/cli/azure/install-azure-cli)

## <a name="add-sql-server-big-data-cluster-controller"></a>SQL Server 빅 데이터 클러스터 컨트롤러 추가

1. 왼쪽 창에서 [연결] 보기를 클릭합니다.
2. [연결] 보기 하단에서 **SQL Server 빅 데이터 클러스터**를 클릭하여 확장합니다.
3. **SQL Server 빅 데이터 클러스터 컨트롤러**를 클릭하여 새 대화 상자를 표시합니다.

## <a name="add-new-controller"></a>새 컨트롤러 추가

1. 클러스터 이름을 입력합니다.
2. 클러스터 관리 서비스 URL을 입력합니다. URL은 BDC 대시보드의 서비스 엔드포인트 테이블에서 확인하거나 클러스터 관리자에게 문의하세요.
3. 사용자 이름과 암호를 입력합니다.

## <a name="launch-controller-dashboard"></a>컨트롤러 대시보드 시작

1. 컨트롤러를 추가한 후에는 SQL Server 빅 데이터 클러스터 아래에서 볼 수 있습니다.
2. 대시보드를 시작하려면 컨트롤러를 마우스 오른쪽 단추로 클릭하고 **관리**를 클릭합니다.

## <a name="controller-dashboard"></a>컨트롤러 대시보드

1. 컨트롤러 대시보드에는 다음과 같은 세 가지 주요 구성 요소가 있습니다.

    - 상단의 **도구 모음**에는 대시보드에서 수행할 수 있는 작업이 있습니다.
    - 왼쪽의 **탐색 창**은 대시보드의 여러 보기에 따라 변경됩니다.
    - **보기**는 페이지의 대부분을 차지합니다.

2. **빅 데이터 클러스터 개요** 페이지에서는 다음을 볼 수 있습니다.

    - **클러스터 속성**: 클러스터에 관한 정보가 표시됩니다.
    - **클러스터 개요**: 모든 클러스터 구성 요소를 대략적으로 살펴보고 비정상 구성 요소를 가려낼 수 있습니다.
    - **서비스 엔드포인트**: SQL Server 빅 데이터 클러스터의 여러 서비스를 복사하거나 액세스할 수 있습니다.

3. **탐색 창**에 표시되는 서비스 목록에서 서비스를 클릭하여 클러스터 세부 정보를 추가할 수 있습니다. 이것은 **클러스터 개요**에서 서비스를 클릭하면 표시되는 것과 같은 보기입니다.

4. **클러스터 세부 정보** 아래의 각 보기는 다음과 같은 동일한 UI 구성 요소로 이루어집니다.

    - **상태 세부 정보**는 해당 구성 요소의 상태를 공유합니다.
    - **메트릭 및 로그**: Grafana와 Kibana의 추가 메트릭과 로그를 볼 수 있습니다.

1. 비정상 구성 요소를 발견했다면 도구 모음에서 **문제 해결**을 클릭하여 문제를 진단하는 데 도움이 되는 Notebook이 포함된 Jupyter Book을 시작할 수 있습니다.

## <a name="next-steps"></a>다음 단계

컨트롤러에 대한 자세한 내용은 [컨트롤러 설명서](concept-controller.md)를 참조하세요.