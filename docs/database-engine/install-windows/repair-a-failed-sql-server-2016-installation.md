---
title: "실패한 SQL Server 2016 설치 복구 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "setup-install"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 90c11b28-892b-44d6-978e-0eee48c75b7d
caps.latest.revision: 18
ms.author: "mikeray"
manager: "jhubbard"
---
# 실패한 SQL Server 2016 설치 복구
  복구 작업은 다음 시나리오에서 사용할 수 있습니다.  
  
-   성공적으로 설치된 후 손상된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 복구  
  
-   인스턴스 이름을 새로 업그레이드한 인스턴스에 매핑한 후 업그레이드 작업을 취소하거나 업그레이드 작업에 실패한 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 복구  
  
    -   요약 로그에 다음 메시지가 표시되면 실패한 업그레이드 인스턴스를 복구할 수 있습니다.  
  
         "[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 업그레이드하지 못했습니다. 계속하려면 실패 이유를 조사하고 문제를 해결한 다음 설치를 복구하십시오."  
  
    -   요약 로그에 다음 메시지가 표시되면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 제거한 후 다시 설치해야 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 복구할 수 없습니다.  
  
         "[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 업그레이드하지 못했습니다. 계속하려면 실패 이유를 조사하고 문제를 해결하십시오."  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스를 복구하는 경우  
  
-   없거나 손상된 파일을 모두 대체한 경우  
  
-   없거나 손상된 레지스트리 키를 모두 대체한 경우  
  
-   없거나 잘못된 구성 값을 모두 기본값으로 설정한 경우  
  
 계속하기 전에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 장애 조치(Failover) 클러스터의 경우 다음 중요 정보를 검토하십시오.  
  
-   복구는 개별 클러스터 노드에서 실행해야 합니다.  
  
-   준비 작업에 실패한 후 장애 조치(Failover) 클러스터 노드를 복구하려면 **노드 제거** 를 사용한 다음 준비 단계를 다시 수행합니다. 자세한 내용은 [SQL Server 장애 조치(failover) 클러스터에서 노드 추가 또는 제거&#40;설치 프로그램&#41;](../../sql-server/failover-clusters/install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md)를 참조하세요.  
  
### 설치 센터에서 실패한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치를 복구하려면  
  
1.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 미디어를 통해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램(setup.exe)을 실행합니다.  
  
2.  필수 구성 요소 및 시스템 확인이 끝나면 설치 프로그램에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 센터 페이지가 표시됩니다.  
  
3.  왼쪽의 탐색 영역에서 **유지 관리**를 클릭한 다음 **복구**를 클릭하여 복구 작업을 시작합니다.  
  
    > [!TIP]  
    >  시작 메뉴를 사용하여 설치 센터를 시작한 경우 지금은 설치 미디어의 위치를 제공해야 합니다.  
  
4.  시스템에 필수 구성 요소가 설치되어 있고 컴퓨터가 설치 유효성 검사 규칙을 통과하는지 확인하기 위해 설치 지원 규칙 및 파일 루틴이 실행됩니다. 계속하려면 **확인** 또는 **설치** 를 클릭합니다.  
  
5.  인스턴스 선택 페이지에서 복구할 인스턴스를 선택한 후 **다음** 을 클릭하여 계속합니다.  
  
6.  작업이 유효한지 검사하는 복구 규칙이 실행됩니다. 계속하려면 **다음**을 클릭합니다.  
  
7.  복구 준비 페이지에서 작업을 진행할 준비가 되었음을 알려 줍니다. 계속하려면 **복구**를 클릭합니다.  
  
8.  복구 진행률 페이지에 복구 작업 상태가 표시됩니다. 완료 페이지에서 작업이 완료되었음을 알려 줍니다.  
  
### 명령 프롬프트를 사용하여 실패한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치를 복구하려면  
  
1.  명령 프롬프트에서 다음 명령을 실행합니다.  
  
    ```  
    Setup.exe /q /ACTION=Repair /INSTANCENAME=instancename  
    ```  
  
## 참고 항목  
 [SQL Server 설치 로그 파일 보기 및 읽기](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)   
 [설치 방법 도움말 항목](../Topic/Installation%20How-to%20Topics.md)  
  
  