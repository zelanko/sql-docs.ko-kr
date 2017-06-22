---
title: "SQL Server 에이전트 오류 로그 이름 바꾸기(SQL Server Management Studio) | Microsoft 문서"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- logs [SQL Server], SQL Server Agent
- renaming SQL Server Agent error log
- SQL Server Agent, errors
- errors [SQL Server Agent]
ms.assetid: dee2b199-48af-44cb-9177-d029a5edb169
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: a6da7992bd9767f4a5b05c307c85af694b074729
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="rename-a-sql-server-agent-error-log-sql-server-management-studio"></a>SQL Server 에이전트 오류 로그 이름 바꾸기(SQL Server Management Studio)
이 항목에서는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]를 사용하여 [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)]에서 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트 오류가 기록된 파일의 이름을 바꾸는 방법에 대해 설명합니다.  
  
**항목 내용**  
  
-   **시작하기 전에:**  
  
    [제한 사항](#Restrictions)  
  
    [보안](#Security)  
  
-   [SQL Server Management Studio를 사용하여 SQL Server 에이전트 오류 로그의 이름을 바꾸려면](#SSMSProcedure)  
  
## <a name="BeforeYouBegin"></a>시작하기 전에  
  
### <a name="Restrictions"></a>제한 사항  
  
-   사용 권한이 있는 경우에만 개체 탐색기에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트 노드가 표시됩니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트에서 새 로그 파일에 기록하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트 서비스를 다시 시작해야 합니다.  
  
### <a name="Security"></a>보안  
  
#### <a name="Permissions"></a>Permissions  
해당 기능을 수행하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에서 **sysadmin** 고정 서버 역할 멤버인 계정의 자격 증명을 사용하도록 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]에이전트를 구성해야 합니다. 이 계정에는 다음과 같은 Windows 사용 권한이 필요합니다.  
  
-   서비스로 로그온(SeServiceLogonRight)  
  
-   프로세스 수준 토큰 바꾸기(SeAssignPrimaryTokenPrivilege)  
  
-   트래버스 검사 무시(SeChangeNotifyPrivilege)  
  
-   프로세스의 메모리 할당량 조정(SeIncreaseQuotaPrivilege)  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트 서비스 계정에 필요한 Windows 사용 권한에 대한 자세한 내용은 [SQL Server 에이전트 서비스의 계정 선택](../../ssms/agent/select-an-account-for-the-sql-server-agent-service.md) 및 [Windows 서비스 계정 설정](http://msdn.microsoft.com/en-us/309b9dac-0b3a-4617-85ef-c4519ce9d014)을 참조하세요.  
  
## <a name="SSMSProcedure"></a>SQL Server Management Studio 사용  
  
#### <a name="to-rename-a-sql-server-agent-error-log"></a>SQL Server 에이전트 오류 로그 이름을 바꾸려면  
  
1.  **개체 탐색기**에서 더하기 기호를 클릭하여 이름을 바꾸려는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트 오류 로그가 포함된 서버를 확장합니다.  
  
2.  더하기 기호를 클릭하여 **SQL Server 에이전트**를 확장합니다.  
  
3.  **오류 로그** 폴더를 마우스 오른쪽 단추로 클릭한 다음 **구성**을 선택합니다.  
  
4.  **SQL Server 에이전트 오류 로그 구성** 대화 상자의 **오류 로그 파일** 상자에서 오류 로그에 대한 새 파일 경로 및 파일 이름을 입력합니다. 또는 줄임표 **(...)** 를 클릭하여 **에이전트 오류 로그 위치를 지정하십시오.** 대화 상자를 엽니다.  
  
5.  완료되었으면 **확인**을 클릭합니다.  
  

