---
title: 설치 후 단계 완료 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: 0a788a2a-9b4f-4bfc-b1b5-83eeb1ea9ab2
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 558236f7034588a544aa4fb78091c19475cc8f4e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63025659"
---
# <a name="complete-the-post-installation-steps"></a>설치 후 단계 완료
  Distributed Replay를 설치한 후에는 Distributed Replay Controller 및 Client 서비스 계정을 수정해야 합니다.  
  
### <a name="to-complete-the-post-installation-steps"></a>설치 후 단계를 완료하려면  
  
1.  **방화벽 규칙을 만들**: 컨트롤러 및 클라이언트 컴퓨터에서 해당 서비스에 대 한 방화벽을 통해 인바운드 트래픽을 허용 해야 합니다. 서비스 실행 파일에 대해 방화벽 규칙을 지정합니다. 이 파일은 설치 폴더에 있습니다.  
  
    1.  컨트롤러 서비스의 경우 설치 폴더에 있는 **DReplayController.exe**에 대해 규칙을 만듭니다. 예를 들어 다음 명령은 이 규칙을 설정하며 여기서 `%InstallPath%` 는 서비스 설치 폴더입니다.  
  
         `netsh advfirewall firewall add rule name="allow dreplay controller" dir=in program="%InstallPath%\DReplayController\DReplayController.exe" action=allow`  
  
    2.  클라이언트 서비스의 경우 각 클라이언트 컴퓨터에서 설치 폴더에 있는 **DReplayClient.exe**에 대해 규칙을 만듭니다. 예를 들어 다음 명령은 이 규칙을 설정하며 여기서 `%InstallPath%` 는 서비스 설치 폴더입니다.  
  
         `netsh advfirewall firewall add rule name="allow dreplay client" dir=in program="%InstallPath%\DReplayClient\DReplayClient.exe" action=allow`  
  
2.  **각 클라이언트를 대상 서버에 대 한 권한 부여**: 클라이언트 서비스 계정을 대상 인스턴스의 sysadmin 역할에 수동으로 추가 해야 클라이언트 컴퓨터에 클라이언트 서비스를 설치를 완료 한 후 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.  
  
## <a name="net-framework-security"></a>.NET Framework 보안  
 Distributed Replay 기능을 설치하려면 관리 권한이 있어야 합니다. sysadmin 권한을 가진 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인만 테스트 서버의 sysadmin 서버 역할에 클라이언트 서비스 계정을 추가할 수 있습니다. Distributed Replay 보안 고려 사항에 대한 자세한 내용은 [Distributed Replay Security](distributed-replay-security.md)을 참조하십시오.  
  
  
