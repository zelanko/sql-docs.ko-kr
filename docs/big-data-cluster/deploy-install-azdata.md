---
title: Pip를 사용 하 여 azdata 설치
titleSuffix: SQL Server big data clusters
description: Pip를 사용 하 여 (미리 보기)를 설치 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] 하 고 관리 하는 azdata 도구를 설치 하는 방법에 대해 알아봅니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: a72e2ab39a17adef6c330f1ae17dcdc8a5dd8ddf
ms.sourcegitcommit: 71fac5fee00e0eca57e555f44274dd7e08d47e1e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2019
ms.locfileid: "70160730"
---
# <a name="install-azdata-for-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd-using-pip"></a>`azdata` 를[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] 사용 하 여 설치`pip`

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

이 문서에서는를 사용 하 여 `azdata` `pip`Windows 또는 Linux에서 릴리스 후보의 도구를 설치 하는 방법을 설명 합니다.

## <a id="prerequisites"></a> 사전 요구 사항

`azdata`는 클러스터 관리자가 REST Api를 통해 빅 데이터 클러스터를 부트스트랩 하 고 관리할 수 있도록 하는 Python으로 작성 된 명령줄 유틸리티입니다. 필요한 최소 Python 버전은 v3.5입니다. 또한 `pip` 를 사용 하 여 도구를 다운로드 하 고 설치 `azdata` 해야 합니다. 아래 지침에서는 Windows 및 Ubuntu용 예제를 제공합니다. 다른 플랫폼에서 Python을 설치하는 경우 [Python 설명서](https://wiki.python.org/moin/BeginnersGuide/Download)를 참조하세요.
또한 최신 버전의 ‘요청’ Python 패키지도 설치 및 업데이트해야 합니다.
```bash
pip3 install -U requests
```

> [!IMPORTANT]
> 빅 데이터 클러스터의 최신 버전을 설치 하는 경우 새 릴리스를 업그레이드 `azdata` 하 고 설치 *하기 전에* 데이터를 백업 하 고 이전 클러스터를 삭제 해야 합니다. 자세한 내용은 [새 릴리스로 업그레이드](deployment-upgrade.md)를 참조하세요.

## <a id="windows"></a>Windows `azdata` 설치

1. Windows 클라이언트에서 [https://www.python.org/downloads/](https://www.python.org/downloads/)를 통해 필요한 Python 패키지를 다운로드합니다. python3.5.3 이상에서는 Python을 설치할 때 pip3도 설치됩니다. 

   > [!TIP] 
   > Python3을 설치하는 경우 **PATH**에 Python을 추가하도록 선택합니다. 추가하지 않는 경우, 나중에 pip3이 있는 위치를 찾아 **PATH**에 수동으로 추가할 수 있습니다.

1. 새 Windows PowerShell 세션을 열어 Python이 있는 최신 경로를 가져옵니다.

1. 이전 버전의 도구가 설치 되어 있는 경우 (CTP 3.2 이전에는 도구를 **mssqlctl**라고 함) 최신 버전의 `azdata`를 설치 하기 전에 먼저 제거 하는 것이 중요 합니다. 다음 명령은 **mssqlctl**의 CTP 3.1 버전을 제거 합니다.

   ```powershell
   pip3 uninstall -r https://private-repo.microsoft.com/python/ctp3.1/mssqlctl/requirements.txt
   ```

1. 이전 버전의 `azdata` 가 설치 되어 있는 경우 최신 버전을 설치 하기 전에 먼저 제거 하는 것이 중요 합니다.

   CTP 3.2의 경우 다음 명령을 실행 합니다.

   ```powershell
   pip3 uninstall -r https://azdatacli.blob.core.windows.net/python/azdata/2019-ctp3.2/requirements.txt
   ```

1. 다음 `azdata` 명령을 사용 하 여를 설치 합니다.

   ```powershell
   pip3 install -r https://aka.ms/azdata
   ```

## <a id="linux"></a>Linux `azdata` 설치

Linux에서 Python 3.5를 설치한 다음, pip를 업그레이드해야 합니다. 다음 예제에서는 Ubuntu에서 작동하는 명령을 보여 줍니다. 다른 Linux 플랫폼의 경우 [Python 설명서](https://wiki.python.org/moin/BeginnersGuide/Download)를 참조하세요.

1. 필요한 Python 패키지를 설치합니다.

   ```bash
   sudo apt-get update && \
   sudo apt-get install -y python3 && \
   sudo apt-get install -y python3-pip
   ```

1. pip3을 업그레이드합니다.

   ```bash
   sudo -H pip3 install --upgrade pip
   ```

1. 이전 버전의 도구가 설치 되어 있는 경우 (CTP 3.2 이전에는 도구를 **mssqlctl**라고 함) 최신 버전의 `azdata`를 설치 하기 전에 먼저 제거 하는 것이 중요 합니다. 다음 명령은 **mssqlctl**의 CTP 3.1 버전을 제거 합니다.

   ```bash
   pip3 uninstall -r https://private-repo.microsoft.com/python/ctp3.1/mssqlctl/requirements.txt
   ```

1. 이전 버전의 `azdata` 가 설치 되어 있는 경우 최신 버전을 설치 하기 전에 먼저 제거 하는 것이 중요 합니다.

   CTP 3.2의 경우 다음 명령을 실행 합니다.

   ```bash
   pip3 uninstall -r https://azdatacli.blob.core.windows.net/python/azdata/2019-ctp3.2/requirements.txt
   ```

1. 다음 `azdata` 명령을 사용 하 여를 설치 합니다.

   ```bash
   pip3 install -r https://aka.ms/azdata --user
   ```

   > [!NOTE]
   > 스위치 `--user` 는 Python `azdata` 사용자 설치 디렉터리에 설치 됩니다. Linux에서는 일반적으로 `~/.local/bin`입니다. 이 디렉터리를 경로에 추가하거나, 사용자 설치 디렉터리로 이동하여 `./azdata`를 실행합니다.

## <a name="next-steps"></a>다음 단계

빅 데이터 클러스터에 대 한 자세한 내용은 [ [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]?](big-data-cluster-overview.md)을 참조 하세요.
