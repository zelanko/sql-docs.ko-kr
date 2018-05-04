---
title: CHANGE_TRACKING_MIN_VALID_VERSION (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/08/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: system-functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- CHANGE_TRACKING_CLEANUP_VERSION
- CHANGE_TRACKING_CLEANUP_VERSION_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CHANGE_TRACKING_MIN_VALID_VERSION
- change tracking [SQL Server], CHANGE_TRACKING_MIN_VALID_VERSION
ms.assetid: 5a43d23f-adcf-4c0b-95ad-07cee03c1f9d
caps.latest.revision: 16
author: rothja
ms.author: jroth
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: e99a4cb1ce5adfedec22b52a05725c97ce38546e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="changetrackingminvalidversion-transact-sql"></a>CHANGE_TRACKING_MIN_VALID_VERSION(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  최소 버전을 변경 사용 하는 경우 지정된 된 테이블에서 추적 정보를 가져오는 데 사용할 유효한 클라이언트에 반환 된 [CHANGETABLE](../../relational-databases/system-functions/changetable-transact-sql.md) 함수입니다.  
    
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
CHANGE_TRACKING_MIN_VALID_VERSION ( table_object_id )  
```  
  
## <a name="arguments"></a>인수  
 *table_object_id*  
 테이블의 개체 ID입니다. *table_object_id* 는 **int**합니다.  
  
## <a name="return-type"></a>반환 형식  
 **bigint**  
  
## <a name="remarks"></a>주의  
 이 함수를 사용 하 여 값의 유효성을 검사 하는 *last_sync_version* CHANGETABLE에 대 한 매개 변수입니다. 경우 *last_sync_version* CHANGETABLE 한 이후의 호출에서 반환 되는 결과가 올바르지 않을 수 있습니다이 함수에 의해 보고 되는 값 보다 작습니다.  
  
 CHANGE_TRACKING_MIN_VALID_VERSION은 다음 정보를 사용하여 반환 값을 결정합니다.  
  
-   변경 내용 추적이 설정된 경우  
  
-   데이터베이스에 대해 지정된 보존 기간보다 오래된 qusurd sodyd 추적 정보를 제거하기 위해 백그라운드 정리 태스크가 실행된 경우  
  
-   테이블이 잘린 경우 테이블에 연결된 모든 변경 내용 추적 정보를 제거합니다.  
  
 다음 조건 중 하나에 해당할 경우 함수가 NULL을 반환합니다.  
  
-   데이터베이스의 변경 내용 추적이 설정되지 않은 경우  
  
-   지정된 테이블 개체 ID가 현재 데이터베이스에 유효하지 않은 경우  
  
-   개체 ID로 지정한 테이블에 대한 권한이 부족한 경우  
  
## <a name="examples"></a>예  
 다음 예에서는 지정한 버전이 유효한 버전인지 여부를 확인합니다. 예제에는 `dbo.Employees` 테이블의 유효한 최소 버전을 가져와 `@last_sync_version` 변수 값과 비교합니다. `@last_sync_version` 값이 `@min_valid_version` 값보다 작으면 변경된 행 목록이 유효하지 않습니다.  
  
> [!NOTE]  
>  일반적으로 데이터를 동기화하는 데 사용된 마지막 버전 번호를 저장한 다른 위치나 테이블에서 값을 가져옵니다.  
  
```  
-- The tracked change is tagged with the specified context   
DECLARE @min_valid_version bigint, @last_sync_version bigint;  
  
SET @min_valid_version =   
CHANGE_TRACKING_MIN_VALID_VERSION(OBJECT_ID('dbo.Employees'));  
  
SET @last_sync_version = 11  
IF (@last_sync_version < @min_valid_version)  
-- Error � do not obtain changes  
ELSE  
-- Obtain changes using CHANGETABLE(CHANGES ...)  
```  
  
## <a name="see-also"></a>관련 항목:  
 [변경 내용 추적 함수&#40;Transact-SQL&#41;](../../relational-databases/system-functions/change-tracking-functions-transact-sql.md)   
 [sys.change_tracking_tables&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/change-tracking-catalog-views-sys-change-tracking-tables.md)  
  
  
