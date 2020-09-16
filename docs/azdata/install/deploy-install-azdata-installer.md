---
title: Windows Installer를 사용하여 azdata 설치
titleSuffix: SQL Server big data clusters
description: 설치 프로그램을 사용하여 SQL Server 빅 데이터 클러스터를 설치 및 관리하기 위한 azdata 도구를 설치하는 방법을 알아봅니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 60d3b60f98a93cb6b724cd569fb2871adec3f1ce
ms.sourcegitcommit: 883435b4c7366f06ac03579752093737b098feab
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/28/2020
ms.locfileid: "89734084"
---
# <a name="install-azdata-to-manage-big-data-clusters-2019-with-windows-installer"></a>Windows Installer를 사용하여 `azdata`를 설치하고 [!INCLUDE[big-data-clusters-2019](../../includes/ssbigdataclusters-ss-nover.md)] 관리

[!INCLUDE[SQL Server 2019](../../includes/applies-to-version/sqlserver2019.md)]

이 문서에서는 Windows에서 SQL Server 2019 빅 데이터 클러스터용 `azdata`를 설치하는 방법을 설명합니다. Windows 설치가 지원되기 전에는 `azdata`를 설치하려면 `pip`가 필요했습니다.

>Linux(Ubuntu)는 [설치 프로그램을 사용하여 `azdata` 설치](./deploy-install-azdata-linux-package.md)를 참조하세요.

지금은 다른 운영 체제 또는 배포판에 `azdata`를 설치할 수 있는 패키지 관리자가 없습니다. 이러한 플랫폼은 [패키지 관리자 없이 `azdata` 설치](./deploy-install-azdata.md)를 참조하세요.

## <a name="install-azdata-with-the-microsoft-windows-installer"></a>Microsoft Windows Installer를 사용하여 `azdata` 설치

Microsoft Windows Installer를 사용하여 `azdata`를 설치하려면 다음을 수행합니다.

1. 기존에 `pip`를 사용하여 `azdata`를 설치했다면 제거합니다. 기존에 Windows Installer를 사용하여 `azdata`를 설치했다면 다음 단계로 넘어갑니다.
1. Windows Installer를 사용하여 `azdata`를 설치합니다.

### <a name="uninstall-if-previous-installation-done-with-pip"></a>기존에 `pip`를 사용하여 설치한 경우 제거

`azdata`의 이전 릴리스가 설치된 경우 먼저 제거한 후 최신 버전을 설치해야 합니다.

   `azdata`의 릴리스 후보 버전을 제거하려면 다음 명령을 실행합니다.

   ```bash
   pip3 uninstall -r https://azdatacli.blob.core.windows.net/python/azdata/2019-rc1/requirements.txt
   ```

제거한 다음 [Windows에 `azdata`를 설치](#install-azdata-windows)합니다.

>[!NOTE]
>이전에 MSI를 사용하여 설치한 경우, MSI 설치 프로그램을 사용하기 위해 먼저 현재 버전을 제거할 필요가 없습니다.

### <a name="install-with-windows-installer"></a><a id="install-azdata-windows"></a>Windows Installer를 사용하여 설치

Windows Installer를 사용하여 Windows에서 `azdata`를 설치 또는 업데이트합니다.

[`azdata` Windows Installer를 다운로드](https://aka.ms/azdata-msi)합니다.

설치 프로그램에서 컴퓨터에 변경을 적용해도 될지 묻는 메시지가 표시되면 `Yes`를 클릭합니다.

### <a name="uninstall-azdata-with-windows-installer"></a>Windows Installer를 사용하여 `azdata` 제거

Windows Installer를 사용하여 `azdata`를 제거하려면 아래에서 해당 운영 체제에 맞는 지침을 따릅니다.

| 플랫폼      | Instructions                                           |
| ------------- |--------------------------------------------------------|
| 윈도우 10| 시작 > 설정 > 앱                                |
| Windows 8     | 시작 > 제어판 > 프로그램 > 프로그램 제거 |

제거할 프로그램의 이름은 `Azdata CLI`입니다. 이 애플리케이션을 선택한 다음 `Uninstall` 단추를 클릭합니다.

## <a name="next-steps"></a>다음 단계

빅 데이터 클러스터에 대한 자세한 내용은 [[!INCLUDE[big-data-clusters-2019](../../includes/ssbigdataclusters-ver15.md)]란?](../../big-data-cluster/big-data-cluster-overview.md)을 참조하세요.