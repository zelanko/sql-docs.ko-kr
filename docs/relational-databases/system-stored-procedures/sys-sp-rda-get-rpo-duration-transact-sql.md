---
title: sys.sp_rda_get_rpo_duration (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-stretch
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.sp_rda_get_rpo_duration
- sys.sp_rda_get_rpo_duration_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_rda_get_rpo_duration stored procedure
ms.assetid: 35882067-3072-47ff-9024-ca453c0f49a7
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a2a8877f7e101241399db2132b02d6e5a41b31b5
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/03/2018
---
# <a name="syssprdagetrpoduration-transact-sql"></a>sys.sp_rda_get_rpo_duration (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  되도록 원격 Azure 데이터베이스의 전체 복원을 지정 시간 복원에 필요한 경우에 준비 테이블에 SQL Server 유지 하는 마이그레이션된 데이터의 시간 수를 가져옵니다. 
  
  자세한 내용은 참조 하십시오. [스트레치 데이터베이스는 마이그레이션된 행을 일시적으로 유지 하 여 Azure 데이터에 대 한 데이터 손실의 위험을 줄이기](../../sql-server/stretch-database/backup-stretch-enabled-databases-stretch-database.md#stretchRPO)합니다.  
    
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)    
    
## <a name="syntax"></a>구문    
    
```    
    
sp_rda_get_rpo_duration @durationinhours output    
    
```    
    
## <a name="output-parameter"></a>출력 매개 변수    
 *@durationinhours*    
  시간 수입니다 (null이 아닌 정수 값) 현재 스트레치 사용 데이터베이스에 대 한 SQL Server 유지 하는 마이그레이션된 데이터의 합니다.    
    
## <a name="permissions"></a>Permissions    
 Db_owner 권한이 필요합니다.    
    
## <a name="remarks"></a>주의    
 실행 하 여 값을 변경 [sys.sp_rda_set_rpo_duration &#40; Transact SQL &#41; ](../../relational-databases/system-stored-procedures/sys-sp-rda-set-rpo-duration-transact-sql.md).    
    
## <a name="see-also"></a>관련 항목:    
 [sys.sp_rda_set_rpo_duration &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sys-sp-rda-set-rpo-duration-transact-sql.md)     
 [스트레치 사용 데이터베이스 복원 (스트레치 데이터베이스)](../../sql-server/stretch-database/restore-stretch-enabled-databases-stretch-database.md)    
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)    
    
  
