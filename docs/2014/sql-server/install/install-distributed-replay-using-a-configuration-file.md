---
title: 구성 파일을 사용 하 여 Distributed Replay 설치 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 3259232c-6963-4c9c-9d10-ae42aa262eef
caps.latest.revision: 14
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 4167456a5d1b59dd44451dda26f3ccb56e417a56
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37155694"
---
# <a name="install-distributed-replay-using-a-configuration-file"></a>구성 파일을 사용하여 Distributed Replay 설치
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 시 사용자 입력 및 시스템 기본값을 기반으로 구성 파일을 생성할 수 있습니다. 관리 도구를 설치하도록 지정한 경우 이 구성 파일을 사용하여 세 가지 Distributed Replay 구성 요소(관리 도구, Distributed Replay Controller 및 Distributed Replay Client)를 배포할 수 있습니다. 구성 파일을 사용하면 Distributed Replay 구성 요소를 설치, 복구 및 다시 설치할 수 있습니다.  
  
 구성 파일은 명령줄에서 설치할 경우에만 사용할 수 있습니다. 구성 파일을 사용할 때 매개 변수의 처리 순서는 다음과 같습니다.  
  
-   구성 파일이 패키지의 기본값을 덮어씁니다.  
  
-   명령줄 값이 구성 파일의 값을 덮어씁니다.  
  
 구성 파일을 사용 하는 방법에 대 한 자세한 내용은 참조 하세요. [SQL Server 2014 사용 하 여 설치 구성 파일](../../database-engine/install-windows/install-sql-server-using-a-configuration-file.md)합니다.  
  
> [!IMPORTANT]  
>  Distributed Replay를 설치한 후에는 컨트롤러 및 클라이언트 컴퓨터에서 방화벽 규칙을 만들고 각 클라이언트 컴퓨터에 대상 서버에 대한 권한을 부여해야 합니다. 자세한 내용은 [설치 후 단계 완료](../../tools/distributed-replay/complete-the-post-installation-steps.md)를 참조하세요.  
  
### <a name="to-generate-a-configuration-file"></a>구성 파일을 생성하려면  
  
1.  설치 마법사의 안내에 따르면 **설치 준비 완료** 페이지가 표시됩니다. 구성 파일의 경로는 **설치 준비 완료** 페이지의 구성 파일 경로 섹션에 지정됩니다.  
  
2.  설치를 실제로 완료하지는 않고 INI 파일을 생성하기 위해 설치를 취소합니다.  
  
### <a name="to-install-distributed-replay-using-the-configuration-file"></a>구성 파일을 사용하여 Distributed Replay를 설치하려면  
  
-   명령 프롬프트에서 설치를 실행하고 ConfigurationFile 매개 변수를 사용하여 ConfigurationFile.ini를 입력합니다.  
  
 **예제 구문**  
  
 다음 예에서는 명령 프롬프트에서 구성 파일을 지정하는 방법을 보여 줍니다.  
  
```  
Setup.exe /CTLRSVCPASSWORD="ctlrsvcpswd" /CLTSVCPASSWORD="cltsvcpswd" / ConfigurationFile=ConfigurationFile.INI\  
```  
  
> [!NOTE]  
>  구성 파일에서는 암호를 구성할 수 없으므로 명령줄에서 두 암호를 모두 지정해야 합니다.  
  
  
