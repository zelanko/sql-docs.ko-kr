---
title: sp_updatestats (Transact SQL) | Microsoft 문서
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
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: cd4eada4db6af75ad794efdba231407b23f79354
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39560583"
---
# <a name="spupdatestats-transact-sql"></a>sp_updatestats(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  현재 데이터베이스의 모든 사용자 정의 및 내부 테이블에 대해 UPDATE STATISTICS를 실행합니다.  
  
 통계 업데이트에 대 한 자세한 내용은 참조 [UPDATE STATISTICS &#40;Transact SQL&#41;](../../t-sql/statements/update-statistics-transact-sql.md). 통계에 대한 자세한 내용은 [통계](../../relational-databases/statistics/statistics.md)를 참조하세요.  
    
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_updatestats [ [ @resample = ] 'resample']  
```  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="arguments"></a>인수  
 [ **@resample** =] **'다시'**  
 지정 하는 **sp_updatestats** 의 재샘플 옵션을 사용 합니다에서 [UPDATE STATISTICS](../../t-sql/statements/update-statistics-transact-sql.md) 문. 경우 **'다시'** 을 지정 하지 않으면 **sp_updatestats** 기본 샘플링을 사용 하 여 통계를 업데이트 합니다. **다시** 는 **varchar(8)** 번호의 기본값이  
  
## <a name="remarks"></a>Remarks  
 **sp_updatestats** 데이터베이스의 모든 사용자 정의 및 내부 테이블에 ALL 키워드를 지정 하 여 UPDATE STATISTICS를 실행 합니다. sp_updatestats는 진행률을 나타내는 메시지를 표시 합니다. 업데이트가 완료되면 모든 테이블에 대해 통계가 업데이트되었다고 보고합니다.  
  
 sp_updatestats는 비활성화된 비클러스터형 인덱스에 대한 통계는 업데이트하며 비활성화된 클러스터형 인덱스에 대한 통계는 업데이트하지 않습니다.  
  
 디스크 기반 테이블의 경우 **sp_updatestats** 에 근거 하 여 통계를 업데이트는 **modification_counter** 정보는 **sys.dm_db_stats_properties** 카탈로그 보기 하나 이상의 행에 수정 된 통계를 업데이트 합니다. 메모리 최적화 된 테이블에 대 한 통계를 항상 실행 하는 경우 업데이트 **sp_updatestats**. 따라서 실행 하지 않도록 **sp_updatestats** 이상이 필요 합니다.  
  
 **sp_updatestats** 를 재컴파일 저장된 프로시저 또는 다른 컴파일된 코드를 트리거할 수 있습니다. 그러나 **sp_updatestats** 만 참조 하는 테이블 및 인덱스에 대 한 하나의 쿼리 계획이 불가능 한 재컴파일을 발생할 수 있습니다. 이러한 경우에는 통계가 업데이트되었더라도 재컴파일이 필요하지 않습니다.  
  
 데이터베이스의 호환성 수준이 90 이면 실행 아래 **sp_updatestats** 특정 통계에 대 한 최신 NORECOMPUTE 설정을 유지 하지 않습니다. 데이터베이스 호환성 수준이 90 이상이 sp_updatestats 특정 통계에 대 한 최신 NORECOMPUTE 옵션을 유지 않습니다. 통계 업데이트를 비활성화하고 다시 활성화하는 방법은 [통계](../../relational-databases/statistics/statistics.md)를 참조하세요.  
  
## <a name="permissions"></a>사용 권한  
 멤버 자격에 필요 하면 **sysadmin** 고정 서버 역할 또는 데이터베이스에 대 한 소유권 (**dbo**).  
  
## <a name="examples"></a>예  
 다음 예에서는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스의 테이블에 대한 통계를 업데이트합니다.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_updatestats;   
```  
  
## <a name="see-also"></a>관련 항목  
 [ALTER DATABASE SET 옵션&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
 [CREATE STATISTICS&#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md)   
 [DBCC SHOW_STATISTICS&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)   
 [DROP STATISTICS&#40;Transact-SQL&#41;](../../t-sql/statements/drop-statistics-transact-sql.md)   
 [sp_autostats&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-autostats-transact-sql.md)   
 [sp_createstats &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-createstats-transact-sql.md)   
 [UPDATE STATISTICS&#40;Transact-SQL&#41;](../../t-sql/statements/update-statistics-transact-sql.md)   
 [시스템 저장 프로시저](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
