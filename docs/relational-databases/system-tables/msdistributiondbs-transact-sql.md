---
title: Msdb..msdistributiondbs (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSdistributiondbs_TSQL
- MSdistributiondbs
dev_langs:
- TSQL
helpviewer_keywords:
- MSdistributiondbs system table
ms.assetid: d7ffa9df-bf1d-41b8-837e-b762c17c2764
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 30eeddfa1adaa75d4f4b074af99d1ed8ad6ed238
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82812977"
---
# <a name="msdistributiondbs-transact-sql"></a>MSdistributiondbs(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **Msdb..msdistributiondbs** 테이블은 로컬 배포자에 정의 된 각 배포 데이터베이스에 대해 하나의 행을 포함 합니다. 이 테이블은 **msdb** 데이터베이스에 저장 됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|배포 데이터베이스의 이름입니다.|  
|**min_distretention**|**int**|트랜잭션을 삭제하기 전의 최소 보존 기간(시)입니다.|  
|**max_distretention**|**int**|트랜잭션을 삭제하기 전의 최대 보존 기간(시)입니다.|  
|**history_retention**|**int**|기록을 보존할 시간입니다.|  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;복제 테이블](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
