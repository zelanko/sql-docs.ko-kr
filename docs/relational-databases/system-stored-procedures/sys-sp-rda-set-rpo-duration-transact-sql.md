---
title: sys.sp_rda_set_rpo_duration (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-stretch
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.sp_rda_set_rpo_duration
- sys.sp_rda_set_rpo_duration_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_rda_set_rpo_duration stored procedure
ms.assetid: 95c80c5b-9252-4612-9ea7-544c48834fd2
caps.latest.revision: 16
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a28b57e46353fbf778be0eac72ca79992292e8a1
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="syssprdasetrpoduration-transact-sql"></a>sys.sp_rda_set_rpo_duration (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  SQL Server 유지 하는 마이그레이션된 데이터의 시간 수 있도록 하려면 원격 Azure 데이터베이스의 전체 복원을 지정 시간 복원에 필요한 경우에 준비 테이블에 설정 합니다.    
    
 자세한 내용은 참조 하십시오. [스트레치 데이터베이스는 마이그레이션된 행을 일시적으로 유지 하 여 Azure 데이터에 대 한 데이터 손실의 위험을 줄이기](../../sql-server/stretch-database/backup-stretch-enabled-databases-stretch-database.md#stretchRPO)합니다.  
   
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)    
     
## <a name="syntax"></a>구문    
    
```    
    
sp_rda_set_rpo_duration [ @duration_hrs = ] duration_hrs    
    
```    
    
## <a name="arguments"></a>인수    
 [ @duration_hrs =] *duration_hrs*    
 시간 수입니다 (null이 아닌 정수 값)를 유지 하려면 SQL Server는 현재 스트레치 사용 데이터베이스에 대 한 마이그레이션된 데이터의 합니다. 기본값 및 최소값은 8 시간입니다.    
 
 > [!NOTE]
 > 값이 높을수록 SQL Server에서 더 많은 저장 공간이 필요 합니다.
    
## <a name="permissions"></a>Permissions    
 Db_owner 권한이 필요합니다.    
    
## <a name="remarks"></a>주의    
 실행 하 여 현재 값을 가져올 [sys.sp_rda_get_rpo_duration &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-rda-get-rpo-duration-transact-sql.md)합니다.    
    
## <a name="see-also"></a>관련 항목:    
 [sys.sp_rda_get_rpo_duration &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-rda-get-rpo-duration-transact-sql.md)     
 [스트레치 사용 데이터베이스 복원 (스트레치 데이터베이스)](../../sql-server/stretch-database/restore-stretch-enabled-databases-stretch-database.md)     
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)    
    
  
