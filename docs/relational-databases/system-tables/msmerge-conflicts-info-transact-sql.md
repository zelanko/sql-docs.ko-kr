---
title: MSmerge_conflicts_info (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: ''
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
- MSmerge_conflicts_info_TSQL
- MSmerge_conflicts_info
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_conflicts_info system table
ms.assetid: 6b76ae96-737a-4000-a6b6-fcc8772c2af4
caps.latest.revision: 19
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 85ce4ab68f0ae49425b72b1e0d7601a7d0ff5f60
ms.sourcegitcommit: d6b1695c8cbc70279b7d85ec4dfb66a4271cdb10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/10/2018
---
# <a name="msmergeconflictsinfo-transact-sql"></a>MSmerge_conflicts_info(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSmerge_conflicts_info** 테이블은 병합 게시에 구독을 동기화 할 때 발생 하는 충돌을 추적 합니다. 충돌에서 패한 행 데이터에 저장 됩니다는 [MSmerge_conflict_publication_article](../../relational-databases/system-tables/msmerge-conflict-publication-article-transact-sql.md) 충돌이 발생 하는 문서에 대 한 테이블입니다. 이 테이블은 게시 데이터베이스의 게시자와 구독 데이터베이스의 구독자에 저장됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**tablenick**|**int**|게시된 테이블의 애칭입니다.|  
|**rowguid**|**uniqueidentifier**|충돌 행의 식별자입니다.|  
|**origin_datasource**|**nvarchar(255)**|충돌을 일으키는 변경이 시작된 데이터베이스의 이름입니다.|  
|**conflict_type**|**int**|발생한 충돌의 유형이며 다음 중 하나일 수 있습니다.<br /><br /> **1** = 업데이트 충돌: 행 수준에서 충돌 검색 됩니다.<br /><br /> **2** = 열 업데이트 충돌: 충돌이 열 수준에서 검색 합니다.<br /><br /> **3** = 업데이트 / 충돌 시 삭제: 삭제가 충돌에서 우선 적용 됩니다.<br /><br /> **4** = 업데이트 Wins 삭제 충돌: 충돌에서 패한 삭제 된 rowguid가이 테이블에 기록 됩니다.<br /><br /> **5** = 업로드 삽입 실패: 게시자에 구독자에서 삽입을 적용할 수 없습니다.<br /><br /> **6** = 다운로드 삽입 실패: 구독자에서 게시자에서의 삽입을 적용할 수 없습니다.<br /><br /> **7** = 업로드 삭제 실패: 구독자에서의 삭제를 게시자로 업로드할 수 없습니다.<br /><br /> **8** = 다운로드 삭제 실패: 게시자에서의 삭제를 구독자로 다운로드할 수 없습니다.<br /><br /> **9** = 업로드 업데이트 실패: 게시자에 구독자에서 업데이트를 적용할 수 없습니다.<br /><br /> **10** = 다운로드 업데이트 실패: 게시자에서 업데이트를 구독자에 적용할 수 없습니다.<br /><br /> **11** = 해결 방법<br /><br /> **12** = 논리 레코드 업데이트 Wins 삭제: 삭제 충돌에서 패한 된 논리 레코드가이 테이블에 기록 됩니다.<br /><br /> **13** = 논리 레코드 충돌 삽입 업데이트: 업데이트와 충돌 하는 논리적 레코드를 삽입 합니다.<br /><br /> **14** = 논리 레코드 삭제 Wins 업데이트 충돌: 업데이트 충돌에서 패한 된 논리 레코드가이 테이블에 기록 됩니다.|  
|**reason_code**|**int**|상황에 따른 오류 코드입니다. 업데이트 / 업데이트 및 업데이트-삭제 충돌의 경우이 열에 대해 사용 되는 값과 동일은 **conflict_type**합니다. 그러나 실패한 변경 충돌의 경우에는 병합 에이전트에서 변경 내용을 적용하지 못하게 하는 오류가 이유 코드에 사용됩니다. 예를 들어 병합 에이전트는 기본 키 위반으로 인해 구독자에서의 삽입을 적용할 수 없습니다, 기록는 **conflict_type** 6 ("다운로드 삽입 실패")와 **reason_code** 되는 2627는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기본 키 위반에 대 한 내부 오류 메시지: "%ls 제약 조건 위반 ' %. * l s. 개체에 중복 키를 삽입할 수 없습니다 ' %. \*l s. "|  
|**reason_text**|**nvarchar(720)**|상황에 따른 오류 설명입니다.|  
|**pubid**|**uniqueidentifier**|게시의 식별자입니다.|  
|**MSrepl_create_time**|**datetime**|충돌 발생 시각입니다.|  
|**origin_datasource_id**|**uniqueidentifier**|충돌을 일으키는 변경이 시작된 데이터베이스의 식별자입니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [복제 테이블 &#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
