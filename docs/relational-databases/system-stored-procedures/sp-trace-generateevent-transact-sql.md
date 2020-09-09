---
description: sp_trace_generateevent(Transact-SQL)
title: sp_trace_generateevent (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_trace_generateevent_TSQL
- sp_trace_generateevent
dev_langs:
- TSQL
helpviewer_keywords:
- sp_trace_generateevent
ms.assetid: 3ef05bfb-b467-4403-89cc-6e77ef9247dd
author: markingmyname
ms.author: maghan
ms.openlocfilehash: d8a5e027b2d76aa1e6965f1fe782b8987a927ce3
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89541591"
---
# <a name="sp_trace_generateevent-transact-sql"></a>sp_trace_generateevent(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 사용자 정의 이벤트를 만듭니다.  
  
>**참고:**  이 저장 프로시저는 더 이상 사용 되지 **않습니다** . 모든 다른 추적 관련 저장 프로시저는 더 이상 사용되지 않습니다.  
  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_trace_generateevent [ @eventid = ] event_id   
     [ , [ @userinfo = ] 'user_info' ]  
     [ , [ @userdata = ] user_data ]  
```  
  
## <a name="arguments"></a>인수  
`[ @eventid = ] event_id` 설정할 이벤트의 ID입니다. *event_id* 는 **int**이며 기본값은 없습니다. ID는 [sp_trace_setevent](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)설정 된 사용자 정의 이벤트를 나타내는 82에서 91 까지의 이벤트 번호 중 하나 여야 합니다.  
  
`[ @userinfo = ] 'user_info'` 이벤트의 이유를 식별 하는 선택적 사용자 정의 문자열입니다. *user_info* 은 **nvarchar (128)** 이며 기본값은 NULL입니다.  
  
`[ @userdata = ] user_data` 이벤트에 대 한 선택적 사용자 지정 데이터입니다. *user_data* 은 **varbinary (8000)** 이며 기본값은 NULL입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 아래 표에서는 저장 프로시저가 완료된 후 사용자가 얻을 수 있는 코드 값을 설명합니다.  
  
|반환 코드|설명|  
|-----------------|-----------------|  
|**0**|오류가 없습니다.|  
|**1**|알 수 없는 오류입니다.|  
|**3**|지정한 이벤트가 유효하지 않습니다. 이벤트가 존재하지 않거나 저장 프로시저에 적합하지 않습니다.|  
|**13**|메모리가 부족합니다. 지정한 동작을 수행할 메모리가 충분하지 않으면 반환됩니다.|  
  
## <a name="remarks"></a>설명  
 **sp_trace_generateevent** 은 **xp_trace_ \* ** 확장 저장 프로시저에 의해 이전에 실행 된 많은 동작을 수행 합니다. **Xp_trace_generate_event**대신 **sp_trace_generateevent** 를 사용 합니다.  
  
 사용자 정의 이벤트의 ID 번호만 **sp_trace_generateevent**와 함께 사용할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 다른 이벤트 ID가 사용되면 오류를 반환합니다.  
  
 모든 SQL 추적 저장 프로시저 (**sp_trace_xx**)의 매개 변수는 엄격 하 게 형식화 됩니다. 이러한 매개 변수가 정확한 입력 매개 변수 데이터 형식으로 호출되지 않으면 인수 설명에서 지정한 대로 저장 프로시저는 오류를 반환합니다.  
  
## <a name="permissions"></a>사용 권한  
 사용자는 ALTER TRACE 권한이 있어야 합니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 예제 테이블에 사용자 구성 이벤트를 만듭니다.  
  
```  
--Create a sample table.  
CREATE TABLE user_config_test(col1 int, col2 char(10));  
  
--DROP the trigger if it already exists.  
IF EXISTS  
   (SELECT * FROM sysobjects WHERE name = 'userconfig_trg')  
   DROP TRIGGER userconfig_trg;  
  
--Create an ON INSERT trigger on the sample table.  
CREATE TRIGGER userconfig_trg  
   ON user_config_test FOR INSERT;  
AS  
EXEC master..sp_trace_generateevent  
   @event_class = 82, @userinfo = N'Inserted row into user_config_test';  
  
--When an insert action happens, the user-configurable event fires. If   
you were capturing the event id=82, you will see it in the Profiler output.  
INSERT INTO user_config_test VALUES(1, 'abc');  
```  
  
## <a name="see-also"></a>참고 항목  
 [fn_trace_geteventinfo &#40;Transact-sql&#41;](../../relational-databases/system-functions/sys-fn-trace-geteventinfo-transact-sql.md)   
 [sp_trace_setevent&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [SQL 추적](../../relational-databases/sql-trace/sql-trace.md)  
  
  
