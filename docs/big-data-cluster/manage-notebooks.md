---
title: '관리: Azure Data Studio Notebook'
titleSuffix: SQL Server Big Data Clusters
description: Azure Data Studio에서 Notebook을 사용하여 빅 데이터 클러스터를 관리하고 문제를 해결합니다.
author: yualan
ms.author: alanyu
ms.reviewer: mikeray
ms.metadata: seo-lt-2019
ms.date: 12/13/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: d2a051e297b48ed8d813fce0e0e8ffa748a84d16
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "75252021"
---
# <a name="manage-sql-server-big-data-clusters-with-azure-data-studio-notebooks"></a>Azure Data Studio Notebooks를 사용하여 SQL Server 빅 데이터 클러스터 관리

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]에서는 Notebook을 포함하는 Azure Data Studio에 대한 확장을 제공합니다. Notebook은 Azure Data Studio에서 SQL Server 2019 빅 데이터 클러스터를 관리하는 데 사용할 수 있는 설명서와 코드를 제공합니다.

원래 오픈 소스 프로젝트로 구현된 [Notebooks](notebooks-guidance.md)는 [Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/download)에 통합되었습니다. 사용 가능한 커널 중 하나와 텍스트 셀에 있는 텍스트의 Markdown을 사용하여 코드 셀에 코드를 작성할 수 있습니다.

Notebook을 사용하여 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]의 빅 데이터 클러스터를 배포할 수 있습니다.

Notebooks 외에도 Jupyter Book이라는 Notebook 컬렉션을 볼 수 있습니다. Jupyter Book은 SQL Server 문제를 해결하거나 클러스터 상태를 확인하기 위해 필요한 Notebook을 쉽게 찾을 수 있도록 Notebooks 컬렉션을 탐색하는 데 도움이 되는 목차를 제공합니다.

## <a name="prerequisites"></a>사전 요구 사항

Notebook을 열려면 다음과 같은 필수 구성 요소가 필요합니다.

* [Azure Data Studio Insiders 빌드](https://aka.ms/azuredatastudio-rc)의 최신 버전
* Azure Data Studio에 설치된 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 확장

이러한 필수 구성 요소 외에도 SQL Server 2019 빅 데이터 클러스터를 배포하려면 다음이 필요합니다.

* [azdata](deploy-install-azdata.md)
* [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-native-package-management)
* [Azure CLI](/cli/azure/install-azure-cli)

## <a name="access-troubleshooting-notebooks"></a>문제 해결 Notebooks에 액세스
세 가지 방법으로 문제 해결 Notebooks에 액세스할 수 있습니다.

### <a name="command-palette"></a>명령 팔레트
1. **뷰** > **명령 팔레트**를 선택합니다.
2. **Jupyter Books: SQL Server 2019 가이드**를 입력합니다.

SQL Server 빅 데이터 클러스터와 관련된 문제 해결 Notebooks가 포함된 Jupyter Book에서 Jupyter Books 뷰렛이 열립니다.

### <a name="sql-master-dashboard"></a>SQL Master 대시보드
1. Azure Data Studio Insiders를 설치한 후 SQL Server 빅 데이터 클러스터 인스턴스에 연결합니다.
2. 인스턴스에 연결한 후 **CONNECTIONS**에서 서버 이름을 마우스 오른쪽 단추로 클릭하고 **관리**를 선택합니다.
3. 대시보드에서 **SQL Server 빅 데이터 클러스터**를 선택합니다. **SQL Server 2019 가이드**를 선택하여 필요한 Notebooks가 포함된 Jupyter Book을 엽니다.
    ![대시보드의 Jupyter Notebooks](media/manage-notebooks/jupyter-book-button.png)

1. 완료해야 하는 작업의 Notebook을 선택합니다.

### <a name="controller-dashboard"></a>컨트롤러 대시보드
1. **연결** 보기에서 **SQL Server 빅 데이터 클러스터**를 확장합니다.
2. 컨트롤러 엔드포인트 세부 정보를 추가합니다.
3. 컨트롤러에 연결한 후 엔드포인트를 마우스 오른쪽 단추로 클릭하고 **관리**를 선택합니다.
4. 대시보드가 로드된 후 **문제 해결**을 선택하여 Jupyter Book 문제 해결 가이드를 엽니다.

## <a name="use-troubleshooting-notebooks"></a>문제 해결 Notebooks 사용
1. Jupyter Book 목차에서 필요한 문제 해결 가이드를 찾습니다.
1. Notebook이 최적화되었으므로 **셀 실행**을 선택하기만 하면 됩니다. 이 작업은 Notebook이 완료될 때까지 Notebook의 각 셀을 개별적으로 실행합니다.
1. 오류가 발견되면 Jupyter Book은 오류를 수정하기 위해 실행할 수 있는 Notebook을 제안합니다. 권장 단계를 수행한 다음, Notebook을 다시 실행합니다.

## <a name="next-steps"></a>다음 단계
Azure Data Studio의 Notebooks에 대한 자세한 내용은 [SQL Server에서 Notebook을 사용하는 방법](notebooks-guidance.md)을 참조하세요.
