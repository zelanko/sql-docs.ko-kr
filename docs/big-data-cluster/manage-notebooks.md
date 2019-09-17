---
title: Azure Data Studio Notebook을 사용하여 SQL Server 빅 데이터 클러스터 관리
titleSuffix: Manage SQL Server big data cluster cluster with Azure Data Studio notebooks
description: Azure Data Studio에서 Notebook을 사용하여 빅 데이터 클러스터를 관리하고 문제를 해결합니다.
author: yualan
ms.author: alanyu
ms.reviewer: mikeray
ms.date: 09/09/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: cb2fcaf7431b5d79698af009b533ee49254777fe
ms.sourcegitcommit: dc8697bdd950babf419b4f1e93b26bb789d39f4a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70846654"
---
# <a name="manage-big-data-clusters-for-sql-server-with-azure-data-studio-notebooks"></a>Azure Data Studio Notebook으로 SQL Server의 빅 데이터 클러스터 관리

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]에서는 Notebook을 포함하는 Azure Data Studio에 대한 확장을 제공합니다. Notebook에는 SQL Server의 빅 데이터 클러스터를 관리하기 위해 Azure Data Studio에서 사용할 수 있는 설명서 및 코드가 포함되어 있습니다.

원래는 오픈 소스 프로젝트로 구현된 [Notebook](notebooks-guidance.md)이 [Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/download)로 구현되었습니다. 사용 가능한 커널 중 하나와 텍스트 셀에 있는 텍스트의 Markdown을 사용하여 코드 셀에 코드를 작성할 수 있습니다.

Notebook을 사용하여 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]의 빅 데이터 클러스터를 배포할 수 있습니다.

노트북 외에도 사용자는 Jupyter 서적 이라는 노트북 컬렉션을 볼 수 있습니다. Jupyter Book은 사용자가 SQL Server 문제를 해결하거나 클러스터 상태를 확인하기 위해 필요한 Notebook을 쉽게 찾을 수 있도록 Notebook 컬렉션을 탐색하기 위한 목차를 제공합니다.

## <a name="prerequisites"></a>사전 요구 사항

Notebook을 시작하려면 다음 필수 구성 요소가 필요합니다.

* 최신 버전의 [Azure Data Studio 참가자 빌드](https://aka.ms/azuredatastudio-rc)
* Azure Data Studio에 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 확장 설치

위 항목 외에도 SQL Server 2019 빅 데이터 클러스터를 배포하려면 다음이 필요합니다.

* [azdata](deploy-install-azdata.md)
* [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-native-package-management)
* [Azure CLI](/cli/azure/install-azure-cli)

## <a name="accessing-troubleshooting-notebooks"></a>문제 해결 Notebook에 액세스
3 가지 방법으로 문제 해결 노트북에 액세스할 수 있습니다.

### <a name="command-palette"></a>명령 팔레트
1. **보기** , **명령 팔레트** 를 차례로 클릭 합니다.
2. "Jupyter 서적: SQL Server 2019 가이드 "
3. 이렇게 하면 빅 데이터 클러스터 SQL Server와 관련 된 TSG를 포함 하는 Jupyter 책 Viewlet이 열립니다.

### <a name="sql-master-dashboard"></a>SQL 마스터 대시보드
1. Azure Data Studio 참가자를 설치한 후 SQL Server 빅 데이터 클러스터 인스턴스에 연결합니다.
2. 성공적으로 연결되면 연결 뷰렛에서 서버 이름을 마우스 오른쪽 단추로 클릭하고 **관리**를 클릭합니다.
3. 대시보드에서 **SQL Server 빅 데이터 클러스터**를 클릭합니다. **SQL Server 2019 가이드**를 클릭하여 필요한 Notebook이 있는 Jupyter Book을 엽니다.
    ![button](media/manage-notebooks/jupyter-book-button.png)

1. 이렇게 하면 TSG jupyter 책이 이미 열려 있는 jupyter 서적 뷰 렛이 열립니다.
4. 완료해야 하는 작업의 Notebook을 클릭합니다.

### <a name="controller-dashboard"></a>컨트롤러 대시보드
1. **연결** 보기에서 **빅 데이터 클러스터 SQL Server를 확장 합니다.**
2. 컨트롤러 끝점 세부 정보를 추가 합니다.
3. 컨트롤러에 성공적으로 연결한 후에 끝점을 마우스 오른쪽 단추로 클릭 하 고 관리를 클릭 **합니다.**
4. 대시보드가 로드 된 후 문제 해결을 클릭 하 여 Jupyter 책 TSG을 시작 합니다.

## <a name="how-to-use-troubleshooting-notebooks"></a>노트북 문제 해결을 사용 하는 방법
1. 필요한 TSG를 찾을 때까지 기존 Jupyter 책 목차를 살펴봅니다.
1. 모든 노트북은 사용자가 **실행 셀** 을 클릭 하기만 하면 되는 경우에 최적화 되어 있습니다. 그러면 완료 될 때까지 노트북의 각 셀이 개별적으로 실행 됩니다.
1. 오류가 발생 하면 Jupyter 책에서 오류를 수정 하기 위해 실행할 수 있는 노트북이 제안 됩니다. 단계에 따라 노트북을 다시 실행 합니다.

## <a name="next-steps"></a>다음 단계
Azure Data Studio의 Notebook에 대한 자세한 내용은 [SQL Server 2019 미리 보기에서 Notebook을 사용하는 방법](notebooks-guidance.md)을 참조하세요.
