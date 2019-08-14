---
title: Azdata 설치
titleSuffix: SQL Server big data clusters
description: SQL Server 2019 빅 데이터 클러스터(미리 보기)를 설치 및 관리하기 위한 azdata 도구를 설치하는 방법을 알아봅니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 9444842081456563f411ad618f32b8dbd59f7513
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/25/2019
ms.locfileid: "68426443"
---
# <a name="install-azdata-to-manage-sql-server-big-data-clusters"></a>SQL Server 빅 데이터 클러스터를 관리하기 위한 azdata 설치

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

이 문서에서는 Windows 또는 Linux에서 CTP 3.2 **azdata** 도구를 설치하는 방법을 설명합니다.

## <a id="prerequisites"></a> 사전 요구 사항

**azdata**는 Python으로 작성된 명령줄 유틸리티로, 클러스터 관리자가 REST API를 통해 빅 데이터 클러스터를 부트스트랩하고 관리할 수 있도록 합니다. 필요한 최소 Python 버전은 v3.5입니다. **azdata** 도구를 다운로드하고 설치하는 데 사용되는 `pip`도 있어야 합니다. 아래 지침에서는 Windows 및 Ubuntu용 예제를 제공합니다. 다른 플랫폼에서 Python을 설치하는 경우 [Python 설명서](https://wiki.python.org/moin/BeginnersGuide/Download)를 참조하세요.
또한 최신 버전의 ‘요청’ Python 패키지도 설치 및 업데이트해야 합니다. 
```bash
pip3 install -U requests
```

> [!IMPORTANT]
> 최신 버전의 빅 데이터 클러스터를 설치하는 경우, 데이터를 백업하고 이전 클러스터를 삭제한 *후에* **azdata**를 업그레이드하고 새 릴리스를 설치해야 합니다. 자세한 내용은 [새 릴리스로 업그레이드](deployment-upgrade.md)를 참조하세요.

## <a id="windows"></a> Windows azdata 설치

1. Windows 클라이언트에서 [https://www.python.org/downloads/](https://www.python.org/downloads/)를 통해 필요한 Python 패키지를 다운로드합니다. python3.5.3 이상에서는 Python을 설치할 때 pip3도 설치됩니다. 

   > [!TIP] 
   > Python3을 설치하는 경우 **PATH**에 Python을 추가하도록 선택합니다. 추가하지 않는 경우, 나중에 pip3이 있는 위치를 찾아 **PATH**에 수동으로 추가할 수 있습니다.

1. 새 Windows PowerShell 세션을 열어 Python이 있는 최신 경로를 가져옵니다.

1. 도구의 이전 릴리스가 설치된 경우(이전 이름은 **mssqlctl**임) 먼저 제거한 다음, 최신 버전의 **azdata**를 설치해야 합니다.

   CTP 3.1 또는 이전 버전에서는 다음 명령을 실행합니다. 명령에서 `ctp3.1`을 제거할 **mssqlctl** 버전으로 바꿉니다. 

   ```powershell
   pip3 uninstall -r https://private-repo.microsoft.com/python/ctp3.1/mssqlctl/requirements.txt
   ```

1. **azdata**의 이전 릴리스가 설치된 경우 먼저 제거한 다음, 최신 버전을 설치해야 합니다.

   CTP 3.2 이상에서는 다음 명령을 실행합니다. 명령에서 `ctp3.2`를 제거할 **azdata** 버전으로 바꿉니다.

   ```powershell
   pip3 uninstall -r https://aka.ms/azdata
   ```

1. 다음 명령을 사용하여 **azdata**를 설치합니다.

   ```powershell
   pip3 install -r https://aka.ms/azdata
   ```

## <a id="linux"></a> Linux azdata 설치

Linux에서 Python 3.5를 설치한 다음, pip를 업그레이드해야 합니다. 다음 예제에서는 Ubuntu에서 작동하는 명령을 보여 줍니다. 다른 Linux 플랫폼의 경우 [Python 설명서](https://wiki.python.org/moin/BeginnersGuide/Download)를 참조하세요.

1. 필요한 Python 패키지를 설치합니다.

   ```bash
   sudo apt-get update && /
   sudo apt-get install -y python3 && /
   sudo apt-get install -y python3-pip
   ```

1. pip3을 업그레이드합니다.

   ```bash
   sudo -H pip3 install --upgrade pip
   ```

1. 도구의 이전 릴리스가 설치된 경우(이전 이름은 **mssqlctl**임) 먼저 제거한 다음, 최신 버전의 **azdata**를 설치해야 합니다.

   CTP 3.1 또는 이전 버전에서는 다음 명령을 실행합니다. 명령에서 `ctp3.1`을 제거할 **mssqlctl** 버전으로 바꿉니다. 

   ```powershell
   pip3 uninstall -r https://private-repo.microsoft.com/python/ctp3.1/mssqlctl/requirements.txt
   ```

1. **azdata**의 이전 릴리스가 설치된 경우 먼저 제거한 다음, 최신 버전을 설치해야 합니다.

   CTP 3.2 이상에서는 다음 명령을 실행합니다. 명령에서 `ctp3.2`를 제거할 **azdata** 버전으로 바꿉니다.

   ```powershell
   pip3 uninstall -r https://aka.ms/azdata
   ```

1. 다음 명령을 사용하여 **azdata**를 설치합니다.

   ```bash
   pip3 install -r https://aka.ms/azdata --user
   ```

   > [!NOTE]
   > `--user` 스위치를 사용하면 Python 사용자 설치 디렉터리에 azdata가 설치됩니다. Linux에서는 일반적으로 `~/.local/bin`입니다. 이 디렉터리를 경로에 추가하거나, 사용자 설치 디렉터리로 이동하여 `./azdata`를 실행합니다.

## <a name="next-steps"></a>다음 단계

빅 데이터 클러스터에 대한 자세한 내용은 [SQL Server 2019 빅 데이터 클러스터란?](big-data-cluster-overview.md)을 참조하세요.
