---
title: "작업 전송 태스크 편집기(작업 페이지) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.transferjobstask.jobs.f1"
helpviewer_keywords: 
  - "작업 전송 태스크 편집기"
ms.assetid: e72b1dc7-8cda-4ee6-abb5-d438370f04df
caps.latest.revision: 24
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 24
---
# 작업 전송 태스크 편집기(작업 페이지)
  **작업 전송 태스크 편집기** 대화 상자의 **작업** 페이지를 사용하여 하나 이상의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 한 인스턴스에서 다른 인스턴스로 복사하기 위한 속성을 지정할 수 있습니다. 작업 전송 태스크에 대한 자세한 내용은 [Transfer Jobs Task](../../integration-services/control-flow/transfer-jobs-task.md)을 참조하십시오.  
  
> [!NOTE]  
>  원본 서버의 작업에 액세스하려면 사용자가 적어도 서버에서 **SQLAgentUserRole** 고정 데이터베이스 역할의 멤버여야 합니다. 대상 서버에 작업을 만들려면 사용자가 **sysadmin** 고정 서버 역할의 멤버이거나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 고정 데이터베이스 역할 중 하나여야 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 고정 데이터베이스 역할 및 해당 권한에 대한 자세한 내용은 [SQL Server 에이전트 고정 데이터베이스 역할](../../ssms/agent/sql-server-agent-fixed-database-roles.md)을 참조하세요.  
  
## 옵션  
 **SourceConnection**  
 목록에서 SMO 연결 관리자를 선택하거나 **\<새 연결...>**을 클릭하여 원본 서버에 대한 새 연결을 만듭니다.  
  
 **DestinationConnection**  
 목록에서 SMO 연결 관리자를 선택하거나 **\<새 연결...>**을 클릭하여 대상 서버에 대한 새 연결을 만듭니다.  
  
 **TransferAllJobs**  
 원본 서버에서 대상 서버로 모든 SQL Server 에이전트 작업을 복사할지, 아니면 지정한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업만 복사할지를 선택합니다.  
  
 이 속성의 옵션은 다음 표에 나열되어 있습니다.  
  
|Value|Description|  
|-----------|-----------------|  
|**True**|모든 작업을 복사합니다.|  
|**False**|지정한 작업만 복사합니다.|  
  
 **JobsList**  
 복사할 작업을 선택하려면 찾아보기 단추**(…)**를 클릭합니다. 하나 이상의 작업을 선택해야 합니다.  
  
> [!NOTE]  
>  복사할 작업을 선택하기 전에 **SourceConnection**을 지정합니다.  
  
 **TransferAllJobs** 를 **True** 로 설정하면 **JobsList**옵션을 사용할 수 없습니다.  
  
 **IfObjectExists**  
 태스크에서 대상 서버에 이미 있는 작업과 이름이 동일한 작업을 처리하는 방법을 선택합니다.  
  
 이 속성의 옵션은 다음 표에 나열되어 있습니다.  
  
|Value|Description|  
|-----------|-----------------|  
|**FailTask**|대상 서버에 이름이 동일한 작업이 이미 있는 경우 태스크가 실패합니다.|  
|**Overwrite**|대상 서버에 이름이 동일한 태스크가 있는 경우 이를 덮어씁니다.|  
|**Skip**|대상 서버에 이름이 동일한 태스크가 있는 경우 이를 건너뜁니다.|  
  
 **EnableJobsAtDestination**  
 대상 서버로 복사한 작업을 활성화할지 여부를 선택합니다.  
  
 이 속성의 옵션은 다음 표에 나열되어 있습니다.  
  
|Value|Description|  
|-----------|-----------------|  
|**True**|대상 서버에서 작업을 활성화합니다.|  
|**False**|대상 서버에서 작업을 비활성화합니다.|  
  
## 관련 항목:  
 [Integration Services 오류 및 메시지 참조](../../integration-services/integration-services-error-and-message-reference.md)   
 [Integration Services 태스크](../../integration-services/control-flow/integration-services-tasks.md)   
 [작업 전송 태스크 편집기&#40;일반 페이지&#41;](../../integration-services/control-flow/transfer-jobs-task-editor-general-page.md)   
 [식 페이지](../../integration-services/expressions/expressions-page.md)   
 [SMO 연결 관리자](../../integration-services/connection-manager/smo-connection-manager.md)  
  
  