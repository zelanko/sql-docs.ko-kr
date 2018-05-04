---
title: 컨트롤러 및 클라이언트 서비스 계정 수정 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: distributed-replay
ms.reviewer: ''
ms.suite: sql
ms.technology:
- setup-install
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 44a73ddb-18ad-415c-bfbe-126ab2e3290b
caps.latest.revision: 29
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 7eb9b2256a5441eebebd2097c7f382ac46636ee8
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MTE
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="modify-the-controller-and-client-services-accounts"></a>컨트롤러 및 클라이언트 서비스 계정 수정
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  이 항목에서는 Distributed Replay Controller 및 Distributed Replay Client 서비스 계정을 수정한 후 ACL(액세스 제어 목록)을 다시 적용하는 방법에 대해 설명합니다.  
  
### <a name="to-start-or-stop-the-distributed-replay-services-using-computer-management"></a>컴퓨터 관리를 사용하여 Distributed Replay 서비스를 시작 또는 중지하려면  
  
1.  Distributed Replay 서비스가 설치된 컴퓨터에서 명령 프롬프트에 **dcomcnfg**을(를) 입력합니다.  
  
2.  **서비스**를 두 번 클릭하고 아래로 스크롤한 다음, **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay \<서비스 이름>** 을 마우스 오른쪽 단추로 클릭하고 **시작** 또는 **중지**를 클릭합니다.  
  
### <a name="to-modify-the-distributed-replay-controller-service"></a>Distributed Replay Controller 서비스를 수정하려면  
  
1.  컨트롤러 컴퓨터에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay Controller 서비스를 중지합니다.  
  
2.  **서비스**에서 **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay Controller**를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 선택합니다.  
  
3.  **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay Controller Properties** 창의 **로그온** 탭에서 **계정 지정**을 선택하거나 **찾아보기** 를 클릭하고 새 로그온 계정을 입력한 다음 **확인**을 클릭합니다.  
  
     **중요**: Distributed Replay Controller를 구성할 때 Distributed Replay Client 서비스를 실행하는 데 사용할 사용자 계정을 하나 이상 지정할 수 있습니다. 다음은 지원되는 계정 목록입니다.  
  
    -   도메인 사용자 계정  
  
    -   사용자가 만든 로컬 사용자 계정  
  
    -   관리자  
  
    -   가상 계정 및 MSA(관리 서비스 계정)  
  
    -   Network Services, 로컬 서비스 및 시스템  
  
     그룹 계정(로컬 또는 도메인) 및 다른 기본 제공 계정(예: Everyone)은 사용할 수 없습니다.  
  
4.  Distributed Replay Controller 서비스를 시작합니다.  
  
### <a name="to-modify-the-distributed-replay-client-service"></a>Distributed Replay Client 서비스를 수정하려면  
  
1.  클라이언트 서비스를 수정하기 전에 변경할 Distributed Replay Client 서비스 계정이 설치 중 컨트롤러 컴퓨터의 CTLRUSERS 매개 변수에 지정되어 있는지 확인합니다. 변경하려는 클라이언트 서비스 계정이 설치 중 지정되지 않은 경우 다음 단계를 먼저 수행해야 합니다.  
  
    1.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay Controller 서비스를 중지합니다.  
  
    2.  Controller 서비스가 설치된 컨트롤러 컴퓨터에서 명령 프롬프트에 **dcomcnfg**을(를) 입력합니다.  
  
    3.  **구성 요소 서비스** 창에서 **콘솔 루트 -> 구성 요소 서비스 -> 컴퓨터 -> 내 컴퓨터 -> DCOM Config ->DReplayController**로 이동합니다.  
  
    4.  **DReplayController**를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
    5.  **DReplayController 속성** 창의 **보안** 탭에 있는 **시작 및 활성화 권한** 섹션에서 **편집** 을 클릭합니다.  
  
    6.  새 클라이언트 서비스 로그온 계정에 **로컬 및 원격 활성화** 권한을 부여한 다음 **확인**을 클릭합니다.  
  
    7.  **액세스 권한** 섹션에서 **편집** 을 클릭하고 새 클라이언트 서비스 로그온 계정에 **로컬 및 원격 액세스** 권한을 부여한 다음 **확인**을 클릭합니다.  
  
    8.  **확인** 을 클릭하여 **DReplayController 속성** 창을 닫습니다.  
  
    9. 컨트롤러 컴퓨터에서 변경한 클라이언트 서비스 로그온 계정을 **Distributed COM Users** 그룹에 추가합니다.  
  
    10. SQL Server Distributed Replay Controller 서비스를 시작합니다.  
  
2.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay Client 서비스를 중지합니다.  
  
3.  **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay Client 속성** 창의 **로그온** 탭에서 **계정 지정**을 선택하거나 **찾아보기** 를 클릭하고 새 로그온 계정을 입력한 다음 **확인**을 클릭합니다.  
  
4.  Distributed Replay Client 서비스를 시작합니다.  
  
  
