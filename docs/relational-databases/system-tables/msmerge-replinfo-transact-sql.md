---
title: MSmerge_replinfo (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- MSmerge_replinfo_TSQL
- MSmerge_replinfo
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_replinfo system table
ms.assetid: b0924094-c0cc-49c1-869a-65be0d0465a0
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7257ce7d12fe4797c09836de2de45829500afd6b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47790661"
---
# <a name="msmergereplinfo-transact-sql"></a>MSmerge_replinfo(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  합니다 **MSmerge_replinfo** 각 구독에 대해 하나의 행을 포함 하는 테이블입니다. 이 테이블은 구독에 대한 정보를 추적합니다. 이 테이블은 게시 및 구독 데이터베이스에 저장됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**repid**|**uniqueidentifier**|복제에 대한 고유 ID입니다.|  
|**use_interactive_resolver**|**bit**|조정하는 동안 대화형 해결 프로그램을 사용할지 여부를 지정합니다.<br /><br /> **0** = 대화형 해결 프로그램을 사용 하지 않습니다.<br /><br /> **1** = 대화형 해결 프로그램을 사용 합니다.|  
|**validation_level**|**int**|구독에서 실행할 유효성 검사의 유형입니다. 지정한 유효성 검사 수준은 다음 값 중 하나를 사용할 수 있습니다.<br /><br /> **0** = 없습니다 유효성을 검사 합니다.<br /><br /> **1** = 행 개수만 유효성을 검사 합니다.<br /><br /> **2** = 행 개수 및 체크섬 유효성 검사 합니다.<br /><br /> **3** = 행 개수 및 이진 체크섬 유효성 검사 합니다.|  
|**resync_gen**|**bigint**|구독을 다시 동기화하는 데 사용되는 생성 번호입니다. 값이 **-1** 구독이 다시 동기화에 대 한 표시 되지 않도록 나타냅니다.|  
|**login_name**|**sysname**|구독을 만든 사용자의 이름입니다.|  
|**호스트 이름**|**sysname**|구독에 대한 파티션을 생성할 때 매개 변수가 있는 행 필터에서 사용되는 값입니다.|  
|**merge_jobid**|**binary(16)**|이 구독에 대한 병합 작업 ID입니다.|  
|**sync_info**|**int**|내부적으로만 사용됩니다.|  
  
## <a name="see-also"></a>관련 항목  
 [복제 테이블 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
