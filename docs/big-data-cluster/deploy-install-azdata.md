---
title: Azdata 설치
titleSuffix: SQL Server big data clusters
description: SQL Server 2019 빅 데이터 클러스터 (미리 보기)를 설치 하 고 관리 하는 azdata 도구를 설치 하는 방법에 대해 알아봅니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 9444842081456563f411ad618f32b8dbd59f7513
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68426443"
---
# <a name="install-azdata-to-manage-sql-server-big-data-clusters"></a>Azdata를 설치 하 여 빅 데이터 클러스터 SQL Server 관리

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

이 문서에서는 Windows 또는 Linux에서 CTP 3.2 용 **azdata** 도구를 설치 하는 방법을 설명 합니다.

## <a id="prerequisites"></a> 사전 요구 사항

**azdata** 는 클러스터 관리자가 REST api를 통해 빅 데이터 클러스터를 부트스트랩 하 고 관리할 수 있도록 하는 Python으로 작성 된 명령줄 유틸리티입니다. 필요한 최소 Python 버전은 v 3.5입니다. 또한 `pip` **azdata** 도구를 다운로드 하 고 설치 하는 데를 사용 해야 합니다. 아래 지침에서는 Windows 및 Ubuntu에 대 한 예제를 제공 합니다. 다른 플랫폼에서 Python을 설치 하는 방법은 [python 설명서](https://wiki.python.org/moin/BeginnersGuide/Download)를 참조 하세요.
또한 최신 버전의 *요청* Python 패키지도 설치 하 고 업데이트 해야 합니다.
```bash
pip3 install -U requests
```

> [!IMPORTANT]
> 빅 데이터 클러스터의 최신 버전을 설치 하는 경우 **azdata** 를 업그레이드 하 고 새 릴리스를 설치 *하기 전에* 데이터를 백업 하 고 이전 클러스터를 삭제 해야 합니다. 자세한 내용은 [새 릴리스로 업그레이드](deployment-upgrade.md)를 참조 하세요.

## <a id="windows"></a>Windows azdata 설치

1. Windows 클라이언트에서에서 [https://www.python.org/downloads/](https://www.python.org/downloads/)필요한 Python 패키지를 다운로드 합니다. Python 3.5.3 이상에서 Python을 설치 하는 경우에도 pip3가 설치 됩니다. 

   > [!TIP] 
   > Python3를 설치할 때 **경로**에 Python을 추가 하려면 선택 합니다. 그렇지 않으면 나중에 pip3가 있는 위치를 찾고 **경로**에 수동으로 추가할 수 있습니다.

1. 새 Windows PowerShell 세션을 열어 Python에서 최신 경로를 가져옵니다.

1. 이전 버전의 도구가 설치 되어 있는 경우 (previosly 명명 된 **mssqlctl**) 최신 버전의 **azdata**를 설치 하기 전에 먼저 제거 하는 것이 중요 합니다.

   CTP 3.1 이하의 경우 다음 명령을 실행 합니다. 명령 `ctp3.1` 에서를 제거할 **mssqlctl** 버전으로 바꿉니다. 

   ```powershell
   pip3 uninstall -r https://private-repo.microsoft.com/python/ctp3.1/mssqlctl/requirements.txt
   ```

1. 이전 버전의 **azdata** 가 설치 되어 있는 경우 최신 버전을 설치 하기 전에 먼저 제거 하는 것이 중요 합니다.

   CTP 3.2 이상에서는 다음 명령을 실행 합니다. 명령 `ctp3.2` 에서를 제거할 **azdata** 버전으로 바꿉니다.

   ```powershell
   pip3 uninstall -r https://aka.ms/azdata
   ```

1. 다음 명령을 사용 하 여 **azdata** 를 설치 합니다.

   ```powershell
   pip3 install -r https://aka.ms/azdata
   ```

## <a id="linux"></a>Linux azdata 설치

Linux에서 Python 3.5을 설치한 다음 pip를 업그레이드 해야 합니다. 다음 예제에서는 Ubuntu에 대해 작동 하는 명령을 보여 줍니다. 다른 Linux 플랫폼의 경우 [Python 설명서](https://wiki.python.org/moin/BeginnersGuide/Download)를 참조 하세요.

1. 필요한 Python 패키지를 설치 합니다.

   ```bash
   sudo apt-get update && /
   sudo apt-get install -y python3 && /
   sudo apt-get install -y python3-pip
   ```

1. 업그레이드 pip3:

   ```bash
   sudo -H pip3 install --upgrade pip
   ```

1. 이전 버전의 도구가 설치 되어 있는 경우 (이전에는 이름이 **mssqlctl**) **azdata**의 최신 버전을 설치 하기 전에 먼저 제거 하는 것이 중요 합니다.

   CTP 3.1 이하의 경우 다음 명령을 실행 합니다. 명령 `ctp3.1` 에서를 제거할 **mssqlctl** 버전으로 바꿉니다. 

   ```powershell
   pip3 uninstall -r https://private-repo.microsoft.com/python/ctp3.1/mssqlctl/requirements.txt
   ```

1. 이전 버전의 **azdata** 가 설치 되어 있는 경우 최신 버전을 설치 하기 전에 먼저 제거 하는 것이 중요 합니다.

   CTP 3.2 이상에서는 다음 명령을 실행 합니다. 명령 `ctp3.2` 에서를 제거할 **azdata** 버전으로 바꿉니다.

   ```powershell
   pip3 uninstall -r https://aka.ms/azdata
   ```

1. 다음 명령을 사용 하 여 **azdata** 를 설치 합니다.

   ```bash
   pip3 install -r https://aka.ms/azdata --user
   ```

   > [!NOTE]
   > 스위치 `--user` 는 Python 사용자 설치 디렉터리에 azdata를 설치 합니다. 이는 일반적 `~/.local/bin` 으로 Linux에서입니다. 경로에이 디렉터리를 추가 하거나 사용자 설치 디렉터리로 이동 하 여이 디렉터리에서 `./azdata` 실행 합니다.

## <a name="next-steps"></a>다음 단계

빅 데이터 클러스터에 대 한 자세한 내용은 [SQL Server 2019 빅 데이터 클러스터 란?](big-data-cluster-overview.md)을 참조 하세요.
