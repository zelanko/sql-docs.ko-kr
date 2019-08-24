---
title: CHANGE_TRACKING_IS_COLUMN_IN_MASK (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/08/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- CHANGE_TRACKING_IS_COLUMN_IN_MASK_TSQL
- CHANGE_TRACKING_IS_COLUMN_IN_MASK
dev_langs:
- TSQL
helpviewer_keywords:
- change tracking [SQL Server], CHANGE_TRACKING_IS_COLUMN_IN_MASK
- CHANGE_TRACKING_IS_COLUMN_IN_MASK
ms.assetid: 649b370b-da54-4915-919d-1b597a39d505
author: rothja
ms.author: jroth
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: a6f7e9d8d9ab99ebe4a7c5749033eacf85b8feb5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68042996"
---
# <a name="change_tracking_is_column_in_mask-transact-sql"></a>CHANGE_TRACKING_IS_COLUMN_IN_MASK(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  CHANGETABLE(CHANGES...) 함수에서 반환 된 SYS_CHANGE_COLUMNS 값을 해석 합니다. 이로 인해 애플리케이션은 정의된 열이 SYS_CHANGE_COLUMNS에 대해 반환된 값에 포함되는지 여부를 확인할 수 있습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
CHANGE_TRACKING_IS_COLUMN_IN_MASK ( column_id , change_columns )  
```  
  
## <a name="arguments"></a>인수  
 *column_id*  
 확인 중인 열의 ID입니다. 열 ID를 사용 하 여 가져올 수 있습니다 합니다 [COLUMNPROPERTY](../../t-sql/functions/columnproperty-transact-sql.md) 함수입니다.  
  
 *change_columns*  
 이진 데이터의 SYS_CHANGE_COLUMNS 열에는 [CHANGETABLE](../../relational-databases/system-functions/changetable-transact-sql.md) 데이터입니다.  
  
## <a name="return-type"></a>반환 형식  
 **bit**  
  
## <a name="return-values"></a>반환 값  
 CHANGE_TRACKING_IS_COLUMN_IN_MASK는 다음 값을 반환합니다.  
  
|반환 값|설명|  
|------------------|-----------------|  
|0|지정된 된 열에 없는 경우는 *change_columns* 목록입니다.|  
|1|지정된 된 열에는 *change_columns* 목록입니다.|  
  
## <a name="remarks"></a>설명  
 CHANGE_TRACKING_IS_COLUMN_IN_MASK 유효성을 검사 하는 검사를 수행 하지 않습니다 합니다 *column_id* 값 또는 합니다 *change_columns* 매개 변수는 테이블에서 가져온는  *column_id* 가져온 합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `Salary` 테이블의 `Employees` 열이 업데이트되었는지 여부를 확인합니다. 합니다 `COLUMNPROPERTY` 의 열 ID를 반환 하는 함수는 `Salary` 열입니다. `@change_columns` 지역 변수는 CHANGETABLE을 데이터 원본으로 사용하여 쿼리의 결과에 설정되어야 합니다.  
  
```sql  
SET @SalaryChanged = CHANGE_TRACKING_IS_COLUMN_IN_MASK  
    (COLUMNPROPERTY(OBJECT_ID('Employees'), 'Salary', 'ColumnId')  
    ,@change_columns);  
```  
  
## <a name="see-also"></a>관련 항목  
 [변경 내용 추적 함수&#40;Transact-SQL&#41;](../../relational-databases/system-functions/change-tracking-functions-transact-sql.md)   
 [CHANGETABLE&#40;Transact-SQL&#41;](../../relational-databases/system-functions/changetable-transact-sql.md)   
 [데이터 변경 내용 추적&#40;SQL Server&#41;](../../relational-databases/track-changes/track-data-changes-sql-server.md)  
  
  
