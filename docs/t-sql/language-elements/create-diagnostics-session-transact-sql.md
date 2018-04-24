---
title: CREATE DIAGNOSTICS SESSION(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: pdw
ms.service: ''
ms.component: t-sql|language-elements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 662d019e-f217-49df-9e2f-b5662fa0342d
caps.latest.revision: 9
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: On Demand
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: fc95a6505066b29b30e5916b1000c686ecad4907
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="create-diagnostics-session-transact-sql"></a>CREATE DIAGNOSTICS SESSION(Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  진단 세션을 사용하면 시스템 또는 쿼리 성능에 자세한 사용자 정의 진단 정보를 저장할 수 있습니다.  
  
 진단 세션은 일반적으로 특정 쿼리의 성능을 디버깅하거나 기기 어플라이언스 작업 중 특정 어플라이언스 구성 요소의 동작을 모니터링하는 데 사용됩니다.  
  
> [!NOTE]  
>  진단 세션을 사용하려면 XML에 대해 잘 알고 있어야 합니다.  
  
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
 진단 세션의 이름입니다. 진단 세션 이름은 문자 a-z, A-Z 및 0-9로만 이루어져야 합니다. 또한 진단 세션 이름은 문자로 시작해야 합니다. *diagnostics_name*은 127자로 제한됩니다.  
  
 *max_item_count_num*  
 보기에 유지할 이벤트 수입니다. 예를 들어 100을 지정하는 경우 필터 조건과 일치하는 최신 이벤트 100개가 진단 세션에 유지됩니다. 일치하는 이벤트가 100개보다 작은 경우 진단 세션은 100개 미만의 이벤트를 포함하게 됩니다. *max_item_count_num*은 100 이하이거나 100,000개여야 합니다.  
  
 *event_name*  
 진단 세션에서 수집할 실제 이벤트를 정의합니다.  *event_name*은 `sys.pdw_diag_events.is_enabled='True'`의 [sys.pdw_diag_events](http://msdn.microsoft.com/en-us/d813aac0-cea1-4f53-b8e8-d26824bc2587)에 나열된 이벤트 중 하나입니다.  
  
 *filter_property_name*  
 결과를 제한하는 속성의 이름입니다. 예를 들어, 세션 ID에 따라 제한하려는 경우 *filter_property_name*은 *SessionId*여야 합니다. *filter_property_name*에 대한 가능한 값의 목록은 아래 *property_name*을 참조하세요.  
  
 *value*  
 *filter_property_name*에 대해 평가할 값입니다. 값 형식은 속성 형식과 일치해야 합니다. 예를 들어, 속성 형식이 10진수이면 *값*의 형식도 10진수여야 합니다.  
  
 *comp_type*  
 비교 유형입니다. 가능한 값은 Equals, EqualsOrGreaterThan, EqualsOrLessThan, GreaterThan, LessThan, NotEquals, Contains, RegEx입니다.  
  
 *property_name*  
 이벤트와 관련된 속성입니다.  속성 이름은 캡처 태그의 일부가 되거나 필터링 조건의 일부가 될 수 있습니다.  
  
|속성 이름|Description|  
|-------------------|-----------------|  
|UserName|사용자(로그인) 이름입니다.|  
|SessionId|세션 ID입니다.|  
|QueryId|쿼리 ID입니다.|  
|CommandType|명령 유형입니다.|  
|CommandText|처리된 명령 내 텍스트입니다.|  
|OperationType|이벤트에 대한 작업 유형입니다.|  
|Duration|이벤트의 기간입니다.|  
|SPID|서비스 프로세스 ID입니다.|  
  
## <a name="remarks"></a>Remarks  
 각 사용자는 최대 10개의 동시 진단 세션이 허용됩니다. 현재 세션 목록은 [sys.pdw_diag_sessions](http://msdn.microsoft.com/en-us/ca111ddc-2787-4205-baf0-1a242c0257a9)를 참조하고, `DROP DIAGNOSTICS SESSION`을 사용하여 필요 없는 세션을 드롭하세요.  
  
 진단 세션은 드롭될 때까지 메타데이터를 계속 수집합니다.  
  
## <a name="permissions"></a>사용 권한  
 **ALTER SERVER STATE** 권한이 필요합니다.  
  
## <a name="locking"></a>잠금  
 진단 세션 테이블에 공유 잠금을 사용합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-creating-a-diagnostics-session"></a>1. 진단 세션 만들기  
 이 예제에서는 데이터베이스 엔진 성능의 메트릭을 기록하는 진단 세션을 만듭니다. 이 예제에서는 엔진 쿼리 실행/종료 이벤트 및 차단 DMS 이벤트를 수신하는 진단 세션을 만듭니다. 반환되는 항목은 명령 텍스트, 컴퓨터 이름, 요청 ID(쿼리 ID) 및 이벤트가 만들어진 세션입니다.  
  
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
  
 진단 세션을 만든 후 쿼리를 실행합니다.  
  
```  
SELECT COUNT(EmployeeKey) FROM AdventureWorksPDW2012..FactSalesQuota;  
```  
  
 그런 다음, sysdiag 스키마에서 선택하여 진단 세션 결과를 봅니다.  
  
```  
SELECT * FROM master.sysdiag.MYDIAGSESSION;  
```  
  
 sysdiag 스키마는 진단 세션 이름으로 명명된 보기를 포함합니다.  
  
 연결에 대한 작업만 확인하려면 `Session.SPID` 속성을 추가하고 `WHERE [Session.SPID] = @@spid;`를 쿼리에 추가합니다.  
  
 진단 세션을 사용하여 마치면 **DROP DIAGNOSTICS** 명령을 사용하여 드롭합니다.  
  
```  
DROP DIAGNOSTICS SESSION MYDIAGSESSION;  
```  
  
### <a name="b-alternative-diagnostic-session"></a>2. 대체 진단 세션  
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
  
 다음과 같은 쿼리를 실행합니다.  
  
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
  
 진단 세션을 사용하여 마치면 **DROP DIAGNOSTICS** 명령을 사용하여 드롭합니다.  
  
```  
DROP DIAGNOSTICS SESSION PdwOptimizationDiagnostics;  
```  
  
  
