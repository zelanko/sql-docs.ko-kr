---
title: sp_trace_generateevent (TRANSACT-SQL) | Microsoft Docs
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
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 8a24bb05e8f10e2920bd206531723c228d6c1734
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58529355"
---
# <a name="sptracegenerateevent-transact-sql"></a>sp_trace_generateevent(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 사용자 정의 이벤트를 만듭니다.  
  
>**참고:**  이 저장 프로시저가 **되지** 사용 되지 않습니다. 모든 다른 추적 관련 저장 프로시저는 더 이상 사용되지 않습니다.  
  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_trace_generateevent [ @eventid = ] event_id   
     [ , [ @userinfo = ] 'user_info' ]  
     [ , [ @userdata = ] user_data ]  
```  
  
## <a name="arguments"></a>인수  
`[ @eventid = ] event_id` 설정할 이벤트의 ID입니다. *event_id* 됩니다 **int**, 기본값은 없습니다. ID는 82에서 91 사용한 설정에 따라 사용자 정의 이벤트를 나타내는 사이의 이벤트 번호 중 하나 여야 합니다 [sp_trace_setevent](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)합니다.  
  
`[ @userinfo = ] 'user_info'` 이벤트에 대 한 이유를 식별 하는 선택적 사용자 정의 문자열입니다. *user_info* 됩니다 **nvarchar (128)**, 기본값은 NULL입니다.  
  
`[ @userdata = ] user_data` 이벤트에 대 한 선택적 사용자 지정 데이터입니다. *user_data* 됩니다 **varbinary(8000)**, 기본값은 NULL입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 아래 표에서는 저장 프로시저가 완료된 후 사용자가 얻을 수 있는 코드 값을 설명합니다.  
  
|반환 코드|Description|  
|-----------------|-----------------|  
|**0**|오류가 없습니다.|  
|**1**|알 수 없는 오류입니다.|  
|**3**|지정한 이벤트가 유효하지 않습니다. 이벤트가 존재하지 않거나 저장 프로시저에 적합하지 않습니다.|  
|**13**|메모리가 부족합니다. 지정한 동작을 수행할 메모리가 충분하지 않으면 반환됩니다.|  
  
## <a name="remarks"></a>Remarks  
 **sp_trace_generateevent** 실행 하 던 작업의 대부분을 수행 합니다 **xp_trace_\***  확장 저장된 프로시저입니다. 사용 하 여 **sp_trace_generateevent** of **xp_trace_generate_event**합니다.  
  
 사용자 정의 이벤트의 ID 번호에만 사용할 수 있습니다 **sp_trace_generateevent**합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 다른 이벤트 ID가 사용되면 오류를 반환합니다.  
  
 모든 SQL Trace 저장 프로시저(**sp_trace_xx**)의 매개 변수는 엄격하게 형식이 지정되어 있습니다. 이러한 매개 변수가 인수 설명에서 지정한대로 정확한 입력 매개 변수 데이터 형식으로 호출되지 않으면 저장 프로시저는 오류를 반환합니다.  
  
## <a name="permissions"></a>사용 권한  
 사용자는 ALTER TRACE 권한이 있어야 합니다.  
  
## <a name="examples"></a>예  
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
  
## <a name="see-also"></a>참고자료  
 [sys.fn_trace_geteventinfo &#40;TRANSACT-SQL&#41;](../../relational-databases/system-functions/sys-fn-trace-geteventinfo-transact-sql.md)   
 [sp_trace_setevent&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [SQL 추적](../../relational-databases/sql-trace/sql-trace.md)  
  
  
