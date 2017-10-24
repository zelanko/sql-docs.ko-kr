---
title: "진단 세션 (Transact SQL) 만들기 | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 662d019e-f217-49df-9e2f-b5662fa0342d
caps.latest.revision: 9
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 71f3463ad4d91bd117c322e9e63c0b331b07ca9f
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="create-diagnostics-session-transact-sql"></a>진단 세션 (Transact SQL) 만들기
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw_md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  진단 세션이 시스템 또는 쿼리 성능에 한 사용자 정의 자세한 진단 정보를 저장할 수 있습니다.  
  
 진단 세션이 특정 쿼리의 성능을 디버깅 하거나 기기 작업 중 특정 기기 구성 요소의 동작을 모니터링 하려면 일반적으로 사용 됩니다.  
  
> [!NOTE]  
>  진단 세션을 사용 하려면 XML에 잘 알고 있어야 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
Creating a new diagnostics session:  
CREATE DIAGNOSTICS SESSION diagnostics_name AS N’{<session_xml>}’;  
  
<session_xml>::  
<Session>  
   [ <MaxItemCount>max_item_count_num</MaxItemCount> ]  
   <Filter>  
      { \<Event Name=”event_name”/>  
         [ <Where>\<filter_property_name Name=”value” ComparisonType="comp_type"/></Where> ] [ ,...n ]  
      } [ ,...n ]  
   </Filter> ]   
   <Capture>  
      \<Property Name=”property_name”/> [ ,...n ]  
   </Capture>  
<Session>  
  
Retrieving results for a diagnostics session:  
SELECT * FROM master.sysdiag.diagnostics_name ;  
  
Removing results for a diagnostics session:  
DROP DIAGNOSTICS SESSION diagnostics_name ;  
```  
  
## <a name="arguments"></a>인수  
 *diagnostics_name*  
 진단 세션의 이름입니다. 진단 세션 이름에는 문자 a-z, A-Z, 0-9만 포함할 수 있습니다. 또한 진단 세션 이름은 문자로 시작 해야 합니다. *diagnostics_name* 127 자로 제한 됩니다.  
  
 *max_item_count_num*  
 보기에서 유지할 이벤트 수를 지정 합니다. 예를 들어 100을 지정 하는 경우 필터 조건과 일치 하는 최신 이벤트 100은 진단 세션에 유지 됩니다. 이벤트를 일치 하는 100 보다 작은 경우 진단 세션 100 개 미만의 이벤트 포함 됩니다. *max_item_count_num* 100 이상 이어야 합니다 및 100, 000입니다.  
  
 *e n t _*  
 진단 세션에서 수집 될 실제 이벤트를 정의 합니다.  *e n t _* 에 나열 된 이벤트 중 하나는 [sys.pdw_diag_events](http://msdn.microsoft.com/en-us/d813aac0-cea1-4f53-b8e8-d26824bc2587) 여기서 `sys.pdw_diag_events.is_enabled='True'`합니다.  
  
 *filter_property_name*  
 결과 제한 하는 속성의 이름입니다. 예를 들어, 세션 id에 따라를 제한 하려는 경우 *filter_property_name* 해야 *SessionId*합니다. 참조 *property_name* 아래에 대 한 잠재적인 값의 목록에 대 한 *filter_property_name*합니다.  
  
 *value*  
 에 대해 평가할 값 *filter_property_name*합니다. 값 형식이 속성 형식과 일치 해야 합니다. 예를 들어, 속성 형식은 10 진수로 유형의 *값* 10 진수 여야 합니다.  
  
 *comp_type*  
 비교 형식입니다. Equals: 가능한 값은, EqualsOrGreaterThan, EqualsOrLessThan, 보다 큼, LessThan, NotEquals, Contains, RegEx  
  
 *property_name*  
 이벤트와 관련 된 속성입니다.  캡처 태그의 일부가 될 수 있습니다 및 필터링 조건의 일부로 사용 하는 속성 이름입니다.  
  
|속성 이름|Description|  
|-------------------|-----------------|  
|UserName|사용자 (로그인) 이름입니다.|  
|SessionId|세션 id입니다.|  
|QueryId|쿼리 id입니다.|  
|CommandType|명령 유형입니다.|  
|CommandText|처리 명령 텍스트입니다.|  
|OperationType|이벤트에 대 한 작업 유형입니다.|  
|기간|이벤트의 기간입니다.|  
|SPID|서비스 프로세스 id입니다.|  
  
## <a name="remarks"></a>주의  
 각 사용자는 최대 10 개의 동시 진단 세션이 허용 됩니다. 참조 [sys.pdw_diag_sessions](http://msdn.microsoft.com/en-us/ca111ddc-2787-4205-baf0-1a242c0257a9) 현재 세션 및 세션 사용 하 여 불필요 한 놓기 목록은 `DROP DIAGNOSTICS SESSION`합니다.  
  
 진단 세션이 삭제 될 때까지 메타 데이터를 수집할 계속 됩니다.  
  
## <a name="permissions"></a>Permissions  
 필요는 **ALTER SERVER STATE** 권한.  
  
## <a name="locking"></a>잠금  
 진단 세션 테이블에 대 한 공유 잠금을 사용합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-creating-a-diagnostics-session"></a>1. 진단 세션 만들기  
 이 예에서는 데이터베이스 엔진 성능 메트릭 기록에 대 한 진단 세션을 만듭니다. 이 예제에서는 엔진 쿼리 실행/종료 이벤트 및 차단 DMS 이벤트를 수신 하는 진단 세션을 만듭니다. 명령 텍스트, 컴퓨터 이름, 요청 id (쿼리 id) 및 이벤트에 만들어진 세션은 반환 되는 항목입니다.  
  
```  
CREATE DIAGNOSTICS SESSION MYDIAGSESSION AS N'  
<Session>  
   <MaxItemCount>100</MaxItemCount>  
   <Filter>  
      <Event Name="EngineInstrumentation:EngineQueryRunningEvent" />  
      <Event Name="DmsCoreInstrumentation:DmsBlockingQueueEnqueueBeginEvent" />  
      <Where>  
         <SessionId Value="381" ComparisonType="NotEquals" />  
      </Where>  
   </Filter>  
   <Capture>  
      <Property Name="Query.CommandText" />  
      <Property Name="MachineName" />  
      <Property Name="Query.QueryId" />  
      <Property Name="Alias" />  
      <Property Name="Duration" />  
      <Property Name="Session.SessionId" />  
   </Capture>  
