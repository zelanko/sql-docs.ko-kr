---
title: "1단원: 복제용 Windows 계정 만들기 | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
helpviewer_keywords:
- replication [SQL Server], tutorials
- replication [SQL Server], administering
ms.assetid: 65c3816b-47f0-448c-a4a4-ebd3e2a58820
caps.latest.revision: "17"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 9688b2bac34a38ea667557b997adfed3e7cf37d3
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="lesson-1-creating-windows-accounts-for-replication"></a>1단원: 복제용 Windows 계정 만들기
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 이 단원에서는 복제 에이전트를 실행할 Windows 계정을 만들며 다음 에이전트에 대해 로컬 서버에 별도의 Windows 계정을 만듭니다.  
  
|에이전트|위치|계정 이름|  
|---------|------------|----------------|  
|스냅숏 에이전트|게시자|\<*machine_name*>\repl_snapshot|  
|로그 판독기 에이전트|게시자|\<*machine_name*>\repl_logreader|  
|배포 에이전트|게시자 및 구독자|\<*machine_name*>\repl_distribution|  
|병합 에이전트|게시자 및 구독자|\<*machine_name*>\repl_merge|  
  
> [!NOTE]  
> 복제 자습서에서는 게시자 및 배포자가 같은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스를 공유합니다. 게시자와 구독자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 같은 인스턴스를 공유할 수 있지만 반드시 이렇게 해야 하는 것은 아닙니다. 게시자와 구독자가 같은 인스턴스를 공유하는 경우 구독자에서는 계정을 만드는 단계를 수행하지 않아도 됩니다.  
  
### <a name="to-create-local-windows-accounts-for-replication-agents-at-the-publisher"></a>게시자에서 복제 에이전트에 대한 로컬 Windows 계정을 만들려면  
  
1.  게시자에서 제어판의 **관리 도구** 에 있는 **컴퓨터 관리** 를 엽니다.  
  
2.  **시스템 도구**에서 **로컬 사용자 및 그룹**을 확장합니다.  
  
3.  **사용자** 를 마우스 오른쪽 단추로 클릭한 다음 **새 사용자**를 클릭합니다.  
  
4.  **사용자 이름** 상자에 **repl_snapshot** 을 입력하고 암호 및 다른 관련 정보를 입력한 다음 **만들기** 를 클릭하여 repl_snapshot 계정을 만듭니다.  
  
5.  이전 단계를 반복하여 repl_logreader, repl_distribution 및 repl_merge 계정을 만듭니다.  
  
6.  **닫기**를 클릭합니다.  
  
### <a name="to-create-local-windows-accounts-for-replication-agents-at-the-subscriber"></a>구독자에서 복제 에이전트에 대한 로컬 Windows 계정을 만들려면  
  
1.  구독자에서 제어판의 **관리 도구** 에 있는 **컴퓨터 관리** 를 엽니다.  
  
2.  **시스템 도구**에서 **로컬 사용자 및 그룹**을 확장합니다.  
  
3.  **사용자** 를 마우스 오른쪽 단추로 클릭한 다음 **새 사용자**를 클릭합니다.  
  
4.  **사용자 이름** 상자에 **repl_distribution** 을 입력하고 암호 및 다른 관련 정보를 입력한 다음 **만들기** 를 클릭하여 repl_distribution 계정을 만듭니다.  
  
5.  이전 단계를 반복하여 repl_merge 계정을 만듭니다.  
  
6.  **닫기**를 클릭합니다.  
  
## <a name="next-steps"></a>다음 단계  
복제 에이전트에 대한 Windows 계정을 성공적으로 만들었습니다. 다음 단원에서는 스냅숏 폴더를 구성합니다. [2단원: 스냅숏 폴더 준비](../../relational-databases/replication/lesson-2-preparing-the-snapshot-folder.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
[복제 에이전트 개요](../../relational-databases/replication/agents/replication-agents-overview.md)  
  
  
  
