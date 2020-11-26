---
title: '클라이언트 도구 설치: 장애 조치(failover) 클러스터'
description: SQL Server 장애 조치(failover) 인스턴스에서 SQL Server Management Studio와 같은 클라이언트 도구를 설치하는 방법을 알아봅니다.
ms.custom: seo-lt-2019
ms.date: 12/13/2019
ms.reviewer: ''
ms.prod: sql
ms.technology: high-availability
ms.topic: how-to
ms.assetid: 3c82d510-9798-46be-bebb-cac9bef56936
author: cawrites
ms.author: chadam
ms.openlocfilehash: 467014114a17d6cafacdaf44f1f7a2c60042721a
ms.sourcegitcommit: 5a1ed81749800c33059dac91b0e18bd8bb3081b1
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/23/2020
ms.locfileid: "96127662"
---
# <a name="install-client-tools-on-a-sql-server-failover-cluster"></a>SQL Server 장애 조치 클러스터에 클라이언트 도구 설치
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 와 같은 클라이언트 도구는 동일한 시스템의 모든 인스턴스에서 공통으로 공유하는 기능으로, 나란히 설치할 수 있도록 지원되는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 의 이전 버전과 호환됩니다. 한 번에 하나의 클라이언트 도구 버전만 노드에 존재합니다.  
  
 설치 중에 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 클라이언트 도구가 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 클러스터의 첫 번째 노드에 설치되면 자동으로 임의 노드에 추가되어 나중에 노드 추가를 사용하여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에 추가할 수 있습니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 온라인 설명서는 노드 추가를 사용하여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 클러스터에 추가된 노드에 자동으로 추가되지 않습니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 온라인 설명서의 로컬 복사본을 두려는 노드에 수동으로 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 온라인 설명서를 설치할 수 있습니다.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 클러스터의 초기 설치 중에 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 클라이언트 도구를 설치하지 않는 경우 나중에 아래 설명된 절차에 따라 설치할 수 있습니다.  
  
## <a name="installation-procedures"></a>설치 절차  
  
#### <a name="installing-ssnoversion-client-tools-using-the-setup-user-interface"></a>설치 사용자 인터페이스를 사용하여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 클라이언트 도구 설치  
  
1.  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 설치 미디어를 넣고 루트 설치 폴더에서 Setup.exe를 두 번 클릭합니다. 네트워크 공유에서 설치하려면 공유에서 루트 폴더를 찾은 다음 Setup.exe를 두 번 클릭합니다.  
  
2.  **설치** 페이지에서 **새 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 독립 실행형 설치 또는 기존 설치에 기능 추가** 를 클릭합니다. **[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치(failover) 클러스터 새로 설치** 를 클릭하지 마세요.  
  
3.  시스템 구성 검사기가 설치를 계속하기 전에 컴퓨터의 시스템 상태를 확인합니다.  
  
4.  **설치 유형** 페이지에서 **[!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 새로 설치** 를 클릭합니다.  
  
5.  **기능 선택** 페이지에서 설치할 도구를 선택하고 설치 프로세스의 나머지 단계를 진행합니다.  
  
#### <a name="installing-ssnoversion-client-tools-at-the-command-prompt"></a>명령 프롬프트를 사용하여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 클라이언트 도구 설치  
  
1.  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 클라이언트 도구 및 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 온라인 설명서를 설치하려면 다음 명령을 실행합니다. Setup.exe/q/Action=Install /Features=Tools  
  
2.  기본 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 관리 도구만 설치하려면 다음 명령을 실행합니다. Setup.exe/q/Action=Install Features=SSMS. 그러면 [!INCLUDE[ssDEnoversion](../../../includes/ssdenoversion-md.md)], [!INCLUDE[ssExpress](../../../includes/ssexpress-md.md)], sqlcmd 유틸리티 및 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PowerShell 공급자에 대한 [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] 지원이 설치됩니다.  
  
3.  전체 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 관리 도구를 설치하려면 다음 명령을 실행합니다. Setup.exe/q/Action=Install /Features=ADV_SSMS. 기능의 매개 변수 값에 대한 자세한 내용은 [명령 프롬프트에서 SQL Server 2016 설치](../../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)를 참조하세요.  
  
### <a name="uninstalling-ssnoversion-client-tools"></a>[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 클라이언트 도구 제거  
 클라이언트 도구는 제어판의 프로그램 추가/제거에 **[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]** 로 나타나고 여기서 제거할 수 있습니다. 장애 조치(Failover) 클러스터에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스를 제거하기 위해 노드 제거를 사용하면 클라이언트 구성 요소가 동시에 제거되지 않습니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 설치 로그 파일 보기 및 읽기](../../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)  
  
