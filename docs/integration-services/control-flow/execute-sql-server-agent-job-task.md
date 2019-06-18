---
title: SQL Server 에이전트 작업 실행 태스크 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.executesqlserveragentjobtask.f1
helpviewer_keywords:
- Execute SQL Server Agent Job task [Integration Services]
- jobs [Integration Services]
- SQL Server Agent [Integration Services]
ms.assetid: 3aa3bc0e-1a1c-452e-81b8-b4e3422ea053
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: a6cdbfec852a8aaf8eb81f77c0e5f7aadba140db
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65727729"
---
# <a name="execute-sql-server-agent-job-task"></a>SQL Server 에이전트 작업 실행 태스크

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업 실행 태스크는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업을 실행합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트는 SQL Server의 인스턴스에 정의된 작업을 실행하는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 서비스입니다. Transact-SQL 문과 ActiveX 스크립트를 실행하는 작업을 만들거나 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 및 복제 유지 관리 태스크를 수행하거나 패키지를 실행할 수 있습니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 모니터링하고 경고가 발생하도록 작업을 구성할 수도 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업은 일반적으로 반복해서 수행하는 태스크를 자동화하는 데 사용됩니다. 자세한 내용은 [작업 구현](../../ssms/agent/implement-jobs.md)을 참조하세요.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업 실행 태스크를 사용하면 패키지가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 요소에 관련된 관리 태스크를 수행할 수 있습니다. 예를 들어 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업은 **sp_enum_dtspackages** 와 같은 시스템 저장 프로시저를 실행하여 폴더의 패키지 목록을 가져올 수 있습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트가 실행되고 있어야만 로컬 또는 다중 서버 관리 작업이 자동으로 실행될 수 있습니다.  
  
 이 태스크는 **sp_start_job** 시스템 프로시저를 캡슐화하고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업 이름을 프로시저에 인수로 전달합니다. 자세한 내용은 [sp_start_job&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-start-job-transact-sql.md)을 참조하세요.  
  
## <a name="configuring-the-execute-sql-server-agent-job-task"></a>SQL Server 에이전트 작업 실행 태스크 구성  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 속성을 설정할 수 있습니다. 이 태스크는 **디자이너의** 도구 상자 **에 있는** 유지 관리 계획 태스크 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 섹션에서 수행할 수 있습니다.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목을 클릭하십시오.  
  
-   [SQL Server 에이전트 작업 실행 태스크&#40;유지 관리 계획&#41;](../../relational-databases/maintenance-plans/execute-sql-server-agent-job-task-maintenance-plan.md)  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 이러한 속성을 설정하는 방법을 보려면 다음 항목을 클릭하십시오.  
  
-   [태스크 또는 컨테이너의 속성 설정](https://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
  
