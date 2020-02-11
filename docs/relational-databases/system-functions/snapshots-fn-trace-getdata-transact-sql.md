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
ms.openlocfilehash: a85a911d4c9f5cd4565e9839f3be44a4e2366079
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68067749"
---
# <a name="snapshotsfn_trace_getdata-transact-sql"></a>snapshots.fn_trace_getdata(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
|\<모든 추적 열>|\<> 다릅니다.|관리 데이터 웨어하우스 데이터베이스의 snapshots.trace_data 테이블에 있는 추적 데이터입니다.<br /><br /> 지정된 추적에 대한 열 목록은 다음 쿼리를 사용하여 얻을 수 있습니다.<br /><br /> `SELECT * FROM sys.trace_columns`<br /><br /> **참고:** Fn_trace_gettable 함수에서 반환 되는 열은 trace_columns 시스템 뷰의 name 열에 있는 값에 해당 합니다. 함수를 사용할 경우 GroupID 열이 반환되지 않는다는 점만 다릅니다.|  
  
## <a name="permissions"></a>사용 권한  
 mdw_reader에 대한 SELECT 권한이 필요합니다.  
  
## <a name="see-also"></a>참고 항목  
 [데이터 컬렉션](../../relational-databases/data-collection/data-collection.md)  
  
  
