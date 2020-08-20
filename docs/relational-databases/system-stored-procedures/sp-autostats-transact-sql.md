---
description: sp_autostats(Transact-SQL)
title: sp_autostats (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_autostats_TSQL
- sp_autostats
dev_langs:
- TSQL
helpviewer_keywords:
- sp_autostats
ms.assetid: d1df8c15-ee73-49eb-9d13-6e98943c3e38
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 113b17db3bd06b8855b91bea2b67b96831b42ac1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88474478"
---
# <a name="sp_autostats-transact-sql"></a>sp_autostats(Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  인덱스, 통계 개체, 테이블 또는 인덱싱된 뷰에 대한 자동 통계 업데이트 옵션 AUTO_UPDATE_STATISTICS를 표시하거나 변경합니다.  
  
 AUTO_UPDATE_STATISTICS 옵션에 대 한 자세한 내용은 [ALTER DATABASE SET Options &#40;transact-sql&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md) 및 [STATISTICS](../../relational-databases/statistics/statistics.md)를 참조 하세요.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_autostats [ @tblname = ] 'table_or_indexed_view_name'   
    [ , [ @flagc = ] 'stats_flag' ]   
    [ , [ @indname = ] 'statistics_name' ]  
```  
  
## <a name="arguments"></a>인수  
`[ @tblname = ] 'table_or_indexed_view_name'` AUTO_UPDATE_STATISTICS 옵션을 표시할 테이블 또는 인덱싱된 뷰의 이름입니다. *table_or_indexed_view_name* 은 **nvarchar (776)** 이며 기본값은 없습니다.  
  
`[ @flagc = ] 'stats_flag'` AUTO_UPDATE_STATISTICS 옵션을 다음 값 중 하나로 업데이트 합니다.  
  
 **ON** = ON  
  
 **OFF** = OFF  
  
 *Stats_flag* 지정 되지 않은 경우 현재 AUTO_UPDATE_STATISTICS 설정을 표시 합니다. *stats_flag* 는 **varchar (10)** 이며 기본값은 NULL입니다.  
  
`[ @indname = ] 'statistics_name'` AUTO_UPDATE_STATISTICS 옵션을 표시 하거나 업데이트할 통계의 이름입니다. 인덱스에 대한 통계를 표시하려면 인덱스 이름을 사용하면 됩니다. 인덱스와 해당 통계 개체는 동일한 이름을 갖습니다.  
  
 *statistics_name* 는 **sysname**이며 기본값은 NULL입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
 *Stats_flag* 지정 하면 **sp_autostats** 는 수행 된 작업을 보고 하지만 결과 집합을 반환 하지 않습니다.  
  
 *Stats_flag* 지정 되지 않은 경우 **sp_autostats** 는 다음 결과 집합을 반환 합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**인덱스 이름**|**varchar(60)**|인덱스 또는 통계의 이름입니다.|  
|**AUTOSTATS**|**varchar (3)**|AUTO_UPDATE_STATISTICS 옵션의 현재 값입니다.|  
|**마지막으로 업데이트한 날짜**|**datetime**|가장 최근의 통계 업데이트 날짜입니다.|  
  
 테이블 또는 인덱싱된 뷰에 대 한 결과 집합에는 인덱스에 대해 생성 된 통계, AUTO_CREATE_STATISTICS 옵션으로 생성 된 단일 열 통계 및 [CREATE statistics](../../t-sql/statements/create-statistics-transact-sql.md) 문으로 만든 통계가 포함 됩니다.  
  
## <a name="remarks"></a>설명  
 지정된 인덱스가 비활성화되었거나 지정된 테이블에 비활성화된 클러스터형 인덱스가 있는 경우에는 오류 메시지가 표시됩니다.  
  
 메모리 최적화 테이블의 AUTO_UPDATE_STATISTICS는 항상 OFF입니다.  
  
## <a name="permissions"></a>사용 권한  
 AUTO_UPDATE_STATISTICS 옵션을 변경 하려면 **db_owner** 고정 데이터베이스 역할의 멤버 자격 또는 *table_name*에 대 한 ALTER 권한이 필요 합니다. AUTO_UPDATE_STATISTICS 옵션을 표시 하려면 **public** 역할의 멤버 자격이 필요 합니다.  
  
## <a name="examples"></a>예제  
  
### <a name="a-display-the-status-of-all-statistics-on-a-table"></a>A. 테이블의 모든 통계에 대한 상태 표시  
 다음은 `Product` 테이블의 모든 통계에 대한 상태를 표시합니다.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_autostats 'Production.Product';  
GO  
```  
  
### <a name="b-enable-auto_update_statistics-for-all-statistics-on-a-table"></a>B. 테이블의 모든 통계에 대해 AUTO_UPDATE_STATISTICS 활성화  
 다음은 `Product` 테이블의 모든 통계에 대해 AUTO_UPDATE_STATISTICS 옵션을 활성화합니다.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_autostats 'Production.Product', 'ON';  
GO  
```  
  
### <a name="c-disable-auto_update_statistics-for-a-specific-index"></a>C. 특정 인덱스에 대해 AUTO_UPDATE_STATISTICS 비활성화  
 다음 예에서는 `AK_Product_Name` 테이블의 `Product` 인덱스에 대해 AUTO_UPDATE_STATISTICS 옵션을 비활성화합니다.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_autostats 'Production.Product', 'OFF', AK_Product_Name;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [통계](../../relational-databases/statistics/statistics.md)   
 [ALTER DATABASE SET 옵션&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
 [Transact-sql&#41;&#40;저장 프로시저 데이터베이스 엔진 ](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [CREATE STATISTICS&#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md)   
 [DBCC SHOW_STATISTICS&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)   
 [DROP STATISTICS&#40;Transact-SQL&#41;](../../t-sql/statements/drop-statistics-transact-sql.md)   
 [Transact-sql&#41;sp_createstats &#40;](../../relational-databases/system-stored-procedures/sp-createstats-transact-sql.md)   
 [UPDATE STATISTICS&#40;Transact-SQL&#41;](../../t-sql/statements/update-statistics-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
