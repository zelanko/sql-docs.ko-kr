---
title: Azure Data Studio 전자 필기장을 사용 하 여 SQL Server 빅 데이터 클러스터 관리
titleSuffix: Manage SQL Server Big Data Clusters with Azure Data Studio notebooks
description: Azure Data Studio에서 Notebook을 사용하여 빅 데이터 클러스터를 관리하고 문제를 해결합니다.
author: yualan
ms.author: alanyu
ms.reviewer: mikeray
ms.date: 09/09/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: e22b16cf8658e53e6bdc5db0fcd82692f3730fc7
ms.sourcegitcommit: c7a202af70fd16467a498688d59637d7d0b3d1f3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/15/2019
ms.locfileid: "72313681"
---
# <a name="manage-sql-server-big-data-clusters-with-azure-data-studio-notebooks"></a>Azure Data Studio 전자 필기장을 사용 하 여 SQL Server 빅 데이터 클러스터 관리

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]에서는 Notebook을 포함하는 Azure Data Studio에 대한 확장을 제공합니다. 노트북은 Azure Data Studio에서 SQL Server 2019 빅 데이터 클러스터를 관리 하는 데 사용할 수 있는 설명서 및 코드를 제공 합니다.

원래 오픈 소스 프로젝트로 구현 된 [노트북](notebooks-guidance.md) 은 [Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/download)에 통합 되었습니다. 사용 가능한 커널 중 하나와 텍스트 셀에 있는 텍스트의 Markdown을 사용하여 코드 셀에 코드를 작성할 수 있습니다.

Notebook을 사용하여 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]의 빅 데이터 클러스터를 배포할 수 있습니다.

노트북 외에도 Jupyter 서적 이라는 노트북 컬렉션을 볼 수 있습니다. Jupyter 책은 노트북 컬렉션을 탐색 하는 데 도움이 되는 목차를 제공 하므로, SQL Server 문제를 해결 하거나 클러스터 상태를 확인할 지 여부에 관계 없이 필요한 노트북을 쉽게 찾을 수 있습니다.

## <a name="prerequisites"></a>사전 요구 사항

노트북을 열려면 다음과 같은 필수 구성 요소가 필요 합니다.

* [Azure Data Studio insider build](https://aka.ms/azuredatastudio-rc) 의 최신 버전
* Azure Data Studio에 설치 된 @no__t 0 확장

이러한 필수 구성 요소 외에도 SQL Server 2019 빅 데이터 클러스터를 배포 하려면 다음이 필요 합니다.

* [azdata](deploy-install-azdata.md)
* [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-native-package-management)
* [Azure CLI](/cli/azure/install-azure-cli)

## <a name="access-troubleshooting-notebooks"></a>액세스 문제 해결 전자 필기장
3 가지 방법으로 문제 해결 노트북에 액세스할 수 있습니다.

### <a name="command-palette"></a>명령 팔레트
1. **보기** > **명령 팔레트**를 선택합니다.
2. @No__t-0Jupyter 책을 입력 합니다. SQL Server 2019 가이드 @ no__t-0.

Jupyter 서적 뷰 렛은 빅 데이터 클러스터 SQL Server와 관련 된 문제 해결 노트북을 포함 하는 jupyter 책이 열립니다.

### <a name="sql-master-dashboard"></a>SQL 마스터 대시보드
1. Azure Data Studio 참가자를 설치한 후 SQL Server 빅 데이터 클러스터 인스턴스에 연결 합니다.
2. 인스턴스에 연결 하 고 나 서 **연결** 아래에서 서버 이름을 마우스 오른쪽 단추로 클릭 하 고 **관리**를 선택 합니다.
3. 대시보드에서 **빅 데이터 클러스터 SQL Server**를 선택 합니다. **SQL Server 2019 가이드** 를 선택 하 여 필요한 노트북을 포함 하는 Jupyter 책을 엽니다.
    대시보드 @ no__t-1에서 ![Jupyter 노트북

1. 완료 해야 하는 작업의 전자 필기장을 선택 합니다.

### <a name="controller-dashboard"></a>컨트롤러 대시보드
1. **연결** 보기에서 **빅 데이터 클러스터 SQL Server**를 확장 합니다.
2. 컨트롤러 끝점 세부 정보를 추가 합니다.
3. 컨트롤러에 연결한 후에는 끝점을 마우스 오른쪽 단추로 클릭 하 고 **관리**를 선택 합니다.
4. 대시보드가 로드 된 후 **문제 해결** 을 선택 하 여 Jupyter 책 문제 해결 가이드를 엽니다.

## <a name="use-troubleshooting-notebooks"></a>노트북 문제 해결 사용
1. Jupyter 책 목차에서 필요한 문제 해결 가이드를 찾습니다.
1. 노트북이 최적화 되었으므로 **셀 실행**을 선택 하기만 하면 됩니다. 이 작업은 노트북이 완료 될 때까지 노트북의 각 셀을 개별적으로 실행 합니다.
1. 오류가 발견 되 면 Jupyter 책은 오류를 수정 하기 위해 실행할 수 있는 노트북을 제안 합니다. 권장 단계를 수행한 후 노트북을 다시 실행 합니다.

## <a name="next-steps"></a>다음 단계
Azure Data Studio의 Notebook에 대한 자세한 내용은 [SQL Server 2019 미리 보기에서 Notebook을 사용하는 방법](notebooks-guidance.md)을 참조하세요.
