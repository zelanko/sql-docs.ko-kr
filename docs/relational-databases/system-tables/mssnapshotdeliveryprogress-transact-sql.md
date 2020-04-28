---
title: MSsnapshotdeliveryprogress (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSsnapshotdeliveryprogress_TSQL
- MSsnapshotdeliveryprogress
dev_langs:
- TSQL
helpviewer_keywords:
- MSsnapshotdeliveryprogress system table
ms.assetid: 9164bfe2-6fc4-4b52-946a-09ea3cf67041
author: stevestein
ms.author: sstein
ms.openlocfilehash: 638bea3db68712300ad2284e50676bf1df67c9ae
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68139809"
---
# <a name="mssnapshotdeliveryprogress-transact-sql"></a>MSsnapshotdeliveryprogress(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSsnapshotdeliveryprogress** 테이블은 스냅숏이 적용 될 때 구독자에 성공적으로 배달 된 파일을 추적 하는 데 사용 됩니다. 이 데이터는 병합 에이전트가 세션 중에 파일을 모두 배달하지 못한 경우 파일 배달을 다시 시작하는 데 사용되어 다음에 병합 에이전트가 실행될 때 같은 파일을 다시 배달하지 않도록 합니다. 이 테이블은 구독 데이터베이스의 구독자에 저장됩니다.  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|**session_token**|**nvarchar(260)**|파일을 성공적으로 배달한 스냅샷 폴더의 경로를 식별합니다. 매개 변수가 있는 필터를 사용 하는 게시의 경우 문자열 **dynsnap** 이 값에 추가 됩니다.|  
|**progress_token_hash**|**int**|지정 된 *progress_token* 값에 대 한 조회 효율성을 향상 시키는 데 사용 되는 *progress_token* 값을 기준으로 생성 된 해시 값입니다.|  
|**progress_token**|**nvarchar (500)**|성공적으로 배달된 파일을 식별합니다. 값은 파일 이름과 경로의 조합입니다.|  
|**progress_timestamp**|**datetime**|스냅숏 파일이 성공적으로 전달 된 시간을 나타내는 **datetime** 값입니다.|  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;복제 테이블](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
