---
title: SQL Server 에이전트 작업을 만들고 관리하도록 사용자 구성 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SQL Server Agent jobs, user configuration
- jobs [SQL Server Agent], user configuration
- SQLAgentUserRole database role
- proxy accounts [SQL Server Agent]
ms.assetid: 67897e3e-b7d0-43dd-a2e2-2840ec4dd1ef
caps.latest.revision: 24
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: e39427bf18fafd44bf48eb869d11d901a4dcea8f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36185318"
---
# <a name="configure-a-user-to-create-and-manage-sql-server-agent-jobs"></a>SQL Server 에이전트 작업을 만들고 관리하도록 사용자 구성
  이 항목에서는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업을 만들거나 실행하도록 사용자를 구성하는 방법에 대해 설명합니다.  
  
-   **시작하기 전 주의 사항:**  [보안](#Security)  
  
-   **다음을 사용하여 SQL Server 에이전트 작업을 만들고 관리하도록 사용자 구성**  [SQL Server Management Studio](#SSMS)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Security"></a> 보안  
 사용자가 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업을 만들거나 실행할 수 있도록 구성하려면 먼저 기존 SQL Server 로그인이나 msdb 역할을 msdb 데이터베이스의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 고정 데이터베이스 역할인 SQLAgentUserRole, SQLAgentReaderRole 또는 SQLAgentOperatorRole 중 하나에 추가해야 합니다.  
  
 기본적으로 이러한 데이터베이스 역할의 멤버는 자신의 계정으로 실행되는 고유한 작업 단계를 만들 수 있습니다. 관리 권한이 없는 이러한 사용자가 다른 작업 단계 유형(예: [!INCLUDE[ssIS](../../includes/ssis-md.md)] 패키지)을 실행하는 작업을 실행하려면 프록시 계정에 액세스할 수 있어야 합니다. sysadmin 고정 서버 역할의 모든 멤버에게는 프록시 계정을 만들고 수정하고 삭제할 수 있는 권한이 있습니다. 이러한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 고정 데이터베이스 역할과 관련된 사용 권한에 대한 자세한 내용은 [SQL Server 에이전트 고정 데이터베이스 역할](sql-server-agent-fixed-database-roles.md)을 참조하세요.  
  
####  <a name="Permissions"></a> Permissions  
 자세한 내용은 [Implement SQL Server Agent Security](implement-sql-server-agent-security.md)을 참조하세요.  
  
##  <a name="SSMS"></a> SQL Server Management Studio 사용  
 **SQL Server 에이전트 고정 데이터베이스 역할에 SQL 로그인이나 msdb 역할을 추가하려면**  
  
1.  **개체 탐색기**에서 서버를 확장합니다.  
  
2.  **보안**을 확장한 다음 **로그인**을 확장합니다.  
  
3.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 고정 데이터베이스 역할에 추가하려는 로그인을 마우스 오른쪽 단추로 클릭한 다음 **속성**을 선택합니다.  
  
4.  에 **사용자 매핑** 의 페이지는 **로그인 속성** 대화 상자를 포함 하는 행 선택 `msdb`합니다.  
  
5.  **데이터베이스 역할 멤버 자격: msdb**에서 적합한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 고정 데이터베이스 역할을 선택합니다.  
  
 **SQL Server 에이전트 작업 단계를 만들고 관리하는 프록시 계정을 구성하려면**  
  
1.  **개체 탐색기**에서 서버를 확장합니다.  
  
2.  **SQL Server 에이전트**를 확장합니다.  
  
3.  **프록시** 를 마우스 오른쪽 단추로 클릭하고 **새 프록시**를 선택합니다.  
  
4.  **새 프록시 계정** 대화 상자의 **일반** 페이지에서 새 프록시의 프록시 이름, 자격 증명 이름 및 설명을 지정합니다. SQL Server 에이전트 프록시를 만들기 전에 자격 증명을 먼저 만들어야 합니다. 자격 증명을 만드는 방법에 대 한 자세한 내용은 참조 [자격 증명 만들기](../../relational-databases/security/authentication-access/create-a-credential.md) 및 [CREATE CREDENTIAL &#40;TRANSACT-SQL&#41;](/sql/t-sql/statements/create-credential-transact-sql)합니다.  
  
5.  이 프록시에 대한 적절한 하위 시스템을 선택합니다.  
  
6.  **보안 주체** 페이지에서 프록시 계정에 대한 액세스 권한을 부여 또는 제거할 로그인이나 역할을 추가하거나 제거합니다.  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server 에이전트 보안 구현](implement-sql-server-agent-security.md)  
  
  
