---
title: Azure Data Studio 전자 필기장을 사용 하 여 SQL Server 빅 데이터 클러스터 배포
titleSuffix: Deploy SQL Server big data cluster cluster with Azure Data Studio notebooks
description: Azure Data Studio에서 노트북을 사용 하 여 빅 데이터 클러스터를 배포 합니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: f12a4f06ceb1c3a48b2b2fc661c59594e6d6cce3
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68426423"
---
# <a name="deploy-sql-server-big-data-cluster-with-azure-data-studio-notebooks"></a>Azure Data Studio 전자 필기장을 사용 하 여 SQL Server 빅 데이터 클러스터 배포

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]배포 노트북을 포함 하는 Azure Data Studio에 대 한 확장을 제공 합니다. 배포 노트북에는 Azure Data Studio SQL Server 빅 데이터 클러스터를 만드는 데 사용할 수 있는 설명서 및 코드가 포함 되어 있습니다. 

원래 오픈 소스 프로젝트로 구현 된 [노트북](notebooks-guidance.md) 은 [Azure Data Studio](http://docs.microsoft.com/sql/azure-data-studio/download)에 구현 되었습니다. 텍스트 셀 및 사용 가능한 커널 중 하나에서 텍스트에 markdown를 사용 하 여 코드 셀에 코드를 작성할 수 있습니다.

노트북을 사용 하 여에 대 한 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]빅 데이터 클러스터를 배포할 수 있습니다.

## <a name="prerequisites"></a>사전 요구 사항
노트북을 시작 하려면 다음 필수 구성 요소가 필요 합니다.

* 최신 버전의 [Azure Data Studio](http://docs.microsoft.com/sql/azure-data-studio/download) 설치 됨
* [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]Azure Data Studio에 설치 된 확장

이 외에도 SQL Server 2019 빅 데이터 클러스터를 배포 하려면 다음이 필요 합니다.

* [azdata](deploy-install-azdata.md)
* [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-native-package-management)
* [Azure CLI](/cli/azure/install-azure-cli)

## <a name="launch-the-notebook"></a>노트북을 시작 합니다.

1. [Azure Data Studio 참가자 빌드](https://github.com/microsoft/azuredatastudio#try-out-the-latest-insiders-build-from-master)를 설치 하 고 시작 합니다.
1.  **연결** 탭에서 **...** 을 클릭 하 고 **빅 데이터 클러스터 SQL Server 배포**...를 선택 합니다.

   ![AI 및 ML](media/deploy-notebooks/deploy-notebooks-1.png)

1. **배포 대상**의 **옵션**에서 **새 Azure Kubernetes Cluster** 또는 **기존 azure Kubernetes Service 클러스터**중 하나를 선택 합니다.
1. **노트북 열기**를 선택 합니다.

이 작업은 적절 한 노트북을 시작 합니다. 배포를 완료 하려면 기존 또는 새 Azure Kubernetes 서비스 클러스터에 대 한 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 빅 데이터 클러스터를 배포 하기 위한 노트북의 지침을 따르세요.
