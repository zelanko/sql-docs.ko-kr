---
title: sp_autostats (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_autostats_TSQL
- sp_autostats
dev_langs:
- TSQL
helpviewer_keywords:
- sp_autostats
ms.assetid: d1df8c15-ee73-49eb-9d13-6e98943c3e38
caps.latest.revision: 38
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: 5e1b26b708db7fc435ea6f37ce81e6ff734e5f7d
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39553443"
---
# <a name="spautostats-transact-sql"></a>sp_autostats(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  인덱스, 통계 개체, 테이블 또는 인덱싱된 뷰에 대한 자동 통계 업데이트 옵션 AUTO_UPDATE_STATISTICS를 표시하거나 변경합니다.  
  
 AUTO_UPDATE_STATISTICS 옵션에 대 한 자세한 내용은 참조 하세요. [ALTER DATABASE SET 옵션 &#40;TRANSACT-SQL&#41; ](../../t-sql/statements/alter-database-transact-sql-set-options.md) 하 고 [통계](../../relational-databases/statistics/statistics.md).  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_autostats [ @tblname = ] 'table_or_indexed_view_name'   
    [ , [ @flagc = ] 'stats_value' ]   
    [ , [ @indname = ] 'statistics_name' ]  
```  
  
## <a name="arguments"></a>인수  
 [  **@tblname=** ] **'***table_or_indexed_view_name***'**  
 AUTO_UPDATE_STATISTICS 옵션을 표시하려는 테이블 또는 인덱싱된 뷰의 이름입니다. *table_or_indexed_view_name* 됩니다 **nvarchar(776)**, 기본값은 없습니다.  
  
 [  **@flagc=** ] **'***stats_value***'**  
 AUTO_UPDATE_STATISTICS 옵션을 다음 값 중 하나로 업데이트합니다.  
  
 **ON** = ON  
  
 **OFF** = OFF  
  
 때 *stats_flag* 은 지정 하지 않으면 현재 AUTO_UPDATE_STATISTICS 설정을 표시 합니다. *stats_value* 됩니다 **varchar(10)**, 기본값은 NULL입니다.  
  
 [  **@indname=** ] **'***statistics_name***'**  
 AUTO_UPDATE_STATISTICS 옵션을 표시하거나 업데이트할 통계의 이름입니다. 인덱스에 대한 통계를 표시하려면 인덱스 이름을 사용하면 됩니다. 인덱스와 해당 통계 개체는 동일한 이름을 갖습니다.  
  
 *statistics_name* 됩니다 **sysname**, 기본값은 NULL입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
 하는 경우 *stats_flag* 를 지정 하면 **sp_autostats** 하지만 결과 집합이 반환 하는 동작을 보고 합니다.  
  
 하는 경우 *stats_flag* 지정 하지 않으면 **sp_autostats** 다음 결과 집합을 반환 합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**Index Name**|**varchar(60)**|인덱스 또는 통계의 이름입니다.|  
|**AUTOSTATS가**|**varchar(3)**|AUTO_UPDATE_STATISTICS 옵션의 현재 값입니다.|  
|**마지막으로 업데이트**|**datetime**|가장 최근의 통계 업데이트 날짜입니다.|  
  
 테이블 또는 인덱싱된 뷰의 인덱스, AUTO_CREATE_STATISTICS 옵션을 사용 하 여 생성 하는 단일 열 통계에 대 한 생성 된 통계를 포함 하 고 작성 된 통계에 대 한 결과 집합을 [CREATE STATISTICS](../../t-sql/statements/create-statistics-transact-sql.md) 문입니다.  
  
## <a name="remarks"></a>Remarks  
 지정된 인덱스가 비활성화되었거나 지정된 테이블에 비활성화된 클러스터형 인덱스가 있는 경우에는 오류 메시지가 표시됩니다.  
  
 메모리 최적화 테이블의 AUTO_UPDATE_STATISTICS는 항상 OFF입니다.  
  
## <a name="permissions"></a>사용 권한  
 옵션 AUTO_UPDATE_STATISTICS를 변경 하려면 멤버 자격 n에 필요 합니다 **db_owner** 고정 데이터베이스 역할 또는 ALTER 권한이 *table_name*합니다. AUTO_UPDATE_STATISTICS를 표시 하려면 옵션은의 멤버 자격이 필요 합니다 **공용** 역할입니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-display-the-status-of-all-statistics-on-a-table"></a>1. 테이블의 모든 통계에 대한 상태 표시  
 다음은 `Product` 테이블의 모든 통계에 대한 상태를 표시합니다.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_autostats 'Production.Product';  
GO  
```  
  
### <a name="b-enable-autoupdatestatistics-for-all-statistics-on-a-table"></a>2. 테이블의 모든 통계에 대해 AUTO_UPDATE_STATISTICS 활성화  
 다음은 `Product` 테이블의 모든 통계에 대해 AUTO_UPDATE_STATISTICS 옵션을 활성화합니다.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_autostats 'Production.Product', 'ON';  
GO  
```  
  
### <a name="c-disable-autoupdatestatistics-for-a-specific-index"></a>3. 특정 인덱스에 대해 AUTO_UPDATE_STATISTICS 비활성화  
 다음 예에서는 `AK_Product_Name` 테이블의 `Product` 인덱스에 대해 AUTO_UPDATE_STATISTICS 옵션을 비활성화합니다.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_autostats 'Production.Product', 'OFF', AK_Product_Name;  
GO  
```  
  
## <a name="see-also"></a>관련 항목  
 [통계](../../relational-databases/statistics/statistics.md)   
 [ALTER DATABASE SET 옵션&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
 [데이터베이스 엔진 저장 프로시저 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [CREATE STATISTICS&#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md)   
 [DBCC SHOW_STATISTICS&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)   
 [DROP STATISTICS&#40;Transact-SQL&#41;](../../t-sql/statements/drop-statistics-transact-sql.md)   
 [sp_createstats &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-createstats-transact-sql.md)   
 [UPDATE STATISTICS&#40;Transact-SQL&#41;](../../t-sql/statements/update-statistics-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
