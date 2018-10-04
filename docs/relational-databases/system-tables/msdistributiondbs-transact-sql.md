---
title: MSdistributiondbs (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- MSdistributiondbs_TSQL
- MSdistributiondbs
dev_langs:
- TSQL
helpviewer_keywords:
- MSdistributiondbs system table
ms.assetid: d7ffa9df-bf1d-41b8-837e-b762c17c2764
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b7b37c25c599e3c823fc319a5ed4ea83e1aae3f6
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47848291"
---
# <a name="msdistributiondbs-transact-sql"></a>MSdistributiondbs(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  합니다 **MSdistributiondbs** 테이블은 로컬 배포자에 정의 된 각 배포 데이터베이스에 대해 하나의 행을 포함 합니다. 이 테이블에 저장 되는 **msdb** 데이터베이스입니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|배포 데이터베이스의 이름입니다.|  
|**min_distretention**|**int**|트랜잭션을 삭제하기 전의 최소 보존 기간(시)입니다.|  
|**max_distretention**|**int**|트랜잭션을 삭제하기 전의 최대 보존 기간(시)입니다.|  
|**history_retention**|**int**|기록을 보존할 시간입니다.|  
  
## <a name="see-also"></a>관련 항목  
 [복제 테이블 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
