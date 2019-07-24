---
title: MSmerge_partition_groups (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_partition_groups_TSQL
- MSmerge_partition_groups
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_partition_groups system table
ms.assetid: 5d56d780-ee40-4afc-9c2a-d1723d86e430
author: stevestein
ms.author: sstein
ms.openlocfilehash: 362735d33f835c7b66e4f0994fd5c4ff6f084f15
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68102188"
---
# <a name="msmergepartitiongroups-transact-sql"></a>MSmerge_partition_groups(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  합니다 **MSmerge_partition_groups** 테이블은 각 사전 계산 파티션이 지정된 된 데이터베이스에 대 한 하나의 행을 저장 합니다. 이 테이블은 나열된 열 이외에도 매개 변수가 있는 행 필터에서 사용된 각 함수당 한 개의 열 또한 포함합니다. 예를 들어, 명명 된 열 **HOST_NAME_FN** 필터를 사용 하는 경우 테이블에 추가 되는 [HOST_NAME](../../t-sql/functions/host-name-transact-sql.md) 함수입니다. 또한 해당 게시자와 동기화한 함수 값의 각 고유 집합에 대한 행이 하나씩 저장됩니다. 이러한 모든 함수에 대 한 정확히 같은 값으로 동기화 하는 두 개 이상의 구독자가 표의 동일한 행을 공유 하 고는 모든 공유 하므로 동일한 파티션 id입니다. 이 테이블은 게시 데이터베이스에 저장됩니다.  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|**partition_id**|**int**|사전 계산 파티션에 대해 고유한 ID를 제공하는 ID 열입니다.|  
|**publication_number**|**smallint**|에 저장 되는 게시 번호 **sysmergepublications**합니다.|  
|**maxgen_whenadded**|**bigint**|현재 행이 테이블에 삽입될 때 게시자에 알려진 최상위 세대입니다.|  
|**using_partition_groups**|**bit**|파티션이 사전 계산 파티션을 사용하는 게시에 속하는지 여부를 나타내며 다음 값 중 하나일 수 있습니다.<br /><br /> **0** = 게시에서 사전 계산된 파티션을 사용 하지 않습니다.<br /><br /> **1** = 사전 계산된 파티션을 게시 사용<br /><br /> 자세한 내용은 [사전 계산 파티션으로 매개 변수가 있는 필터 성능 최적화](../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md)를 참조하세요.|  
|**HOST_NAME_FN**|**nvarchar(128)**|매개 변수가 있는 행 필터를 사용하여 파티션을 생성할 때 제공된 값입니다. 자세한 내용은 [매개 변수가 있는 행 필터](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)를 참조하십시오.|  
  
## <a name="see-also"></a>관련 항목  
 [복제 테이블 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
