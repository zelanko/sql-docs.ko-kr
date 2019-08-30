---
title: Windows Installer를 사용 하 여 azdata 설치
titleSuffix: SQL Server big data clusters
description: 설치 관리자를 사용 하 여 (미리 보기)를 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] 설치 하 고 관리 하는 azdata 도구를 설치 하는 방법에 대해 알아봅니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: a8dd5d2c7d0210880a82d774185a3f2a915608ec
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2019
ms.locfileid: "70158148"
---
# <a name="install-azdata-to-manage-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd-with-windows-installer"></a>Windows Installer `azdata` 를 사용 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] 하 여 관리 하기 위해 설치

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

이 문서에서는 Windows에서 SQL Server `azdata` 2019 빅 데이터 클러스터 릴리스 후보에 대해를 설치 하는 방법을 설명 합니다. Windows 설치를 사용할 수 있기 전에 `azdata` 필수 `pip`설치를 수행 합니다.

>Linux (Ubuntu)의 경우 설치 [관리자 `azdata` 를 사용 하 여 설치](./deploy-install-azdata-linux-package.md)를 참조 하세요.

지금은 다른 운영 체제 또는 배포에 설치할 `azdata` 패키지 관리자가 없습니다. 이러한 플랫폼의 경우 [패키지 관리자 `azdata` 를 사용 하지 않고 설치](./deploy-install-azdata.md)를 참조 하세요.

## <a name="install-azdata-with-the-microsoft-windows-installer"></a>Microsoft Windows Installer `azdata` 를 사용 하 여 설치

Microsoft Windows Installer를 `azdata` 사용 하 여에 설치 하려면

1. 을 `azdata` 사용 하 여 `pip`설치 된 경우 제거 합니다. Windows Installer `azdata` 를 사용 하 여 설치 된 경우 다음 단계를 진행 합니다.
1. Windows Installer `azdata` 를 사용 하 여 설치 합니다.

### <a name="uninstall-if-previous-installation-done-with-pip"></a>이전 설치를 수행한 경우 제거`pip`

이전 버전의 **mssqlctl** 가 설치 되어 있는 경우 제거 합니다. 다음 명령은 **mssqlctl**의 CTP 3.1 버전을 제거 합니다.

   ```bash
   pip3 uninstall -r https://private-repo.microsoft.com/python/ctp3.1/mssqlctl/requirements.txt
   ```

이전 버전의 `azdata` 가 설치 되어 있는 경우 최신 버전을 설치 하기 전에 먼저 제거 하는 것이 중요 합니다.

   CTP 3.2의 경우 다음 명령을 실행 합니다.

   ```bash
   pip3 uninstall -r https://azdatacli.blob.core.windows.net/python/azdata/2019-ctp3.2/requirements.txt
   ```

제거 되 면 [Windows `azdata` 에 설치](#install-azdata-windows)합니다.

>[!NOTE]
>이전에 MSI를 사용 하 여 설치를 수행한 경우에는 MSI 설치 관리자를 사용 하기 전에 최신 버전을 제거할 필요가 없습니다.

### <a id="install-azdata-windows"></a>Windows Installer를 사용 하 여 설치

Windows Installer를 사용 하 여 Windows에서 `azdata` 설치 하거나 업데이트 합니다.

[Windows Installer를 `azdata` 다운로드](http://aka.ms/azdata-msi)합니다.

설치 관리자가 컴퓨터를 변경할 수 있는지 묻는 메시지가 표시 되 면을 `Yes`클릭 합니다.

### <a name="uninstall-azdata-with-windows-installer"></a>Windows Installer `azdata` 를 사용 하 여 제거

Windows Installer를 `azdata` 제거 하려면 적절 한 운영 체제에 대 한 지침을 따르세요.

| 플랫폼      | 지침                                           |
| ------------- |--------------------------------------------------------|
| Windows 10    | 앱 > > 설정 시작                                |
| Windows 8     | 프로그램 > 제어판 > 프로그램 제거 > 프로그램 제거 |

제거할 프로그램을 라고 **`Azdata CLI`** 합니다. 이 응용 프로그램을 선택한 다음 `Uninstall` 단추를 클릭 합니다.

## <a name="next-steps"></a>다음 단계

빅 데이터 클러스터에 대 한 자세한 내용은 [ [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]?](big-data-cluster-overview.md)을 참조 하세요.
