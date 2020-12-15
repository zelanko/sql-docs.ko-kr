---
description: sp_updatestats(Transact-SQL)
title: sp_updatestats (Transact-sql) | Microsoft Docs
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
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f976f9be51d688833a09e5faaae42b8864ecc274
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97482384"
---
# <a name="sp_updatestats-transact-sql"></a>sp_updatestats(Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

`UPDATE STATISTICS`현재 데이터베이스에 있는 모든 사용자 정의 테이블 및 내부 테이블에 대해 실행 됩니다.  
  
에 대 한 자세한 내용은 `UPDATE STATISTICS` [UPDATE STATISTICS &#40;transact-sql&#41;](../../t-sql/statements/update-statistics-transact-sql.md)를 참조 하세요. 통계에 대한 자세한 내용은 [통계](../../relational-databases/statistics/statistics.md)를 참조하세요.  
    
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
sp_updatestats [ [ @resample = ] 'resample']  
```  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="arguments"></a>인수  
`[ @resample = ] 'resample'`**Sp_updatestats** [UPDATE STATISTICS](../../t-sql/statements/update-statistics-transact-sql.md) 문의 다시 샘플링 옵션을 사용 하도록 지정 합니다. ' 다시 지정 **'** 을 지정 하지 않으면 **sp_updatestats** 기본 샘플링을 사용 하 여 통계를 업데이트 합니다. 다시 **샘플링** 은 **varchar (8)** 이며 기본값은 NO입니다.  
  
## <a name="remarks"></a>설명  
 **sp_updatestats** `UPDATE STATISTICS` 은 `ALL` 데이터베이스의 모든 사용자 정의 및 내부 테이블에 대해 키워드를 지정 하 여 실행 합니다. sp_updatestats 진행률을 나타내는 메시지를 표시 합니다. 업데이트가 완료되면 모든 테이블에 대해 통계가 업데이트되었다고 보고합니다.  
  
**sp_updatestats** 는 비활성화 된 비클러스터형 인덱스에 대 한 통계를 업데이트 하 고 비활성화 된 클러스터형 인덱스에 대 한 통계를 업데이트 하지 않습니다.  
  
디스크 기반 테이블의 경우 **sp_updatestats** 는 **sys.dm_db_stats_properties** 카탈로그 뷰의 **modification_counter** 정보에 따라 통계를 업데이트 하 여 하나 이상의 행이 수정 된 통계를 업데이트 합니다. **Sp_updatestats** 를 실행 하면 메모리 최적화 테이블에 대 한 통계가 항상 업데이트 됩니다. 따라서 **sp_updatestats** 필요 이상으로 실행 되지 않습니다.  
  
**sp_updatestats** 저장 프로시저나 다른 컴파일된 코드를 다시 컴파일할 수 있습니다. 그러나 참조 된 테이블과 인덱스에 대 한 쿼리 계획을 하나만 사용할 수 있는 경우에는 **sp_updatestats** 에서 재컴파일을 발생 시 키 지 않을 수 있습니다. 이러한 경우에는 통계가 업데이트되었더라도 재컴파일이 필요하지 않습니다.  
  
호환성 수준이 90 미만인 데이터베이스의 경우 **sp_updatestats** 를 실행 해도 특정 통계에 대 한 최신 NORECOMPUTE 설정이 유지 되지 않습니다. 호환성 수준이 90 이상인 데이터베이스의 경우 sp_updatestats는 특정 통계에 대 한 최신 NORECOMPUTE 옵션을 유지 합니다. 통계 업데이트를 비활성화하고 다시 활성화하는 방법은 [통계](../../relational-databases/statistics/statistics.md)를 참조하세요.  
  
## <a name="permissions"></a>사용 권한  

**Sp_updatestats** 를 실행 하려면 사용자가 데이터베이스의 소유자 ( `dbo` 역할의 멤버가 아니라 `db_owner` ) 이거나 sysadmin 고정 서버 역할의 멤버 여야 합니다.

## <a name="examples"></a>예  
다음 예에서는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스의 테이블에 대한 통계를 업데이트합니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
EXEC sp_updatestats;   
```  

## <a name="automatic-index-and-statistics-management"></a>자동 인덱스 및 통계 관리
[Adaptive Index Defrag](https://github.com/Microsoft/tigertoolbox/tree/master/AdaptiveIndexDefrag)와 같은 솔루션을 사용하여 하나 이상의 데이터베이스에 대한 인덱스 조각 모음 및 통계 업데이트를 자동으로 관리합니다. 이 절차는 다른 매개 변수 사이에서 조각화 수준에 따라 인덱스를 다시 작성하거나 다시 구성할지 여부를 자동으로 선택하고 통계를 선형 임계값으로 업데이트합니다.

## <a name="see-also"></a>참고 항목  
 [ALTER DATABASE SET 옵션&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
 [CREATE STATISTICS&#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md)   
 [DBCC SHOW_STATISTICS&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)   
 [DROP STATISTICS&#40;Transact-SQL&#41;](../../t-sql/statements/drop-statistics-transact-sql.md)   
 [sp_autostats&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-autostats-transact-sql.md)   
 [sp_createstats &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-createstats-transact-sql.md)   
 [UPDATE STATISTICS&#40;Transact-SQL&#41;](../../t-sql/statements/update-statistics-transact-sql.md)   
 [시스템 저장 프로시저](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
 