</Session>';  
```  
  
 진단 세션을 만든 후 쿼리를 실행 합니다.  
  
```  
SELECT COUNT(EmployeeKey) FROM AdventureWorksPDW2012..FactSalesQuota;  
```  
  
 그런 다음 sysdiag 스키마에서 선택 하 여 진단 세션 결과 봅니다.  
  
```  
SELECT * FROM master.sysdiag.MYDIAGSESSION;  
```  
  
 진단 세션 이름을 라는 보기 sysdiag 스키마에 포함 되어 있는지 확인 합니다.  
  
 연결에 대 한 활동만 보려면 추가 `Session.SPID` 속성 추가 `WHERE [Session.SPID] = @@spid;` 쿼리 합니다.  
  
 사용 하 여 진단 세션이 끝나면 삭제는 **DROP 진단** 명령입니다.  
  
```  
DROP DIAGNOSTICS SESSION MYDIAGSESSION;  
```  
  
### <a name="b-alternative-diagnostic-session"></a>2. 진단 세션을 대체  
 약간 다른 속성을 가진 두 번째 예입니다.  
  
```  
-- Determine the session_id of your current session  
SELECT TOP 1 session_id();  
-- Replace \<*session_number*> in the code below with the numbers in your session_id  
CREATE DIAGNOSTICS SESSION PdwOptimizationDiagnostics AS N'  
<Session>  
   <MaxItemCount>100</MaxItemCount>  
   <Filter>  
      <Event Name="EngineInstrumentation:MemoGenerationBeginEvent" />  
      <Event Name="EngineInstrumentation:MemoGenerationEndEvent" />  
      <Event Name="DSQLInstrumentation:OptimizationBeginEvent" />  
      <Event Name="DSQLInstrumentation:OptimizationEndEvent" />  
      <Event Name="DSQLInstrumentation:BuildRelOpContextTreeBeginEvent" />  
      <Event Name="DSQLInstrumentation:PostPlanGenModifiersEndEvent" />  
      <Where>  
         <SessionId Value="\<*session_number*>" ComparisonType="Equals" />  
      </Where>  
   </Filter>  
   <Capture>  
      <Property Name="Session.SessionId" />  
      <Property Name="Query.QueryId" />  
      <Property Name="Query.CommandText" />  
      <Property Name="Name" />  
      <Property Name="DateTimePublished" />  
      <Property Name="DateTimePublished.Ticks" />  
  </Capture>  
</Session>';  
```  
  
 와 같은 쿼리를 실행 합니다.  
  
```  
USE ssawPDW;  
GO  
SELECT * FROM dbo.FactFinance;  
```  
  
 다음 쿼리는 권한 부여 시간을 반환합니다.  
  
```  
SELECT *   
FROM master.sysdiag.PdwOptimizationDiagnostics   
ORDER BY DateTimePublished;  
```  
  
 사용 하 여 진단 세션이 끝나면 삭제는 **DROP 진단** 명령입니다.  
  
```  
DROP DIAGNOSTICS SESSION PdwOptimizationDiagnostics;  
```  
  
  

