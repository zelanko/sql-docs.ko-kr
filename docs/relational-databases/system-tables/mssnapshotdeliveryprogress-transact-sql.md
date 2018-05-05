---
title: MSsnapshotdeliveryprogress (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- MSsnapshotdeliveryprogress_TSQL
- MSsnapshotdeliveryprogress
dev_langs:
- TSQL
helpviewer_keywords:
- MSsnapshotdeliveryprogress system table
ms.assetid: 9164bfe2-6fc4-4b52-946a-09ea3cf67041
caps.latest.revision: 30
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 0989999080b57bf2f78b6a297df29a0ee8a32f35
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="mssnapshotdeliveryprogress-transact-sql"></a>MSsnapshotdeliveryprogress(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSsnapshotdeliveryprogress** 테이블은 성공적으로 배달 된 구독자에 스냅숏을 적용 되는 경우 파일을 추적 하는 데 사용 됩니다. 이 데이터는 병합 에이전트가 세션 중에 파일을 모두 배달하지 못한 경우 파일 배달을 다시 시작하는 데 사용되어 다음에 병합 에이전트가 실행될 때 같은 파일을 다시 배달하지 않도록 합니다. 이 테이블은 구독 데이터베이스의 구독자에 저장됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**session_token**|**nvarchar(260)**|파일을 성공적으로 배달한 스냅숏 폴더의 경로를 식별합니다. 문자열 매개 변수가 있는 필터를 사용 하는 게시에 대 한 **dynsnap** 값에 추가 됩니다.|  
|**progress_token_hash**|**int**|생성 된 해시 값의 값에 따라 *progress_token* 사용 되는 대 한 조회 효율성을 높이 주어진 *progress_token* 값입니다.|  
|**progress_token**|**nvarchar(500)**|성공적으로 배달된 파일을 식별합니다. 값은 파일 이름과 경로의 조합입니다.|  
|**progress_timestamp**|**datetime**|**datetime** 스냅숏 파일을 성공적으로 배달를 나타내는 값입니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [복제 테이블 &#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
