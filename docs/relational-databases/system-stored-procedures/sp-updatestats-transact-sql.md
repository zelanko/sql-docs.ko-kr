---
title: sp_updatestats (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/25/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_updatestats_TSQL
- sp_updatestats
dev_langs:
- TSQL
helpviewer_keywords:
- sp_updatestats
ms.assetid: 01184651-6e61-45d9-a502-366fecca0ee4
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: c00bdd453bc4d1bf467b37aca3639eb43f55e022
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68085787"
---
# <a name="spupdatestats-transact-sql"></a>sp_updatestats(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

실행 `UPDATE STATISTICS` 현재 데이터베이스의 모든 사용자 정의 및 내부 테이블에 대 한 합니다.  
  
에 대 한 자세한 내용은 `UPDATE STATISTICS`를 참조 하세요 [UPDATE STATISTICS &#40;TRANSACT-SQL&#41;](../../t-sql/statements/update-statistics-transact-sql.md)합니다. 통계에 대한 자세한 내용은 [통계](../../relational-databases/statistics/statistics.md)를 참조하세요.  
    
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
sp_updatestats [ [ @resample = ] 'resample']  
```  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="arguments"></a>인수  
`[ @resample = ] 'resample'` 지정 **sp_updatestats** RESAMPLE 옵션을 사용할지는 [UPDATE STATISTICS](../../t-sql/statements/update-statistics-transact-sql.md) 문입니다. 하는 경우 **'resample'** 지정 하지 않으면 **sp_updatestats** 기본 샘플링을 사용 하 여 통계를 업데이트 합니다. **다시** 는 **varchar(8)** 번호의 기본값이  
  
## <a name="remarks"></a>설명  
 **sp_updatestats** 실행 `UPDATE STATISTICS`를 지정 하 여는 `ALL` 키워드, 데이터베이스의 모든 사용자 정의 및 내부 테이블입니다. sp_updatestats는 진행률을 나타내는 메시지를 표시 합니다. 업데이트가 완료되면 모든 테이블에 대해 통계가 업데이트되었다고 보고합니다.  
  
sp_updatestats는 비활성화된 비클러스터형 인덱스에 대한 통계는 업데이트하며 비활성화된 클러스터형 인덱스에 대한 통계는 업데이트하지 않습니다.  
  
디스크 기반 테이블에 대 한 **sp_updatestats** 기반으로 하는 통계를 업데이트 합니다 **modification_counter** 의 정보를 **sys.dm_db_stats_properties** 카탈로그 뷰를 하나 이상의 행에 수정한 통계를 업데이트 합니다. 메모리 최적화 테이블에 대 한 통계를 실행할 때 항상 업데이트 됩니다 **sp_updatestats**합니다. 따라서 실행 하지 마십시오 **sp_updatestats** 두 개 필요 합니다.  
  
**sp_updatestats** 저장 프로시저나 기타 컴파일된 코드의 재컴파일을 트리거할 수 있습니다. 그러나 **sp_updatestats** 하나 쿼리 계획은 참조 되는 테이블 및 인덱스에만 재컴파일이 발생 하지 않을 수 있습니다. 이러한 경우에는 통계가 업데이트되었더라도 재컴파일이 필요하지 않습니다.  
  
데이터베이스 호환성 수준이 90으로 실행 미만인 **sp_updatestats** 특정 통계에 대 한 최신 NORECOMPUTE 설정이 유지 되지 않습니다. Sp_updatestats는 호환성 수준이 90 이상인 데이터베이스에 대 한 특정 통계에 대 한 최신 NORECOMPUTE 옵션을 유지 하 고 있습니다. 통계 업데이트를 비활성화하고 다시 활성화하는 방법은 [통계](../../relational-databases/statistics/statistics.md)를 참조하세요.  
  
## <a name="permissions"></a>사용 권한  
 멤버 자격에 필요 하면 **sysadmin** 고정 서버 역할 또는 데이터베이스에 대 한 소유권 (**dbo**).  

## <a name="examples"></a>예  
다음 예에서는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스의 테이블에 대한 통계를 업데이트합니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
EXEC sp_updatestats;   
```  

## <a name="automatic-index-and-statistics-management"></a>자동 인덱스 및 통계 관리
[Adaptive Index Defrag](https://github.com/Microsoft/tigertoolbox/tree/master/AdaptiveIndexDefrag)와 같은 솔루션을 사용하여 하나 이상의 데이터베이스에 대한 인덱스 조각 모음 및 통계 업데이트를 자동으로 관리합니다. 이 절차는 다른 매개 변수 사이에서 조각화 수준에 따라 인덱스를 다시 작성하거나 다시 구성할지 여부를 자동으로 선택하고 통계를 선형 임계값으로 업데이트합니다.

## <a name="see-also"></a>관련 항목  
 [ALTER DATABASE SET 옵션&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
 [CREATE STATISTICS&#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md)   
 [DBCC SHOW_STATISTICS&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)   
 [DROP STATISTICS&#40;Transact-SQL&#41;](../../t-sql/statements/drop-statistics-transact-sql.md)   
 [sp_autostats&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-autostats-transact-sql.md)   
 [sp_createstats &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-createstats-transact-sql.md)   
 [UPDATE STATISTICS&#40;Transact-SQL&#41;](../../t-sql/statements/update-statistics-transact-sql.md)   
 [시스템 저장 프로시저](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
 
