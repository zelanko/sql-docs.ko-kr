---
title: "마스터 서버에서 대상 서버 제거 | Microsoft 문서"
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
- SQL Server Agent jobs, target servers
- target servers [SQL Server], defecting
- SQL Server Agent jobs, master servers
- master servers [SQL Server], defecting target servers
- defecting target servers
ms.assetid: a6da262b-7b38-4ce4-bfd6-6a557c6e8a84
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 660fbd83ba89ceb38ca240fe2c8c7d2d6d6b8dcd
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="defect-a-target-server-from-a-master-server"></a>Defect a Target Server from a Master Server
이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)]에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)], [!INCLUDE[tsql](../../includes/tsql_md.md)] 또는 SMO(SQL Server 관리 개체)를 사용하여 마스터 서버에서 대상 서버를 제거하는 방법에 대해 설명합니다. 이 프로시저를 대상 서버에서 실행합니다.  
  
**항목 내용**  
  
-   **시작하기 전에:**  
  
    [보안](#Security)  
  
-   **대상 서버를 제거하려면:**  
  
    [SQL Server Management Studio](#SSMSProcedure)  
  
    [Transact-SQL](#TsqlProcedure)  
  
    [SMO](#PowerShellProcedure)  
  
## <a name="BeforeYouBegin"></a>시작하기 전에  
  
### <a name="Security"></a>보안  
  
#### <a name="Permissions"></a>Permissions  
이 저장 프로시저를 실행하려면 사용자가 **sysadmin** 고정 서버 역할의 멤버여야 합니다.  
  
## <a name="SSMSProcedure"></a>SQL Server Management Studio 사용  
  
#### <a name="to-defect-a-target-server-from-a-master-server"></a>마스터 서버에서 대상 서버를 제거하려면  
  
1.  **개체 탐색기**에서 대상 서버로 구성된 서버를 확장합니다.  
  
2.  **SQL Server 에이전트**를 마우스 오른쪽 단추로 클릭하고 **다중 서버 관리**를 가리킨 다음 **제거**를 클릭합니다.  
  
3.  **예** 를 클릭하여 마스터 서버에서 이 대상 서버를 제거할 것을 확인합니다.  
  
## <a name="TsqlProcedure"></a>Transact-SQL 사용  
  
#### <a name="to-defect-a-target-server-from-a-master-server"></a>마스터 서버에서 대상 서버를 제거하려면  
  
1.  [!INCLUDE[ssDE](../../includes/ssde_md.md)]에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
```  
sp_msx_defect ;  
```  
  
자세한 내용은 [sp_msx_defect(Transact-SQL)](http://msdn.microsoft.com/en-us/0dfd963a-3bc5-4b58-94f7-aec976da2883)를 참조하세요.  
  
## <a name="PowerShellProcedure"></a>SMO(SQL Server 관리 개체) 사용  
**MsxDefect 메서드**를 사용합니다.  
  
## <a name="see-also"></a>참고 항목  
[다중 서버 환경 만들기](../../ssms/agent/create-a-multiserver-environment.md)  
[기업 내 관리 자동화](../../ssms/agent/automated-administration-across-an-enterprise.md)  
[마스터 서버에서 여러 대상 서버 제거](../../ssms/agent/defect-multiple-target-servers-from-a-master-server.md)  
  

