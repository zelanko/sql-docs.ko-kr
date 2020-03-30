---
title: Azdata 설치
titleSuffix: SQL Server big data clusters
description: 빅 데이터 클러스터를 설치하고 관리할 수 있는 azdata 도구 설치 방법을 알아봅니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 01/07/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 40338c4083241fedd113bca3a1beb839dbdd3fca
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "75721770"
---
# <a name="install-azdata"></a>`azdata` 설치

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

`azdata`는 REST API를 통해 빅 데이터 클러스터를 부트스트랩하고 관리할 수 있도록 Python으로 작성된 명령줄 유틸리티입니다. 

## <a name="find-latest-version"></a>최신 버전 찾기

최신 버전에 대한 파일 목록은 [https://aka.ms/azdata](https://aka.ms/azdata)에서 항상 사용할 수 있습니다.

설치된 버전을 찾고 업데이트해야 할지 여부를 확인하려면 `azdata --version`을 실행합니다.

## <a name="os-specific-instructions"></a>OS 관련 지침

* [Windows에 설치](deploy-install-azdata-installer.md)
* [macOS에 설치](deploy-install-azdata-macos.md)
* Linux 또는 [Linux(WSL)용 Windows 하위 시스템에 설치](/windows/wsl/about/)
   * [apt를 사용하여 Debian 또는 Ubuntu에 설치](deploy-install-azdata-linux-package.md)
   * [yum을 사용하여 RHEL 또는 CentOS에 설치](deploy-install-azdata-yum.md)
   * [Zypper를 사용하여 openSUSE 또는 SLE에 설치](deploy-install-azdata-zypper.md)
   * [스크립트에서 설치](deploy-install-azdata-pip.md)

[!INCLUDE [azdata-package-installation-remove-pip-install](../includes/azdata-package-installation-remove-pip-install.md)]

## <a name="next-steps"></a>다음 단계

빅 데이터 클러스터에 대한 자세한 내용은 [[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]란?](big-data-cluster-overview.md)을 참조하세요.
