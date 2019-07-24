---
title: Azure Data Studio 노트북을 사용 하 여 SQL Server 빅 데이터 클러스터 관리
titleSuffix: Manage SQL Server big data cluster cluster with Azure Data Studio notebooks
description: Azure Data Studio에서 노트북을 사용 하 여 빅 데이터 클러스터를 관리 하 고 문제를 해결 합니다.
author: yualan
ms.author: alanyu
ms.reviewer: mikeray
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 8d87b09878539cccd40191d870bf97487579dca2
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68426403"
---
# <a name="manage-big-data-clusters-for-sql-server-with-azure-data-studio-notebooks"></a>Azure Data Studio 전자 필기장을 사용 하 여 SQL Server에 대 한 빅 데이터 클러스터 관리

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]배포 노트북을 포함 하는 Azure Data Studio에 대 한 확장을 제공 합니다. 배포 노트북에는 SQL Server에 대 한 빅 데이터 클러스터를 관리 하는 Azure Data Studio에서 사용할 수 있는 설명서 및 코드가 포함 되어 있습니다.

원래 오픈 소스 프로젝트로 구현 된 [노트북](notebooks-guidance.md) 은 [Azure Data Studio](http://docs.microsoft.com/sql/azure-data-studio/download)에 구현 되었습니다. 텍스트 셀 및 사용 가능한 커널 중 하나에서 텍스트에 markdown를 사용 하 여 코드 셀에 코드를 작성할 수 있습니다.

노트북을 사용 하 여에 대 한 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]빅 데이터 클러스터를 배포할 수 있습니다.

## <a name="prerequisites"></a>사전 요구 사항

노트북을 시작 하려면 다음 필수 구성 요소가 필요 합니다.

* 최신 버전의 [Azure Data Studio 참가자 빌드](https://github.com/microsoft/azuredatastudio#try-out-the-latest-insiders-build-from-master)
* [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]Azure Data Studio에 설치 된 확장

이 외에도 SQL Server 2019 빅 데이터 클러스터를 배포 하려면 다음이 필요 합니다.

* [azdata](deploy-install-azdata.md)
* [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-native-package-management)
* [Azure CLI](/cli/azure/install-azure-cli)
