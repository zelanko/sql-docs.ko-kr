---
title: sys. sp_rda_set_rpo_duration (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: language-reference
f1_keywords:
- sys.sp_rda_set_rpo_duration
- sys.sp_rda_set_rpo_duration_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_rda_set_rpo_duration stored procedure
ms.assetid: 95c80c5b-9252-4612-9ea7-544c48834fd2
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 3588f12006de3f7a9e79f6743ae8dffbe01f42c2
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82807944"
---
# <a name="syssp_rda_set_rpo_duration-transact-sql"></a>sys. sp_rda_set_rpo_duration (Transact-sql)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  지정 시간 복원이 필요한 경우 원격 Azure 데이터베이스를 전체 복원할 수 있도록 SQL Server 준비 테이블에 유지 되는 마이그레이션된 데이터의 시간을 설정 합니다.    
    
 자세한 내용은 [마이그레이션된 행을 일시적으로 유지 하 여 Azure 데이터에 대 한 데이터 손실의 위험을 줄이기 Stretch Database](../../sql-server/stretch-database/backup-stretch-enabled-databases-stretch-database.md#stretchRPO)를 참조 하세요.  
   
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)    
     
## <a name="syntax"></a>구문    
    
```    
    
sp_rda_set_rpo_duration [ @duration_hrs = ] duration_hrs    
    
```    
    
## <a name="arguments"></a>인수    
 [ @duration_hrs =] *duration_hrs*    
 현재 스트레치 사용 데이터베이스에 대해 유지 하려는 마이그레이션된 SQL Server 데이터의 시간 (null이 아닌 정수 값) 수입니다. 기본값 및 최소값은 8 시간입니다.    
 
 > [!NOTE]
 > 값이 높을수록 SQL Server에 더 많은 저장 공간이 필요 합니다.
    
## <a name="permissions"></a>권한    
 Db_owner 권한이 필요 합니다.    
    
## <a name="remarks"></a>설명    
 [Sp_rda_get_rpo_duration &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-rda-get-rpo-duration-transact-sql.md)를 실행 하 여 현재 값을 가져옵니다.    
    
## <a name="see-also"></a>참고 항목    
 [sp_rda_get_rpo_duration &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-rda-get-rpo-duration-transact-sql.md)     
 [스트레치 사용 데이터베이스 복원 (Stretch Database)](../../sql-server/stretch-database/restore-stretch-enabled-databases-stretch-database.md)     
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)    
    
  
