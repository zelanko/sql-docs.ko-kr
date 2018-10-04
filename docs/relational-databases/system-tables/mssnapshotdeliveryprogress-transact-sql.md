---
title: MSsnapshotdeliveryprogress (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
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
manager: craigg
ms.openlocfilehash: 59be6e8f6faaded5ffb78f2e7dd8fecb4371ed52
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47720951"
---
# <a name="mssnapshotdeliveryprogress-transact-sql"></a>MSsnapshotdeliveryprogress(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  합니다 **MSsnapshotdeliveryprogress** 테이블 성공적으로 배달 된 구독자에 스냅숏을 적용 되 면 파일 추적을 사용 합니다. 이 데이터는 병합 에이전트가 세션 중에 파일을 모두 배달하지 못한 경우 파일 배달을 다시 시작하는 데 사용되어 다음에 병합 에이전트가 실행될 때 같은 파일을 다시 배달하지 않도록 합니다. 이 테이블은 구독 데이터베이스의 구독자에 저장됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**session_token**|**nvarchar(260)**|파일을 성공적으로 배달한 스냅숏 폴더의 경로를 식별합니다. 문자열 매개 변수가 있는 필터를 사용 하는 게시에 대 한 **dynsnap** 값에 추가 됩니다.|  
|**progress_token_hash**|**int**|생성 된 해시 값의 값을 기반으로 *progress_token* 사용 되는 대 한 조회 효율성을 높이 지정 된 *progress_token* 값입니다.|  
|**progress_token**|**nvarchar(500)**|성공적으로 배달된 파일을 식별합니다. 값은 파일 이름과 경로의 조합입니다.|  
|**progress_timestamp**|**datetime**|합니다 **날짜/시간** 스냅숏 파일을 성공적으로 배달 된 시기를 나타내는 값입니다.|  
  
## <a name="see-also"></a>관련 항목  
 [복제 테이블 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
