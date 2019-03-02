---
title: mssqlctl 설치
titleSuffix: SQL Server 2019 big data clusters
description: 설치 하 고 SQL Server 2019 빅 데이터 클러스터 (미리 보기) 관리 mssqlctl 도구를 설치 하는 방법에 알아봅니다.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: c0805eabcdeefc8827a55e2469cb4d77b26347c5
ms.sourcegitcommit: 56fb7b648adae2c7b81bd969de067af1a2b54180
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/02/2019
ms.locfileid: "57227295"
---
# <a name="install-mssqlctl-to-manage-sql-server-2019-big-data-clusters"></a>SQL Server 2019 빅 데이터 클러스터를 관리 하는 mssqlctl 설치

이 문서에서는 설치 하는 방법을 설명 합니다 **mssqlctl** Windows 또는 Linux에서 도구입니다.

**mssqlctl** 하면 클러스터 관리자가 부트스트랩 REST Api를 통해 빅 데이터 클러스터를 관리 하는 Python으로 작성 된 명령줄 유틸리티입니다. 필요한 최소 Python 버전 v3.5 됩니다. 또한 있어야 `pip` 다운로드 및 설치 하는 데 사용 되는 **mssqlctl** 도구입니다. 아래 지침에 따라 Windows 및 Ubuntu에 대 한 예제를 제공합니다. 다른 플랫폼에서 Python을 설치 하는 것에 대 한 참조를 [Python 설명서](https://wiki.python.org/moin/BeginnersGuide/Download)합니다.

> [!IMPORTANT]
> 빅 데이터 클러스터의 최신 버전을 설치 하는 경우 데이터를 백업 하 고 이전 클러스터를 삭제 해야 *하기 전에* 업그레이드 **mssqlctl** 및 새 릴리스를 설치 합니다. 자세한 내용은 [새 릴리스로 업그레이드](deployment-guidance.md#upgrade)합니다.

## <a id="windows"></a> Windows mssqlctl 설치

1. Windows 클라이언트에 필요한 Python 패키지를 다운로드 [ https://www.python.org/downloads/ ](https://www.python.org/downloads/)합니다. Python3.5.3 이상에서는 Python을 설치할 때는 pip3도 설치 됩니다. 

   > [!TIP] 
   > Python을 추가 하려면 선택 하는 Python3을 설치할 때 사용자 **경로**합니다. 그렇지 않으면 나중에 pip3 위치한 찾아 수 수동으로 추가 하 여 **경로**합니다.

1. Python 사용 하 여 최신 경로 가져와서 있도록 새 Windows PowerShell 세션을 엽니다.

1. 모든 이전 버전의 경우 **mssqlctl** 설치를 반드시 제거할 **mssqlctl** 최신 버전을 설치 하기 전에 첫 번째입니다.

   ```powershell
   pip3 uninstall mssqlctl
   ```

1. 설치할 **mssqlctl** 다음 명령을 사용 하 여:

   ```powershell
   pip3 install -r  https://private-repo.microsoft.com/python/ctp-2.3/mssqlctl/requirements.txt
   ```

## <a id="linux"></a> Linux mssqlctl 설치

Linux에서 Python 3.5를 설치 하 고 그런 다음 pip를 업그레이드 해야 합니다. 다음 예제에서는 Ubuntu에 대 한 작동 하는 명령을 보여 줍니다. 다른 Linux 플랫폼에 대 한 참조를 [Python 설명서](https://wiki.python.org/moin/BeginnersGuide/Download)합니다.

1. 필요한 Python 패키지를 설치 합니다.

   ```bash
   sudo apt-get update && /
   sudo apt-get install -y python3 && /
   sudo apt-get install -y python3-pip
   ```

1. Pip3 업그레이드:

   ```bash
   sudo -H pip3 install --upgrade pip
   ```

1. 모든 이전 버전의 경우 **mssqlctl** 설치를 반드시 제거할 **mssqlctl** 최신 버전을 설치 하기 전에 첫 번째입니다.

   ```bash
   pip3 uninstall mssqlctl
   ```

1. 설치할 **mssqlctl** 다음 명령을 사용 하 여:

   ```bash
   pip3 install -r  https://private-repo.microsoft.com/python/ctp-2.3/mssqlctl/requirements.txt --user
   ```

   > [!NOTE]
   > `--user` 스위치는 mssqlctl Python 사용자 설치 디렉터리에 설치 합니다. 이 일반적으로 `~/.local/bin` linux. 이 디렉터리 경로를 추가 하거나 또는 사용자 설치 디렉터리로 이동 하 고 실행 `./mssqlctl` 거기서에서 합니다.

## <a name="next-steps"></a>다음 단계

빅 데이터 클러스터에 대 한 자세한 내용은 참조 하십시오 [SQL Server 2019 빅 데이터 클러스터 이란?](big-data-cluster-overview.md)합니다.
