---
title: Windows Installer를 사용하여 Azure Data CLI(azdata) 설치
titleSuffix: ''
description: 설치 관리자를 사용하여 Azure Data CLI(azdata) 도구를 설치하는 방법을 알아봅니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 09/30/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: c5b190c50dbbeebef94cdd15314539e5ce501160
ms.sourcegitcommit: 3bd188e652102f3703812af53ba877cce94b44a9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/15/2020
ms.locfileid: "97489643"
---
# <a name="install-azure-data-cli-azdata-with-windows-installer"></a>Windows Installer를 사용하여 [!INCLUDE [azure-data-cli-azdata](../../includes/azure-data-cli-azdata.md)] 설치

[!INCLUDE [azdata](../../includes/applies-to-version/azdata.md)]

이 문서에서는 설치 프로그램을 사용하여 Windows에 `azdata`를 설치하는 방법을 설명합니다. SQL Server 빅 데이터 클러스터 또는 Azure Arc 지원 데이터 서비스를 관리하려면 `azdata`를 사용하세요.

## <a name="steps-to-install-azdata-with-the-microsoft-windows-installer"></a>Microsoft Windows Installer를 사용하여 `azdata`를 설치하는 단계

Microsoft Windows Installer를 사용하여 `azdata`를 설치하려면 다음을 수행합니다.

1. 기존에 `pip`를 사용하여 `azdata`를 설치했다면 제거합니다. 기존에 Windows Installer를 사용하여 `azdata`를 설치했다면 다음 단계로 넘어갑니다.
1. [Windows Installer](https://aka.ms/azdata-msi)를 사용하여 `azdata`를 설치합니다.

### <a name="uninstall-azdata-with-windows-installer"></a>Windows Installer를 사용하여 `azdata` 제거

Windows Installer를 사용하여 `azdata`를 제거하려면 아래에서 해당 운영 체제에 맞는 지침을 따릅니다.

| 플랫폼      | Instructions                                           |
| ------------- |--------------------------------------------------------|
| 윈도우 10| 시작 > 설정 > 앱                                |
| Windows 8     | 시작 > 제어판 > 프로그램 > 프로그램 제거 |

제거할 프로그램의 이름은 `Azure Data CLI`입니다. 이 애플리케이션을 선택한 다음 `Uninstall` 단추를 클릭합니다.

## <a name="next-steps"></a>다음 단계

빅 데이터 클러스터에 대한 자세한 내용은 [[!INCLUDE[big-data-clusters-2019](../../includes/ssbigdataclusters-ver15.md)]란?](../../big-data-cluster/big-data-cluster-overview.md)을 참조하세요.

`azdata`를 [Azure Arc 지원 데이터 서비스](/azure/azure-arc/data/)와 함께 사용
