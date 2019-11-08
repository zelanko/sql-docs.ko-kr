---
title: pip를 사용하여 azdata 설치
titleSuffix: SQL Server big data clusters
description: pip를 사용하여 빅 데이터 클러스터를 설치하고 관리할 수 있는 azdata 도구 설치 방법을 알아봅니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: aaccbae2b4acb745e2cb9ea531f382e0903b528f
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/04/2019
ms.locfileid: "73532059"
---
# <a name="install-azdata-for-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd-using-pip"></a>`pip`를 사용하여 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]용 `azdata` 설치

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

이 문서에서는 `pip`를 사용하여 `azdata` 도구 Windows 또는 Linux를 설치하는 방법을 설명합니다.

Windows 및 Linux(Ubuntu 배포판)의 경우 [패키지 관리자](./deploy-install-azdata-installer.md)를 사용하여 간단한 환경을 설치할 수 있습니다.

## <a id="prerequisites"></a> 사전 요구 사항

`azdata`는 Python으로 작성된 명령줄 유틸리티로, 클러스터 관리자가 REST API를 통해 빅 데이터 클러스터를 부트스트랩하고 관리할 수 있게 해줍니다. 필요한 최소 Python 버전은 v3.5입니다. `pip`는 `azdata` 도구를 다운로드하고 설치하는 데 필요합니다. 아래 지침에서는 Windows 및 Ubuntu용 예제를 제공합니다. 다른 플랫폼에서 Python을 설치하는 경우 [Python 설명서](https://wiki.python.org/moin/BeginnersGuide/Download)를 참조하세요.
그리고 최신 버전의 `requests` Python 패키지를 설치하고 업데이트합니다.

```bash
pip3 install -U requests
```

> [!IMPORTANT]
> 최신 버전의 빅 데이터 클러스터를 설치하는 경우 데이터를 백업하고 이전 클러스터를 삭제한 후 `azdata`를 업그레이드하고 새 릴리스를 설치합니다. 자세한 내용은 [새 릴리스로 업그레이드](deployment-upgrade.md)를 참조하세요.

## <a id="windows"></a> Windows `azdata` 설치

1. Windows 클라이언트에서 [https://www.python.org/downloads/](https://www.python.org/downloads/)를 통해 필요한 Python 패키지를 다운로드합니다. python3.5.3 이상에서는 Python을 설치할 때 pip3도 설치됩니다. 

   > [!TIP] 
   > Python3를 설치하는 경우 `PATH`에 Python을 추가하도록 선택합니다. 추가하지 않는 경우 나중에 pip3가 있는 위치를 찾아 `PATH`에 수동으로 추가할 수 있습니다.

1. 새 Windows PowerShell 세션을 열어 Python이 있는 최신 경로를 가져옵니다.

1. `azdata`의 이전 릴리스가 설치된 경우 먼저 제거한 후 최신 버전을 설치해야 합니다.

   CTP 3.2 또는 RC1의 경우 다음 명령을 실행합니다.

   ```bash
   pip3 uninstall -r https://azdatacli.blob.core.windows.net/python/azdata/2019-ctp3.2/requirements.txt
   ```
   로 구분하거나 여러
   ```bash
   pip3 uninstall -r https://azdatacli.blob.core.windows.net/python/azdata/2019-rc1/requirements.txt
   ```

1. 다음 명령을 사용하여 `azdata`를 설치합니다.

   ```powershell
   pip3 install -r https://aka.ms/azdata
   ```

## <a id="linux"></a> Linux `azdata` 설치

Linux에서 Python 3.5를 설치한 다음, pip를 업그레이드해야 합니다. 다음 예제에서는 Ubuntu에서 작동하는 명령을 보여 줍니다. 다른 Linux 플랫폼의 경우 [Python 설명서](https://wiki.python.org/moin/BeginnersGuide/Download)를 참조하세요.

1. 필요한 Python 패키지를 설치합니다.

   ```bash
   sudo apt-get update && \
   sudo apt-get install -y python3 && \
   sudo apt-get install -y python3-pip && \
   sudo apt-get install -y libkrb5-dev && \
   sudo apt-get install -y libsqlite3-dev && \
   sudo apt-get install -y unixodbc-dev
   ```

1. pip3을 업그레이드합니다.

   ```bash
   sudo -H pip3 install --upgrade pip
   ```

1. `azdata`의 이전 릴리스가 설치된 경우 먼저 제거한 후 최신 버전을 설치해야 합니다.

   CTP 3.2 또는 RC1의 경우 다음 명령을 실행합니다.

   ```bash
   pip3 uninstall -r https://azdatacli.blob.core.windows.net/python/azdata/2019-ctp3.2/requirements.txt
   ```
   로 구분하거나 여러
   ```bash
   pip3 uninstall -r https://azdatacli.blob.core.windows.net/python/azdata/2019-rc1/requirements.txt
   ```

1. 다음 명령을 사용하여 `azdata`를 설치합니다.

   ```bash
   pip3 install -r https://aka.ms/azdata --user
   ```

   > [!NOTE]
   > `--user` 스위치는 Python 사용자 설치 디렉터리에 `azdata`를 설치합니다. Linux에서는 일반적으로 `~/.local/bin`입니다. 이 디렉터리를 경로에 추가하거나, 사용자 설치 디렉터리로 이동하여 `./azdata`를 실행합니다.

## <a id="macOSX"></a> macOS 또는 OS X에 `azdata` 설치

macOS 또는 OS X에 `azdata`를 설치하려면 다음 단계를 완료합니다. 각 단계의 예제를 터미널에서 실행합니다.

1. 아직 [Homebrew](https://brew.sh)가 없으면 macOS 클라이언트에서 Homebrew를 설치합니다.

   ```
   /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
   ```

1. Python 및 pip 버전 3.0 이상을 설치합니다.

   ```
   brew install python3
   ```

1. 종속성을 설치합니다.

   ```
   pip3 install -U requests
   brew install freetds
   ```

1. 도구의 이전 릴리스가 설치된 경우 먼저 제거한 후 `azdata` 최신 버전을 설치해야 합니다. 다음 명령은 `azdata` 버전을 제거합니다.

   ```
   pip3 uninstall -r https://azdatacli.blob.core.windows.net/python/azdata/2019-rc1/requirements.txt
   ```

1. 다음 명령을 사용하여 `azdata`를 설치합니다.

   ```
   pip3 install -r https://aka.ms/azdata
   ```

## <a name="next-steps"></a>다음 단계

빅 데이터 클러스터에 대한 자세한 내용은 [[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]란?](big-data-cluster-overview.md)을 참조하세요.
