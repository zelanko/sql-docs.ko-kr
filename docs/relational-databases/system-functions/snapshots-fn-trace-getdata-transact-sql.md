---
title: snapshot. fn_trace_getdata (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- snapshots.fn_trace_getdata
dev_langs:
- TSQL
helpviewer_keywords:
- snapshots.fn_trace_getdata function
ms.assetid: ac28ef48-f4f4-4bf2-ba22-d44e1be88172
author: rothja
ms.author: jroth
ms.openlocfilehash: 96120924b3362ec14df84d5043f7b7741a0f2b8f
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85898439"
---
# <a name="snapshotsfn_trace_getdata-transact-sql"></a>snapshots.fn_trace_getdata(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  이 함수는 지정된 추적에 대해 캡처된 모든 이벤트를 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
snapshots.fn_trace_gettable ( trace_info_id, start_time, end_time )  
```  
  
## <a name="arguments"></a>인수  
 *trace_info_id*  
 관리 데이터 웨어하우스 데이터베이스에 있는 trace_info 테이블의 기본 키에 대 한 고유 식별자입니다. *trace_info_id* 은 **int**입니다.  
  
 *start_time*  
 추적이 시작된 시간입니다. *start_time* 은 **datetime**입니다.  
  
 *end_time*  
 추적이 종료된 시간입니다. *end_time* 은 **datetime**입니다.  
  
## <a name="table-returned"></a>반환된 테이블  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|\<All trace columns>|\<Varies>|관리 데이터 웨어하우스 데이터베이스의 snapshots.trace_data 테이블에 있는 추적 데이터입니다.<br /><br /> 지정된 추적에 대한 열 목록은 다음 쿼리를 사용하여 얻을 수 있습니다.<br /><br /> `SELECT * FROM sys.trace_columns`<br /><br /> **참고:** Fn_trace_gettable 함수에서 반환 되는 열은 trace_columns 시스템 뷰의 name 열에 있는 값에 해당 합니다. 함수를 사용할 경우 GroupID 열이 반환되지 않는다는 점만 다릅니다.|  
  
## <a name="permissions"></a>사용 권한  
 mdw_reader에 대한 SELECT 권한이 필요합니다.  
  
## <a name="see-also"></a>참고 항목  
 [데이터 수집](../../relational-databases/data-collection/data-collection.md)  
  
  
