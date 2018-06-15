---
title: sp_updatestats (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/25/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_updatestats_TSQL
- sp_updatestats
dev_langs:
- TSQL
helpviewer_keywords:
- sp_updatestats
ms.assetid: 01184651-6e61-45d9-a502-366fecca0ee4
caps.latest.revision: 45
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 895c3fd65ac6cad3a0ce67dee54cfe8cf1070ea4
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
ms.locfileid: "33259473"
---
# <a name="spupdatestats-transact-sql"></a>sp_updatestats(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  현재 데이터베이스의 모든 사용자 정의 및 내부 테이블에 대해 UPDATE STATISTICS를 실행합니다.  
  
 UPDATE STATISTICS에 대 한 자세한 내용은 참조 [UPDATE STATISTICS &#40;TRANSACT-SQL&#41;](../../t-sql/statements/update-statistics-transact-sql.md)합니다. 통계에 대 한 자세한 내용은 참조 [통계](../../relational-databases/statistics/statistics.md)합니다.  
    
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_updatestats [ [ @resample = ] 'resample']  
```  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="arguments"></a>인수  
 [ **@resample** =] **'resample'**  
 지정 하는 **sp_updatestats** RESAMPLE 옵션을 사용 합니다는 [UPDATE STATISTICS](../../t-sql/statements/update-statistics-transact-sql.md) 문. 경우 **'resample'** 를 지정 하지 않으면 **sp_updatestats** 기본 샘플링을 사용 하 여 통계를 업데이트 합니다. **resample** 은 **varchar(8)** 이며 기본값은 no입니다.  
  
## <a name="remarks"></a>주의  
 **sp_updatestats** 데이터베이스의 모든 사용자 정의 및 내부 테이블에는 ALL 키워드를 지정 하 여 UPDATE STATISTICS를 실행 합니다. sp_updatestats는 진행률을 나타내는 메시지를 표시 합니다. 업데이트가 완료되면 모든 테이블에 대해 통계가 업데이트되었다고 보고합니다.  
  
 sp_updatestats는 비활성화된 비클러스터형 인덱스에 대한 통계는 업데이트하며 비활성화된 클러스터형 인덱스에 대한 통계는 업데이트하지 않습니다.  
  
 디스크 기반 테이블에 대 한 **sp_updatestats** 기준으로 통계를 업데이트는 **modification_counter** 의 정보는 **sys.dm_db_stats_properties** 카탈로그 뷰를 하나 이상의 행에 수정 된 통계를 업데이트 합니다. 메모리 액세스에 최적화 된 테이블에 대 한 통계를 실행할 때 항상 업데이트 됩니다 **sp_updatestats**합니다. 따라서 실행 하지 않도록 **sp_updatestats** 필요 이상.  
  
 **sp_updatestats** 저장 프로시저나 기타 컴파일된 코드의 재컴파일을 트리거할 수 있습니다. 그러나 **sp_updatestats** 하나만 쿼리 계획이 하나 이면 참조 된 테이블 및 인덱스에 대 한 가능한 재컴파일이 발생 하지 수도 있습니다. 이러한 경우에는 통계가 업데이트되었더라도 재컴파일이 필요하지 않습니다.  
  
 호환성 수준이 90으로 실행 미만인 데이터베이스에 대 한 **sp_updatestats** 특정 통계에 대 한 최신 NORECOMPUTE 설정이 유지 되지 않습니다. 호환성 수준이 90 이상인 데이터베이스에 대해 sp_updatestats는 특정 통계에 대 한 최신 norecompute 유지. 통계 업데이트를 비활성화하고 다시 활성화하는 방법은 [통계](../../relational-databases/statistics/statistics.md)를 참조하세요.  
  
## <a name="permissions"></a>Permissions  
 멤버 자격이 필요는 **sysadmin** 고정 서버 역할 또는 데이터베이스의 소유권 (**dbo**).  
  
## <a name="examples"></a>예  
 다음 예에서는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스의 테이블에 대한 통계를 업데이트합니다.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_updatestats;   
```  
  
## <a name="see-also"></a>관련 항목:  
 [ALTER DATABASE SET 옵션&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
 [CREATE STATISTICS&#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md)   
 [DBCC SHOW_STATISTICS&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)   
 [DROP STATISTICS&#40;Transact-SQL&#41;](../../t-sql/statements/drop-statistics-transact-sql.md)   
 [sp_autostats&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-autostats-transact-sql.md)   
 [sp_createstats &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-createstats-transact-sql.md)   
 [UPDATE STATISTICS&#40;Transact-SQL&#41;](../../t-sql/statements/update-statistics-transact-sql.md)   
 [시스템 저장 프로시저](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
