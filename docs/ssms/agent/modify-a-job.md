---
title: "작업 수정 | Microsoft 문서"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-agent
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- jobs [SQL Server Agent], modifying
- modifying jobs
- SQL Server Agent jobs, modifying
ms.assetid: dd5e5f20-20c4-4ab9-a19a-db87577dcd43
caps.latest.revision: "5"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: b62eb721f8e0bbfdf00e916d81e2bb4dee1058d7
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/17/2018
---
# <a name="modify-a-job"></a>Modify a Job
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 이 항목에서는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)], [!INCLUDE[tsql](../../includes/tsql_md.md)] 또는 SQL Server 관리 개체를 사용하여 [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)]에서 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트 작업의 속성을 변경하는 방법에 대해 설명합니다.  
  
**항목 내용**  
  
-   **시작하기 전 주의 사항:** ,  
  
    [제한 사항](#Restrictions)  
  
    [보안](#Security)  
  
-   **작업을 수정하려면:**  
  
    [SQL Server Management Studio](#SSMS)  
  
    [Transact-SQL](#TSQL)  
  
    [SQL Server 관리 개체](#SMO)  
  
## <a name="BeforeYouBegin"></a>시작하기 전 주의 사항  
  
### <a name="Restrictions"></a>제한 사항  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트 마스터 작업은 로컬 및 원격 서버 모두에서 대상이 될 수 없습니다.  
  
### <a name="Security"></a>보안  
**sysadmin** 고정 서버 역할의 멤버가 아닌 경우 자신이 소유한 작업만 수정할 수 있습니다. 자세한 내용은 [Implement SQL Server Agent Security](../../ssms/agent/implement-sql-server-agent-security.md)을 참조하세요.  
  
## <a name="SSMS"></a>SQL Server Management Studio 사용  
  
#### <a name="to-modify-a-job"></a>작업을 수정하려면  
  
1.  **개체 탐색기** 에서 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]인스턴스에 연결한 다음 해당 인스턴스를 확장합니다.  
  
2.  **SQL Server 에이전트**, **작업**을 차례로 확장한 다음 수정할 작업을 마우스 오른쪽 단추로 클릭하고 **속성**을 클릭합니다.  
  
3.  **작업 속성** 대화 상자에서 해당 페이지를 사용하여 작업의 속성, 단계, 일정, 경고 및 알림을 업데이트합니다.  
  
## <a name="TSQL"></a>Transact-SQL 사용  
  
#### <a name="to-modify-a-job"></a>작업을 수정하려면  
  
1.  개체 탐색기에서 데이터베이스 엔진의 인스턴스에 연결한 다음 해당 인스턴스를 확장합니다.  
  
2.  도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  쿼리 창에서 다음 시스템 저장 프로시저를 사용하여 작업을 수정합니다.  
  
    -   작업의 특성을 변경하려면 [sp_update_job(Transact-SQL)](http://msdn.microsoft.com/en-us/cbdfea38-9e42-47f3-8fc8-5978b82e2623) 을 실행합니다.  
  
    -   작업 정의에 대한 일정 정보를 변경하려면 [sp_update_schedule(Transact-SQL)](http://msdn.microsoft.com/en-us/97b3119b-e43e-447a-bbfb-0b5499e2fefe) 을 실행합니다.  
  
    -   새 작업 단계를 추가하려면 [sp_add_jobstep(Transact-SQL)](http://msdn.microsoft.com/en-us/97900032-523d-49d6-9865-2734fba1c755) 을 실행합니다.  
  
    -   기존의 작업 단계를 변경하려면 [sp_update_jobstep(Transact-SQL)](http://msdn.microsoft.com/en-us/e158802c-c347-4a5d-bf75-c03e5ae56e6b) 을 실행합니다.  
  
    -   작업에서 작업 단계를 제거하려면 [sp_delete_jobstep(Transact-SQL)](http://msdn.microsoft.com/en-us/421ede8e-ad57-474a-9fb9-92f70a3e77e3) 을 실행합니다.  
  
    -   SQL Server 에이전트 마스터 작업을 수정하는 추가 저장 프로시저:  
  
        -   현재 작업과 연결되어 있는 서버를 삭제하려면 [sp_delete_jobserver(Transact-SQL)](http://msdn.microsoft.com/en-us/6d63ed32-68cf-4d8f-aa40-05a3826e05b8) 를 실행합니다.  
  
        -   현재 작업과 서버를 연결하려면 [sp_add_jobserver(Transact-SQL)](http://msdn.microsoft.com/en-us/485252cc-0081-490a-9bd1-cbbd68eea286) 를 실행합니다.  
  
## <a name="SMO"></a>SQL Server 관리 개체 사용  
**작업을 수정하려면**  
  
Visual Basic, Visual C#, PowerShell 등 선택한 프로그래밍 언어를 사용하여 **Job** 클래스를 사용합니다. 자세한 내용은 [SMO(SQL Server 관리 개체)](http://msdn.microsoft.com/library/ms162169.aspx)를 참조하세요.  
  
