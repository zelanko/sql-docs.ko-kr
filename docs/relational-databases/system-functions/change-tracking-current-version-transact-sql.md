---
description: CHANGE_TRACKING_CURRENT_VERSION(Transact-SQL)
title: CHANGE_TRACKING_CURRENT_VERSION (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 08/08/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- CHANGE_TRACKING_CURRENT_VERSION_TSQL
- CHANGE_TRACKING_CURRENT_VERSION
dev_langs:
- TSQL
helpviewer_keywords:
- change tracking [SQL Server], CHANGE_TRACKING_CURRENT_VERSION
- CHANGE_TRACKING_CURRENT_VERSION
ms.assetid: 3027c4f7-6b4d-4089-a369-5926e8a8da1c
author: rothja
ms.author: jroth
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 874cf3c72400cc4885ec2515e005bb01ea42d473
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97440634"
---
# <a name="change_tracking_current_version-transact-sql"></a>CHANGE_TRACKING_CURRENT_VERSION(Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  마지막으로 커밋된 트랜잭션과 연관된 버전을 반환합니다. 이 버전은 [CHANGETABLE](../../relational-databases/system-functions/changetable-transact-sql.md)을 사용 하 여 변경 내용을 열거할 때 사용할 수 있습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
CHANGE_TRACKING_CURRENT_VERSION ( )  
```  
  
## <a name="return-type"></a>반환 형식  
 **bigint**  
  
## <a name="remarks"></a>설명  
 데이터베이스에 대해 변경 내용 추적이 설정되어 있지 않으면 NULL을 반환합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 추적된 변경 내용의 현재 버전을 저장하기 위해 지역 변수 `@next_baseline`을 선언한 다음 `CHANGE_TRACKING_CURRENT_VERSION()` 함수를 사용하여 이 변수에 대한 값을 가져옵니다.  
  
```sql  
DECLARE @next_baseline bigint;  
SET @next_baseline = CHANGE_TRACKING_CURRENT_VERSION();  
```  
  
## <a name="see-also"></a>참고 항목  
 [변경 내용 추적 함수&#40;Transact-SQL&#41;](../../relational-databases/system-functions/change-tracking-functions-transact-sql.md)   
 [CHANGETABLE&#40;Transact-SQL&#41;](../../relational-databases/system-functions/changetable-transact-sql.md)   
 [CHANGE_TRACKING_MIN_VALID_VERSION&#40;Transact-SQL&#41;](../../relational-databases/system-functions/change-tracking-min-valid-version-transact-sql.md)   
 [데이터 변경 내용 추적&#40;SQL Server&#41;](../../relational-databases/track-changes/track-data-changes-sql-server.md)  
  
  
