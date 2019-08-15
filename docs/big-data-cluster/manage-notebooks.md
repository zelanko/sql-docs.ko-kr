---
title: Azure Data Studio Notebook을 사용하여 SQL Server 빅 데이터 클러스터 관리
titleSuffix: Manage SQL Server big data cluster cluster with Azure Data Studio notebooks
description: Azure Data Studio에서 Notebook을 사용하여 빅 데이터 클러스터를 관리하고 문제를 해결합니다.
author: yualan
ms.author: alanyu
ms.reviewer: mikeray
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 7adc5c3d07b47b5310d8a45d00747d6dd6de9952
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/14/2019
ms.locfileid: "69028579"
---
# <a name="manage-big-data-clusters-for-sql-server-with-azure-data-studio-notebooks"></a>Azure Data Studio Notebook으로 SQL Server의 빅 데이터 클러스터 관리

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]에서는 Notebook을 포함하는 Azure Data Studio에 대한 확장을 제공합니다. Notebook에는 SQL Server의 빅 데이터 클러스터를 관리하기 위해 Azure Data Studio에서 사용할 수 있는 설명서 및 코드가 포함되어 있습니다.

원래는 오픈 소스 프로젝트로 구현된 [Notebook](notebooks-guidance.md)이 [Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/download)로 구현되었습니다. 사용 가능한 커널 중 하나와 텍스트 셀에 있는 텍스트의 Markdown을 사용하여 코드 셀에 코드를 작성할 수 있습니다.

Notebook을 사용하여 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]의 빅 데이터 클러스터를 배포할 수 있습니다.

노트북 외에도 사용자는 Jupyter 서적 이라는 노트북 컬렉션을 볼 수 있습니다. Jupyter Book은 사용자가 SQL Server 문제를 해결하거나 클러스터 상태를 확인하기 위해 필요한 Notebook을 쉽게 찾을 수 있도록 Notebook 컬렉션을 탐색하기 위한 목차를 제공합니다.

## <a name="prerequisites"></a>사전 요구 사항

Notebook을 시작하려면 다음 필수 구성 요소가 필요합니다.

* 최신 버전의 [Azure Data Studio 참가자 빌드](https://github.com/microsoft/azuredatastudio#try-out-the-latest-insiders-build-from-master)
* Azure Data Studio에 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 확장 설치

위 항목 외에도 SQL Server 2019 빅 데이터 클러스터를 배포하려면 다음이 필요합니다.

* [azdata](deploy-install-azdata.md)
* [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-native-package-management)
* [Azure CLI](/cli/azure/install-azure-cli)

## <a name="accessing-troubleshooting-notebooks"></a>문제 해결 Notebook에 액세스

1. Azure Data Studio 참가자를 설치한 후 SQL Server 빅 데이터 클러스터 인스턴스에 연결합니다.
2. 성공적으로 연결되면 연결 뷰렛에서 서버 이름을 마우스 오른쪽 단추로 클릭하고 **관리**를 클릭합니다.
3. 대시보드에서 **SQL Server 빅 데이터 클러스터**를 클릭합니다. **SQL Server 2019 가이드**를 클릭하여 필요한 Notebook이 있는 Jupyter Book을 엽니다.
    ![단추](media/manage-notebooks/jupyter-book-button.png)

1. 폴더 선택 창에서 Jupyter Book을 저장할 위치를 선택합니다.
2. **다시 로드**를 클릭하여 Azure Data Studio을 다시 로드한 후 Jupyter Book을 확인합니다. **새 인스턴스 열기**를 클릭하여 Jupyter Book이 있는 Azure Data Studio의 새 인스턴스를 엽니다.
3. 탐색기 보기에 **Books** 섹션이 표시됩니다. 확장되지 않은 경우 클릭하여 Notebook을 봅니다.
4. 완료해야 하는 작업의 Notebook을 클릭합니다.

## <a name="next-steps"></a>다음 단계
Azure Data Studio의 Notebook에 대한 자세한 내용은 [SQL Server 2019 미리 보기에서 Notebook을 사용하는 방법](notebooks-guidance.md)을 참조하세요.
