---
description: MSmerge_history(Transact-SQL)
title: MSmerge_history (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_history_TSQL
- MSmerge_history
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_history system table
ms.assetid: 936195ad-ca07-41a8-a1a0-6699b6e63403
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 348df963920d35aeb874a83cad83701995d563cd
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89540886"
---
# <a name="msmerge_history-transact-sql"></a>MSmerge_history(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **MSmerge_history** 테이블에는 이전 병합 에이전트 작업 세션의 결과에 대 한 자세한 설명이 포함 된 기록 행이 포함 되어 있습니다. 이 테이블은 에이전트가 출력한 각 줄당 한 개의 행을 포함하며 배포 데이터베이스와 각 구독 데이터베이스에 사용됩니다. 배포 데이터베이스의 경우 이 테이블에는 배포자를 사용하는 모든 병합 게시 및 구독에 대한 기록이 포함되고, 각 구독 데이터베이스의 경우 이 테이블에는 구독자가 구독하는 게시에 대한 기록이 포함됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**session_id**|**int**|병합 에이전트 작업의 ID입니다.|  
|**agent_id**|**int**|병합 에이전트의 ID입니다.|  
|**주석만**|**nvarchar(255)**|메시지 텍스트입니다.|  
|**error_id**|**int**|[MSrepl_errors](../../relational-databases/system-tables/msrepl-errors-transact-sql.md) 시스템 테이블에 있는 오류의 ID입니다.|  
|**timestamp**|**timestamp**|이 테이블의 타임스탬프 열입니다.|  
|**updatable_row**|**bit**|기록 행을 덮어쓸 수 있는 경우 **1** 로 설정 합니다.|  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;복제 테이블 ](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
