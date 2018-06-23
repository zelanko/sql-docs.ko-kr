---
title: SQL Server 에이전트에서 Windows PowerShell 작업 단계 실행 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: f25f7549-c9b3-4618-85f2-c9a08adbe0e3
caps.latest.revision: 9
author: mgblythe
ms.author: mblythe
manager: jhubbard
ms.openlocfilehash: 58837a63969baff47ff79bcebb78b6dd24deb31e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36091517"
---
# <a name="run-windows-powershell-steps-in-sql-server-agent"></a>SQL Server 에이전트에서 Windows PowerShell 작업 단계 실행
  SQL Server 에이전트를 사용하여 일정에 따라 SQL Server PowerShell 스크립트를 실행할 수 있습니다.  
  
1.  **시작하기 전에:**  [제한 사항](#LimitationsRestrictions)  
  
2.  **에서 SQL Server 에이전트에서 PowerShell을 실행하려면**  [PowerShell 작업 단계](#PShellJob), [명령 프롬프트 작업 단계](#CmdExecJob)  
  
## <a name="before-you-begin"></a>시작하기 전 주의 사항  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에이전트 작업 단계 유형은 여러 가지가 있습니다. 각 유형은 복제 에이전트나 명령 프롬프트 환경과 같은 특정 환경을 구현하는 하위 시스템과 관련되어 있습니다. Windows PowerShell 스크립트를 코딩한 다음 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에이전트를 사용하여 예약된 시간에 실행되거나 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 이벤트에 대한 응답으로 실행되는 스크립트를 작업에 포함할 수 있습니다. 명령 프롬프트 작업 단계 또는 PowerShell 작업 단계를 사용하여 Windows PowerShell 스크립트를 실행할 수 있습니다.  
  
1.  PowerShell 작업 단계를 사용하여 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에이전트 하위 시스템에서 `sqlps` 유틸리티를 실행하도록 합니다. 이 유틸리티는 PowerShell 2.0을 시작하고 `sqlps` 모듈을 가져옵니다.  
  
2.  명령 프롬프트 작업 단계를 사용 하 여 PowerShell.exe를 실행 하 고 가져오는 스크립트를 지정 된 `sqlps` 모듈입니다.  
  
###  <a name="LimitationsRestrictions"></a> 제한 사항  
  
> [!CAUTION]  
>  PowerShell과 `sqlps` 모듈을 함께 실행하는 각 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에이전트 작업 단계에서는 약 20MB의 메모리를 사용하는 프로세스를 시작합니다. 따라서 많은 수의 Windows PowerShell 작업 단계를 동시에 실행하면 성능이 저하될 수 있습니다.  
  
##  <a name="PShellJob"></a> PowerShell 작업 단계 만들기  
 **PowerShell 작업 단계를 만들려면**  
  
1.  **SQL Server 에이전트**를 확장하고 새 작업을 만들거나 기존 작업을 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다. 작업을 만드는 방법은 [작업 만들기](../ssms/agent/create-jobs.md)를 참조하세요.  
  
2.  **작업 속성** 대화 상자에서 **단계** 페이지를 클릭한 다음 **새로 만들기**를 클릭합니다.  
  
3.  **새 작업 단계** 대화 상자에서 작업 **단계 이름**을 입력합니다.  
  
4.  **형식** 목록에서 **PowerShell**을 클릭합니다.  
  
5.  **다음 계정으로 실행** 목록에서 작업에 사용할 자격 증명을 가진 프록시 계정을 선택합니다.  
  
6.  **명령** 입력란에 작업 단계를 위해 실행될 PowerShell 스크립트 구문을 입력합니다. 아니면 **열기** 를 클릭한 다음 해당 스크립트 구문이 포함된 파일을 선택합니다.  
  
7.  **고급** 페이지를 클릭하여 작업 단계가 성공 또는 실패할 경우에 수행할 동작, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에이전트의 작업 단계 실행 시도 횟수, 그리고 다시 시도 간격 등 작업 단계 옵션을 설정합니다.  
  
##  <a name="CmdExecJob"></a> 명령 프롬프트 작업 단계 만들기  
 **CmdExec 작업 단계를 만들려면**  
  
1.  **SQL Server 에이전트**를 확장하고 새 작업을 만들거나 기존 작업을 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다. 작업을 만드는 방법은 [작업 만들기](../ssms/agent/create-jobs.md)를 참조하세요.  
  
2.  **작업 속성** 대화 상자에서 **단계** 페이지를 클릭한 다음 **새로 만들기**를 클릭합니다.  
  
3.  **새 작업 단계** 대화 상자에서 작업 **단계 이름**을 입력합니다.  
  
4.  **유형** 목록에서 **운영 체제(CmdExec)** 를 선택합니다.  
  
5.  **다음 계정으로 실행** 목록에서 해당 작업이 사용할 자격 증명을 가진 프록시 계정을 선택합니다. 기본적으로 CmdExec 작업 단계는 SQL Server 에이전트 서비스 계정의 컨텍스트에서 실행됩니다.  
  
6.  **성공한 명령의 프로세스 종료 코드** 상자에 0에서 999999까지의 값을 입력합니다.  
  
7.  **명령** 입력란에 실행할 PowerShell 스크립트를 지정하는 매개 변수와 함께 powershell.exe를 입력합니다.  
  
8.  **고급** 페이지를 클릭하여 작업 단계의 성공 또는 실패 여부에 따라 수행할 동작, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에이전트가 작업 단계를 수행할 횟수, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에이전트가 작업 단계 출력을 쓸 파일 등의 작업 단계 옵션을 설정합니다. **sysadmin** 고정 서버 역할의 멤버만 운영 체제 파일에 작업 단계 출력을 쓸 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server PowerShell](sql-server-powershell.md)  
  
  