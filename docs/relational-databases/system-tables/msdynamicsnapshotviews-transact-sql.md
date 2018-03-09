---
title: MSdynamicsnapshotviews (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- MSdynamicsnapshotviews_TSQL
- MSdynamicsnapshotviews
dev_langs: TSQL
helpviewer_keywords: MSdynamicsnapshotviews system table
ms.assetid: 4fc1822a-5d6e-4034-a2e2-363210232d3b
caps.latest.revision: "26"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7625cd2c9316c4abc7f72b1aacbb8d8c1dd650ae
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="msdynamicsnapshotviews-transact-sql"></a>MSdynamicsnapshotviews(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSdynamicsnapshotviews** 스냅숏 에이전트에 의해 만들어진 모든 필터링 된 데이터 스냅숏 뷰를 추적 하 고 SQL Server 에이전트의 비정상적인 종료 시 뷰를 정리 하기 위해 시스템에서 사용 하는 테이블 또는 스냅숏 에이전트입니다. 이 테이블은 게시 및 구독 데이터베이스에 저장됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**dynamic_snapshot_view_name**|**sysname**|필터링된 임시 데이터 스냅숏 뷰의 이름입니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [복제 테이블&#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
