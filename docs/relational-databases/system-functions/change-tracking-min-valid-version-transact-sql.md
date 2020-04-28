---
title: CHANGE_TRACKING_MIN_VALID_VERSION (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 08/08/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
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
author: rothja
ms.author: jroth
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 5bb0baec2284d17d84c7a8c3dddd13de3fa69510
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68042937"
---
# <a name="change_tracking_min_valid_version-transact-sql"></a>CHANGE_TRACKING_MIN_VALID_VERSION(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  [CHANGETABLE](../../relational-databases/system-functions/changetable-transact-sql.md) 함수를 사용 하는 경우 지정 된 테이블에서 변경 내용 추적 정보를 가져오는 데 사용할 수 있는 클라이언트의 최소 버전을 반환 합니다.  
    
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
CHANGE_TRACKING_MIN_VALID_VERSION ( table_object_id )  
```  
  
## <a name="arguments"></a>인수  
 *table_object_id*  
 테이블의 개체 ID입니다. *table_object_id* 은 **int**입니다.  
  
## <a name="return-type"></a>반환 형식  
 **bigint**  
  
## <a name="remarks"></a>설명  
 이 함수를 사용 하 여 CHANGETABLE의 *last_sync_version* 매개 변수 값에 대 한 유효성을 검사 합니다. *Last_sync_version* 이 함수에서 보고 한 값 보다 작은 경우 CHANGETABLE의 이후 호출에서 반환 된 결과가 유효 하지 않을 수 있습니다.  
  
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
  
## <a name="see-also"></a>참고 항목  
 [변경 내용 추적 함수 &#40;Transact-sql&#41;](../../relational-databases/system-functions/change-tracking-functions-transact-sql.md)   
 [sys.change_tracking_tables&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/change-tracking-catalog-views-sys-change-tracking-tables.md)  
  
  
