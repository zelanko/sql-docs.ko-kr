---
title: MSmerge_conflicts_info (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- MSmerge_conflicts_info_TSQL
- MSmerge_conflicts_info
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_conflicts_info system table
ms.assetid: 6b76ae96-737a-4000-a6b6-fcc8772c2af4
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 34dd7496d514db14399134eb7ffe222af7251f95
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47737733"
---
# <a name="msmergeconflictsinfo-transact-sql"></a>MSmerge_conflicts_info(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  합니다 **MSmerge_conflicts_info** 테이블은 병합 게시에 대 한 구독을 동기화 할 때 발생 하는 충돌을 추적 합니다. 충돌 패한 행 데이터에 저장 되는 [MSmerge_conflict_publication_article](../../relational-databases/system-tables/msmerge-conflict-publication-article-transact-sql.md) 충돌이 발생 한 아티클에 대 한 테이블입니다. 이 테이블은 게시 데이터베이스의 게시자와 구독 데이터베이스의 구독자에 저장됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**tablenick**|**int**|게시된 테이블의 애칭입니다.|  
|**rowguid**|**uniqueidentifier**|충돌 행의 식별자입니다.|  
|**origin_datasource**|**nvarchar(255)**|충돌을 일으키는 변경이 시작된 데이터베이스의 이름입니다.|  
|**conflict_type**|**int**|발생한 충돌의 유형이며 다음 중 하나일 수 있습니다.<br /><br /> **1** = 업데이트 충돌: 행 수준에서 충돌이 검색 됩니다.<br /><br /> **2** = 열 업데이트 충돌: 충돌이 열 수준에서 검색 합니다.<br /><br /> **3** = 업데이트 / 충돌 시 삭제: 삭제 충돌에서 승리 합니다.<br /><br /> **4** = 업데이트 Wins 삭제 충돌: 삭제 충돌이 손실 된 rowguid가이 테이블에 기록 됩니다.<br /><br /> **5** = 업로드 삽입 실패: 게시자의 구독자에서의 삽입을 적용할 수 없습니다.<br /><br /> **6** = 다운로드 삽입 실패: 구독자에서 게시자에서의 삽입을 적용할 수 없습니다.<br /><br /> **7** = 업로드 삭제 실패: 구독자에서의 삭제를 게시자로 업로드할 수 없습니다.<br /><br /> **8** = 다운로드 삭제 실패: 게시자에서의 삭제를 구독자로 다운로드할 수 없습니다.<br /><br /> **9** = 업로드 업데이트 실패: 게시자의 구독자에서 업데이트를 적용할 수 없습니다.<br /><br /> **10** = 다운로드 업데이트 실패: 구독자에 게시자에서 업데이트를 적용할 수 없습니다.<br /><br /> **11** = 해결 방법<br /><br /> **12** = 논리 레코드 업데이트 Wins 삭제: 삭제 충돌이 손실 된 논리 레코드가이 테이블에 기록 됩니다.<br /><br /> **13** = 논리 레코드 충돌 삽입 업데이트: 업데이트를 사용 하 여 충돌을 논리적 레코드를 삽입 합니다.<br /><br /> **14** = 논리 레코드 삭제 Wins 업데이트 충돌: 업데이트 충돌이 손실 된 논리 레코드가이 테이블에 기록 됩니다.|  
|**reason_code**|**int**|상황에 따른 오류 코드입니다. 업데이트 / 업데이트 및 업데이트-삭제 충돌이 있을 경우이 열에 사용 된 값 동일 합니다 **conflict_type**합니다. 그러나 실패한 변경 충돌의 경우에는 병합 에이전트에서 변경 내용을 적용하지 못하게 하는 오류가 이유 코드에 사용됩니다. 예를 들어 병합 에이전트는 기본 키 위반으로 인해 구독자에서 삽입을 적용할 수 없습니다, 하는 경우 기록를 **conflict_type** 6 ("다운로드 삽입 실패") 및 **reason_code** 는 2627의의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기본 키 위반에 대 한 내부 오류 메시지: "%ls 제약 조건 위반 ' %. * l s입니다. 개체에 중복 키를 삽입할 수 없습니다. ' %. \*l s. "|  
|**reason_text**|**nvarchar(720)**|상황에 따른 오류 설명입니다.|  
|**pubid**|**uniqueidentifier**|게시의 식별자입니다.|  
|**MSrepl_create_time**|**datetime**|충돌 발생 시각입니다.|  
|**origin_datasource_id**|**uniqueidentifier**|충돌을 일으키는 변경이 시작된 데이터베이스의 식별자입니다.|  
  
## <a name="see-also"></a>관련 항목  
 [복제 테이블 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
