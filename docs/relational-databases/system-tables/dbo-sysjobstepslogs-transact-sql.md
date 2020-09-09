---
description: dbo.sysjobstepslogs(Transact-SQL)
title: dbo.sysjobstepslogs (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dbo.sysjobstepslogs_TSQL
- sysjobstepslogs_TSQL
- sysjobstepslogs
- dbo.sysjobstepslogs
dev_langs:
- TSQL
helpviewer_keywords:
- sysjobstepslogs system table
ms.assetid: 128c25db-0b71-449d-bfb2-38b8abcf24a0
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 067edf1d3c58df81eac4e49a6ea8d73385d7e21c
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89544581"
---
# <a name="dbosysjobstepslogs-transact-sql"></a>dbo.sysjobstepslogs(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  작업 단계 출력을 테이블에 쓰도록 구성되는 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업 단계에 대한 작업 단계 로그를 포함합니다. 이 테이블은 **msdb** 데이터베이스에 저장 됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**log_id**|**int**|작업 단계 로그의 ID입니다.|  
|**로깅할**|**nvarchar(max)**|작업 단계 로그 내용입니다.|  
|**date_created**|**datetime**|작업 단계 로그가 생성된 날짜 및 시간입니다.|  
|**date_modified**|**datetime**|작업 단계 로그가 마지막으로 수정된 날짜와 시간입니다.|  
|**log_size**|**int**|작업 단계 로그의 크기(바이트)입니다.|  
|**step_uid**|**uniqueidentifier**|작업 단계의 고유 식별자입니다.|  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;sp_help_jobsteplog &#40;](../../relational-databases/system-stored-procedures/sp-help-jobsteplog-transact-sql.md)   
 [Transact-sql&#41;sp_delete_jobsteplog &#40;](../../relational-databases/system-stored-procedures/sp-delete-jobsteplog-transact-sql.md)  
  
  
