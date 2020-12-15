---
description: sys.dm_db_objects_disabled_on_compatibility_level_change(Transact-SQL)
title: sys.dm_db_objects_disabled_on_compatibility_level_change (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_db_objects_disabled_on_compatibility_level_change
- dm_db_objects_disabled_on_compatibility_level_change_TSQL
- sys.dm_db_objects_disabled_on_compatibility_level_change
- sys.dm_db_objects_disabled_on_compatibility_level_change_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_objects_disabled_on_compatibility_level_change catalog view
ms.assetid: a5d70064-0330-48b9-b853-01eba50755d0
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: fdb9fb661ed0da6eee45206acb302922243609c8
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97475084"
---
# <a name="spatial-data---sysdm_db_objects_disabled_on_compatibility_level_change"></a>공간 데이터-sys.dm_db_objects_disabled_on_compatibility_level_change
[!INCLUDE [SQL Server Azure SQL Database ](../../includes/applies-to-version/sql-asdb.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 호환성 수준 변경의 결과로 비활성화되는 인덱스 및 제약 조건을 나열합니다. 식에서 공간 UDT를 사용하는 지속형 계산 열을 포함하는 인덱스 및 제약 조건은 호환성 수준을 업그레이드하거나 변경하면 비활성화됩니다. 이 동적 관리 함수를 사용하여 호환성 수준 변경의 결과를 확인할 수 있습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```sql  
sys.dm_db_objects_disabled_on_compatibility_level_change ( compatibility_level )   
```  
  
##  <a name="arguments"></a><a name="Arguments"></a> 인수  
 *compatibility_level*  
 설정 하려는 호환성 수준을 식별 하는 **int** 입니다.  
  
## <a name="table-returned"></a>반환된 테이블  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**class**|**int**|1 = 제약 조건<br /><br /> 7 = 인덱스 및 힙|  
|**class_desc**|**nvarchar(60)**|제약 조건의 경우 OBJECT 또는 COLUMN<br /><br /> 인덱스 및 힙의 경우 INDEX|  
|**major_id**|**int**|제약 조건의 개체 ID<br /><br /> 인덱스 및 힙을 포함하는 테이블의 개체 ID|  
|**minor_id**|**int**|제약 조건의 경우 NULL<br /><br /> 인덱스 및 힙의 경우 Index_id|  
|**관계가**|**nvarchar(60)**|제약 조건 또는 인덱스의 비활성을 야기하는 종속성에 대한 설명입니다. 업그레이드 중 발생하는 경고에도 동일한 값이 사용됩니다. 이러한 데이터의 예는 다음과 같습니다.<br /><br /> 내장 함수의 경우 "space"<br /><br /> 시스템 UDT의 경우 "geometry"<br /><br /> 시스템 UDT의 메서드의 경우 "geography::Parse"|  
  
## <a name="general-remarks"></a>일반적인 주의 사항  
 호환성 수준을 변경하면 일부 내장 함수를 사용하는 지속형 계산 열이 비활성화됩니다. 또한 Geometry나 Geography 메서드를 사용하는 지속형 계산 열은 데이터베이스 업그레이드 시 비활성화됩니다.  
  
### <a name="which-functions-cause-persisted-computed-columns-to-be-disabled"></a>지속형 계산 열을 비활성화하는 함수  
 지속형 계산 열의 식에서 다음 함수를 사용할 경우 호환성 수준을 80에서 90으로 변경하면 해당 열을 참조하는 인덱스 및 제약 조건이 비활성화됩니다.  
  
-   **IsNumeric**  
  
 지속형 계산 열의 식에서 다음 함수를 사용할 경우 호환성 수준을 100에서 110 이상으로 변경하면 해당 열을 참조하는 인덱스 및 제약 조건이 비활성화됩니다.  
  
-   **Soundex**  
  
-   **Geography:: GeomFromGML**  
  
-   **Geography:: STGeomFromText**  
  
-   **Geography:: STLineFromText**  
  
-   **Geography:: STPolyFromText**  
  
-   **Geography:: STMPointFromText**  
  
-   **Geography:: STMLineFromText**  
  
-   **Geography:: STMPolyFromText**  
  
-   **Geography:: STGeomCollFromText**  
  
-   **Geography:: STGeomFromWKB**  
  
-   **Geography:: STLineFromWKB**  
  
-   **Geography:: STPolyFromWKB**  
  
-   **Geography:: STMPointFromWKB**  
  
-   **Geography:: STMLineFromWKB**  
  
-   **Geography:: STMPolyFromWKB**  
  
-   **Geography:: STUnion**  
  
-   **Geography:: STIntersection**  
  
-   **Geography:: STDifference**  
  
-   **Geography:: STSymDifference**  
  
-   **Geography:: STBuffer**  
  
-   **Geography:: BufferWithTolerance**  
  
-   **Geography:: Parse**  
  
-   **Geography:: 줄임**  
  
### <a name="behavior-of-the-disabled-objects"></a>비활성화된 개체의 동작  
 **인덱스**  
  
 클러스터형 인덱스를 사용할 수 없거나 비클러스터형 인덱스가 강제로 적용 된 경우에는 다음 오류가 발생 합니다. "인덱스 '% (으)로 인해 쿼리 프로세서에서 계획을 생성할 수 없습니다. \* ls ' 테이블 또는 뷰 '%. \* ls '을 (를) 사용할 수 없습니다. " 이러한 개체를 다시 활성화 하려면 업그레이드 후 **ALTER INDEX ON ...를 호출 하 여 인덱스를 다시 작성 합니다. 다시 작성**.  
  
 **힙**  
  
 비활성화된 힙이 포함된 테이블을 사용하면 다음 오류가 발생합니다. 이러한 개체를 다시 활성화 하려면 업그레이드 후 **ALTER INDEX ALL ON ...을 호출 하 여 다시 빌드하십시오. 다시 작성**.  
  
```  
// ErrorNumber: 8674  
// ErrorSeverity: EX_USER  
// ErrorFormat: The query processor is unable to produce a plan because the table or view '%.*ls' is disabled.  
// ErrorCause: The table has a disabled heap.   
// ErrorCorrectiveAction: Rebuild the disabled heap to enable it.   
// ErrorInserts: table or view name   
// ErrorOwner: mtintor   
// ErrorFirstProduct: SQL11  
```  
  
 온라인 작업 중에 힙을 다시 작성 하려고 하면 오류가 발생 합니다.  
  
 **CHECK 제약 조건 및 외래 키**  
  
 비활성화된 CHECK 제약 조건 및 외래 키는 오류를 일으키지 않습니다. 그러나 행이 수정될 때 제약 조건이 적용되지 않습니다. 이러한 개체를 다시 사용 하도록 설정 하려면 업그레이드 후 **ALTER TABLE ... CHECK 제약 조건** 입니다.  
  
 **지속형 계산 열**  
  
 단일 열은 비활성화할 수 없으므로 클러스터형 인덱스나 힙을 비활성화하여 전체 테이블이 비활성화됩니다.  
  
## <a name="security"></a>보안  
  
### <a name="permissions"></a>사용 권한  
 VIEW DATABASE STATE 권한이 필요합니다.  
  
## <a name="example"></a>예  
 다음 예에서는 호환성 수준을 120로 변경 하 여 영향을 받는 개체를 찾는 **sys.dm_db_objects_disabled_on_compatibility_level_change** 에 대 한 쿼리를 보여 줍니다.  
  
```sql  
SELECT * FROM sys.dm_db_objects_disabled_on_compatibility_level_change(120);  
GO  
  
```  
  
  
