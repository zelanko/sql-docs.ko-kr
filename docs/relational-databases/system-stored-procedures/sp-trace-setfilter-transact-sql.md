---
title: sp_trace_setfilter (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_trace_setfilter
- sp_trace_setfilter_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_trace_setfilter
ms.assetid: 11e7c7ac-a581-4a64-bb15-9272d5c1f7ac
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 5d6646bb794b50158035759916ba823c6fca2102
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82820272"
---
# <a name="sp_trace_setfilter-transact-sql"></a>sp_trace_setfilter(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  추적에 필터를 적용합니다. **sp_trace_setfilter** 는 중지 된 기존 추적 에서만 실행할 수 있습니다 (*상태* **0**). [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]존재 하지 않거나 *상태가* **0**이 아닌 추적에서이 저장 프로시저를 실행 하는 경우 오류를 반환 합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 확장 이벤트를 대신 사용하세요.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_trace_setfilter [ @traceid = ] trace_id   
          , [ @columnid = ] column_id  
          , [ @logical_operator = ] logical_operator  
          , [ @comparison_operator = ] comparison_operator  
          , [ @value = ] value  
```  
  
## <a name="arguments"></a>인수  
`[ @traceid = ] trace_id`필터가 설정 된 추적의 ID입니다. *trace_id* 는 **int**이며 기본값은 없습니다. 사용자는이 *trace_id* 값을 사용 하 여 추적을 식별, 수정 및 제어할 수 있습니다.  
  
`[ @columnid = ] column_id`필터가 적용 되는 열의 ID입니다. *column_id* 는 **int**이며 기본값은 없습니다. *Column_id* 가 NULL 이면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 지정 된 추적에 대 한 모든 필터를 지웁니다.  
  
`[ @logical_operator = ] logical_operator`AND (**0**) 또는 or (**1**) 연산자를 적용할지 여부를 지정 합니다. *logical_operator* 는 **int**이며 기본값은 없습니다.  
  
`[ @comparison_operator = ] comparison_operator`비교할 유형을 지정 합니다. *comparison_operator* 는 **int**이며 기본값은 없습니다. 비교 연산자 및 나타내는 값이 표에 나와 있습니다.  
  
|값|비교 연산자|  
|-----------|-------------------------|  
|**0**|=(같음)|  
|**1**|<>  (같지 않음)|  
|**2**|> (보다 큼)|  
|**3**|<(보다 작음)|  
|**4**|>= (크거나 같음)|  
|**5**|<= (작거나 같음)|  
|**6**|LIKE|  
|**7**|유사하지 않음|  
  
`[ @value = ] value`필터링 할 값을 지정 합니다. *값* 의 데이터 형식은 필터링 할 열의 데이터 형식과 일치 해야 합니다. 예를 들어, 필터가 **int** 데이터 유형인 개체 ID 열에 대해 설정 된 경우 *값* 은 **int**여야 합니다. *Value* 가 **nvarchar** 또는 **varbinary**이면 최대 길이가 8000 일 수 있습니다.  
  
 비교 연산자가 LIKE 또는 NOT LIKE일 경우 논리 연산자는 "%" 또는 LIKE 연산에 적합한 다른 필터를 포함할 수 있습니다.  
  
 Null 열 값을 사용 하 여 이벤트를 필터링 하려면 *value* 에 null을 지정할 수 있습니다. **0** (= equal) 및 **1** (<> 같지 않음) 연산자만 NULL과 함께 사용할 수 있습니다. 이 경우 이러한 연산자는 [!INCLUDE[tsql](../../includes/tsql-md.md)] IS NULL 및 IS NOT NULL 연산자와 같습니다.  
  
 열 값 범위 사이에 필터를 적용 하려면 **sp_trace_setfilter** 크거나 같음 (' >= ') 비교 연산자를 사용 하 여 한 번 실행 해야 하 고 다른 시간에는 보다 작거나 같음 (' <= ') 연산자를 사용 해야 합니다.  
  
 데이터 열 데이터 형식에 대 한 자세한 내용은 [SQL Server 이벤트 클래스 참조](../../relational-databases/event-classes/sql-server-event-class-reference.md)를 참조 하세요.  
  
## <a name="return-code-values"></a>반환 코드 값  
 아래 표에서는 저장 프로시저가 완료된 후 사용자가 얻을 수 있는 코드 값을 설명합니다.  
  
|반환 코드|설명|  
|-----------------|-----------------|  
|0|오류가 없습니다.|  
|1|알 수 없는 오류입니다.|  
|2|추적이 현재 실행 중입니다. 지금 추적을 변경하변 오류가 발생합니다.|  
|4|지정한 열이 유효하지 않습니다.|  
|5|지정한 열을 필터링할 수 없습니다. 이 값은 **sp_trace_setfilter**에서만 반환 됩니다.|  
|6|지정한 비교 연산자가 유효하지 않습니다.|  
|7|지정한 논리 연산자가 유효하지 않습니다.|  
|9|지정한 추적 핸들이 유효하지 않습니다.|  
|13|메모리가 부족합니다. 지정한 동작을 수행할 메모리가 충분하지 않으면 반환됩니다.|  
|16|함수가 이 추적에 유효하지 않습니다.|  
  
## <a name="remarks"></a>설명  
 **sp_trace_setfilter** 는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이전 버전의에서 사용할 수 있는 확장 저장 프로시저에 의해 이전에 실행 된 작업을 대부분 수행 하는 저장 프로시저입니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . **Xp_trace_set \* 필터** 확장 저장 프로시저 대신 **sp_trace_setfilter** 를 사용 하 여 추적에 필터를 생성, 적용, 제거 또는 조작할 수 있습니다. 자세한 내용은 [추적 필터링](../../relational-databases/sql-trace/filter-a-trace.md)을 참조 하세요.  
  
 특정 열에 대 한 모든 필터는 **sp_trace_setfilter**한 번의 실행에서 함께 사용 해야 합니다. 예를 들어 필터 두 개를 애플리케이션 이름 열에, 그리고 필터 하나를 사용자 이름 열에 적용하려면 애플리케이션 이름에 필터를 차례로 지정해야 합니다. 한 번의 저장 프로시저 호출에서 애플리케이션 이름에 필터 하나를 지정한 다음 사용자 이름에 필터를 지정하고 애플리케이션 이름에 나머지 필터 하나를 지정하려고 하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 오류를 반환합니다.  
  
 모든 SQL 추적 저장 프로시저 (**sp_trace_xx**)의 매개 변수는 엄격 하 게 형식화 됩니다. 이러한 매개 변수를 인수 설명에 지정된 올바른 입력 매개 변수 데이터 형식으로 호출하지 않으면 저장 프로시저가 오류를 반환합니다.  
  
## <a name="permissions"></a>사용 권한  
 사용자는 ALTER TRACE 권한이 있어야 합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 추적 `1`에 필터 3개를 설정합니다. `N'SQLT%'` 및 `N'MS%'` 필터는 한 열(`AppName`, 값 `10`)에서 "`LIKE`" 비교 연산자를 사용하여 실행됩니다. `N'joe'` 필터는 다른 열(`UserName`, 값 `11`)에서 "`EQUAL`" 비교 연산자를 사용하여 실행됩니다.  
  
```  
sp_trace_setfilter  1, 10, 0, 6, N'SQLT%';  
sp_trace_setfilter  1, 10, 0, 6, N'MS%';  
sp_trace_setfilter  1, 11, 0, 0, N'joe';  
```  
  
## <a name="see-also"></a>참고 항목  
 [fn_trace_getfilterinfo &#40;Transact-sql&#41;](../../relational-databases/system-functions/sys-fn-trace-getfilterinfo-transact-sql.md)   
 [fn_trace_getinfo &#40;Transact-sql&#41;](../../relational-databases/system-functions/sys-fn-trace-getinfo-transact-sql.md)   
 [SQL 추적](../../relational-databases/sql-trace/sql-trace.md)  
  
  
