---
title: 설치 후 단계 완료
titleSuffix: SQL Server Distributed Replay
description: Distributed Replay를 설치한 후에는 Distributed Replay Controller 및 Client 서비스 계정을 수정해야 합니다.
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
ms.assetid: 0a788a2a-9b4f-4bfc-b1b5-83eeb1ea9ab2
author: markingmyname
ms.author: maghan
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.openlocfilehash: bda2bda26d8933c580597b01fba79d1912cb5b56
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85681852"
---
# <a name="complete-the-post-installation-steps"></a>설치 후 단계 완료

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

Distributed Replay를 설치한 후에는 Distributed Replay Controller 및 Client 서비스 계정을 수정해야 합니다.  
  
## <a name="to-complete-the-post-installation-steps"></a>설치 후 단계를 완료하려면  
  
1. **방화벽 규칙 만들기**: 컨트롤러 및 클라이언트 컴퓨터에서 해당 서비스에 대해 방화벽을 통과하는 인바운드 트래픽을 허용해야 합니다. 서비스 실행 파일에 대해 방화벽 규칙을 지정합니다. 이 파일은 설치 폴더에 있습니다.  
  
    1. 컨트롤러 서비스의 경우 설치 폴더에 있는 **DReplayController.exe**에 대해 규칙을 만듭니다. 예를 들어 다음 명령은 이 규칙을 설정하며 여기서 `%InstallPath%` 는 서비스 설치 폴더입니다.  
  
         `netsh advfirewall firewall add rule name="allow dreplay controller" dir=in program="%InstallPath%\DReplayController\DReplayController.exe" action=allow`  
  
    2. 클라이언트 서비스의 경우 각 클라이언트 컴퓨터에서 설치 폴더에 있는 **DReplayClient.exe**에 대해 규칙을 만듭니다. 예를 들어 다음 명령은 이 규칙을 설정하며 여기서 `%InstallPath%` 는 서비스 설치 폴더입니다.  
  
         `netsh advfirewall firewall add rule name="allow dreplay client" dir=in program="%InstallPath%\DReplayClient\DReplayClient.exe" action=allow`  
  
2. **대상 서버에서 각 클라이언트 권한 부여**: 클라이언트 컴퓨터에 클라이언트 서비스를 설치하는 작업을 완료하면 대상 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 sysadmin 역할에 클라이언트 서비스 계정을 수동으로 추가해야 합니다.  
  
## <a name="net-framework-security"></a>.NET Framework 보안

Distributed Replay 기능을 설치하려면 관리 권한이 있어야 합니다. sysadmin 권한을 가진 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인만 테스트 서버의 sysadmin 서버 역할에 클라이언트 서비스 계정을 추가할 수 있습니다. Distributed Replay 보안 고려 사항에 대한 자세한 내용은 [Distributed Replay Security](../../tools/distributed-replay/distributed-replay-security.md)을 참조하십시오.