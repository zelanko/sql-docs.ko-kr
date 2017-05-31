---
title: "작업 보기 또는 수정 | Microsoft 문서"
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
- jobs [SQL Server Agent], modifying
- jobs [SQL Server Agent], viewing
- modifying jobs
- viewing jobs
- SQL Server Agent jobs, viewing
- SQL Server Agent jobs, modifying
- displaying jobs
ms.assetid: 57f649b8-190c-4304-abd7-7ca5297deab7
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: fb14f6a9c778a48454a9f8d2e64f49d724558e88
ms.contentlocale: ko-kr
ms.lasthandoff: 04/11/2017

---
# <a name="view-or-modify-jobs"></a>작업 보기 또는 수정
생성한 모든 작업을 볼 수 있습니다. 작업을 실행한 후 해당 기록도 볼 수 있습니다. 작업 기록을 보면 작업 실행 시간, 작업 전체 상태, 각 작업 단계의 상태 등을 확인할 수 있습니다. 과거 작업 실패 여부, 마지막으로 작업이 완료된 시간 및 각 작업 실행 시 작성된 출력 등을 볼 수 있습니다. **sysadmin** 고정 서버 역할의 멤버는 소유자에 관계없이 모든 작업을 보거나 수정할 수 있습니다.  
  
> [!NOTE]  
> 최소 한 번 이상 작업을 실행해야 작업 기록이 남습니다. 작업 기록 로그의 전체 크기와 작업당 크기를 제한할 수 있습니다.  
  
끝으로 새로운 요구 사항을 충족하도록 작업을 수정할 수 있습니다. 다음을 수정할 수 있습니다.  
  
-   응답 옵션  
  
-   일정  
  
-   작업 단계  
  
-   소유권  
  
-   작업 범주  
  
-   대상 서버(다중 서버 작업만)  
  
다중 서버 작업에 변경한 내용을 적용하려면 변경 내용을 다운로드 목록에 올려 대상 서버가 업데이트된 작업을 다운로드할 수 있도록 해야 합니다. 대상 서버에 최신 작업 정의를 적용하려면 다중 서버 작업을 다음과 같이 업데이트한 후에 INSERT 명령을 게시하십시오.  
  
```  
EXECUTE sp_post_msx_operation 'INSERT', 'JOB', '<job id>'  
```  
  
자세한 내용은 [sp_purge_jobhistory(Transact-SQL)](http://msdn.microsoft.com/en-us/237f9bad-636d-4262-9bfb-66c034a43e88)를 참조하세요.  
  
**sysadmin** 고정 서버 역할의 멤버는 모든 작업의 정의나 기록을 볼 수 있고 모든 작업을 수정할 수 있습니다.  
  
## <a name="related-tasks"></a>관련 작업  
  
|||  
|-|-|  
|**Description**|**항목**|  
|[!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트 작업을 보는 방법에 대해 설명합니다.|[View a Job](../../ssms/agent/view-a-job.md)|  
|[!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트 작업 기록 로그를 보는 방법에 대해 설명합니다.|[View the Job History](../../ssms/agent/view-the-job-history.md)|  
|[!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트 작업 기록 로그의 내용을 삭제하는 방법에 대해 설명합니다.|[Clear the Job History Log](../../ssms/agent/clear-the-job-history-log.md)|  
|[!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트 작업 기록 로그의 크기 제한을 설정하는 방법에 대해 설명합니다.|[Resize the Job History Log](../../ssms/agent/resize-the-job-history-log.md)|  
|[!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트 작업의 속성을 변경하는 방법에 대해 설명합니다.|[Modify a Job](../../ssms/agent/modify-a-job.md)|  
  
## <a name="see-also"></a>참고 항목  
[sysjobhistory](http://msdn.microsoft.com/en-us/1b1fcdbb-2af2-45e6-bf3f-e8279432ce13)  
  

