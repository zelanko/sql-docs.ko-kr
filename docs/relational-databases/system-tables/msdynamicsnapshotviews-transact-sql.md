---
title: MSdynamicsnapshotviews (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSdynamicsnapshotviews_TSQL
- MSdynamicsnapshotviews
dev_langs:
- TSQL
helpviewer_keywords:
- MSdynamicsnapshotviews system table
ms.assetid: 4fc1822a-5d6e-4034-a2e2-363210232d3b
author: stevestein
ms.author: sstein
ms.openlocfilehash: 8de7dd1571f7b9082144e97c8b35d9a39d6cabe8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67907318"
---
# <a name="msdynamicsnapshotviews-transact-sql"></a>MSdynamicsnapshotviews(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  합니다 **MSdynamicsnapshotviews** 스냅숏 에이전트에 의해 만들어진 모든 필터링 된 데이터 스냅숏 뷰를 추적 하 고는 시스템에서 SQL Server 에이전트의 비정상적인 종료 시 뷰를 정리 하는 테이블 또는 스냅숏 에이전트입니다. 이 테이블은 게시 및 구독 데이터베이스에 저장됩니다.  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|**dynamic_snapshot_view_name**|**sysname**|필터링된 임시 데이터 스냅샷 뷰의 이름입니다.|  
  
## <a name="see-also"></a>관련 항목  
 [복제 테이블&#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
