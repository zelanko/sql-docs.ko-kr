---
title: 비즈니스 논리 처리기 디버깅(복제 프로그래밍) | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- merge replication business logic handlers [SQL Server replication]
- business logic handlers [SQL Server replication]
- BusinessLogicModule class
ms.assetid: edd0d17a-0e9c-4c28-8395-a7d47e8ce3d6
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 01a1e4be7476b2f683345e8bfd23f4fcf0e90642
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68063079"
---
# <a name="debug-a-business-logic-handler-replication-programming"></a>비즈니스 논리 처리기 디버깅(복제 프로그래밍)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  비즈니스 논리 처리기를 사용하여 병합 구독이 동기화될 때 사용자 지정 비즈니스 논리를 호출할 수 있습니다. 자세한 내용은 [병합 동기화 중 비즈니스 논리 실행](../../relational-databases/replication/merge/execute-business-logic-during-merge-synchronization.md)을 참조하세요.  
  
 병합 복제 조정자(replrec.dll)는 비즈니스 논리가 포함된 관리 코드 어셈블리를 호출합니다. 대부분의 경우 replrec.dll과 사용자 지정 비즈니스 논리는 병합 에이전트가 실행되는 컴퓨터(끌어오기 구독의 경우 구독자, 밀어넣기 구독의 경우 배포자)에서 실행됩니다. 웹 동기화 또는 [!INCLUDE[ssEW](../../includes/ssew-md.md)] 구독자의 경우 조정자와 사용자 지정 비즈니스 논리는 웹 서버에서 실행됩니다.  
  
### <a name="to-debug-a-business-logic-handler-on-a-local-computer"></a>로컬 컴퓨터의 비즈니스 논리 처리기를 디버깅하려면  
  
1.  게시 및 배포를 구성하고 게시를 만들고 게시에 대한 구독을 만듭니다. 자세한 내용은 [게시 및 배포 구성](../../relational-databases/replication/configure-publishing-and-distribution.md) 및 [게시 만들기](../../relational-databases/replication/publish/create-a-publication.md)를 참조하세요.  
  
2.  비즈니스 논리 처리기를 만들고 등록합니다. 자세한 내용은 [병합 아티클에 대한 비즈니스 논리 처리기 구현](../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md)을 참조하세요.  
  
3.  [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Studio에서 프로그래밍 방식으로 병합 에이전트를 동기적으로 시작하는 RMO(복제 관리 개체) 프로젝트를 만듭니다. 자세한 내용은 [끌어오기 구독 동기화](../../relational-databases/replication/synchronize-a-pull-subscription.md)을 참조하세요.  
  
4.  비즈니스 논리 처리기 코드에서 디버깅 대상 메서드 또는 클래스 생성자 내에 중단점을 설정합니다. 비즈니스 논리 처리기에 구현할 수 있는 메서드에 대한 자세한 내용은 <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule> 메서드 항목을 참조하십시오.  
  
5.  비즈니스 논리 처리기를 디버그 모드로 빌드하고 어셈블리와 디버깅 기호 파일(.pdb)을 1단계에서 등록한 위치에 배포합니다.  
  
    > [!NOTE]  
    >  디버깅을 간소화하기 위해 비즈니스 논리 처리기 프로젝트와 구독을 동기화하는 프로젝트를 모두 포함하는 단일 Visual Studio .NET 솔루션을 만듭니다. 이 경우에 동기화 프로젝트를 시작 프로젝트로 설정하고, 디버깅 중에 1단계에서 등록한 위치에 비즈니스 논리 어셈블리를 배포하도록 빌드 환경을 구성합니다.  
  
6.  구독 또는 게시 데이터베이스를 대상으로 삽입, 업데이트 또는 삭제 명령을 실행합니다. 명령 및 실행 위치는 디버깅 대상 메서드에 따라 달라집니다.  
  
7.  3단계의 프로젝트를 디버그 모드로 시작하여 구독을 동기화합니다.  
  
8.  설정된 다른 중단점이 없고 올바른 명령이 복제된 경우 비즈니스 논리 처리기에 설정한 중단점에 도달하면 실행이 중지됩니다.  
  
### <a name="to-debug-a-business-logic-handler-on-a-web-server-using-web-synchronization-or-for-a-sql-server-compact-subscriber"></a>웹 동기화를 사용하는 웹 서버 또는 SQL Server Compact 구독자의 비즈니스 논리 처리기를 디버깅하려면  
  
1.  게시 및 배포를 구성하고 게시를 만들고 게시에 대한 끌어오기 구독을 만듭니다. 게시는 웹 동기화 또는 [!INCLUDE[ssEW](../../includes/ssew-md.md)] 구독자를 지원해야 합니다.  
  
2.  비즈니스 논리 처리기를 만들고 등록합니다. 자세한 내용은 [병합 아티클에 대한 비즈니스 논리 처리기 구현](../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md)을 참조하세요.  
  
3.  비즈니스 논리 처리기 코드에서 디버깅 대상 메서드 또는 클래스 생성자 내에 중단점을 설정합니다. 비즈니스 논리 처리기에 구현할 수 있는 메서드에 대한 자세한 내용은 <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule> 메서드 항목을 참조하십시오.  
  
4.  비즈니스 논리 처리기를 디버그 모드로 빌드하고 웹 서버에서 어셈블리와 디버깅 기호 파일(.pdb)을 1단계에서 등록한 위치에 배포합니다.  
  
    > [!NOTE]  
    >  어셈블리가 사용 중이어서 비즈니스 논리 처리기 빌드가 실패하는 경우에는 웹 서버의 명령 프롬프트에서 `iisreset` 명령을 입력하여 웹 서버를 다시 설정하십시오.  
  
5.  웹 동기화를 설정하고 구독을 동기화합니다. 동기화 중에 웹 서버는 등록된 어셈블리를 로드합니다.  
  
6.  Visual Studio .NET 디버거를 사용하여 웹 서버의 다음 프로세스 중 하나에 연결합니다.  
  
    -   w3wp.exe - Windows Server 2003  
  
    -   inetinfo.exe - Windows 2000 및 Windows XP  
  
7.  **출력** 창의 디버그 출력에서 등록된 어셈블리에 대한 기호가 올바르게 로드되었는지 확인합니다. 기호가 로드되지 않은 경우 4단계에서 올바른 .pdb 파일을 복사했는지 확인하고 5단계를 반복합니다.  
  
8.  구독 또는 게시 데이터베이스를 대상으로 삽입, 업데이트 또는 삭제 명령을 실행합니다. 명령 및 실행 위치는 디버깅 대상 메서드에 따라 달라집니다.  
  
9. Visual Studio 디버거를 사용하여 w3wp.exe 프로세스에 연결합니다.  
  
10. 웹 동기화를 사용하여 구독을 다시 동기화합니다.  
  
11. 설정된 다른 중단점이 없고 올바른 명령이 복제된 경우 비즈니스 논리 처리기에 설정한 중단점에 도달하면 실행이 중지됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [병합 아티클에 대한 비즈니스 논리 처리기 구현](../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md)  
  
  
