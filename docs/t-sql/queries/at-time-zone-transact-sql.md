---
title: AT TIME ZONE(Transact-SQL) | Microsoft Docs
ms.date: 11/16/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.custom: ''
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- AT TIME ZONE
- AT_TIME_ZONE_TSQL
helpviewer_keywords:
- AT TIME ZONE function
ms.assetid: 311f682f-7f1b-43b6-9ea0-24e36b64f73a
caps.latest.revision: 13
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 7e4323ddbdf8ac827a2a9ca6b96c98cc97b47235
ms.sourcegitcommit: a6596c62f607041c4402f7d5b41a232fca257c14
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36243555"
---
# <a name="at-time-zone-transact-sql"></a>AT TIME ZONE(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  *inputdate*를 대상 표준 시간대의 해당 *datetimeoffset* 값으로 변환합니다. *inputdate*가 오프셋 정보 없이 제공되는 경우 함수는 *inputdate* 값이 대상 표준 시간대에서 제공되는 것으로 가정하고 표준 시간대의 오프셋을 적용합니다. *inputdate*가 *datetimeoffset* 값으로 제공되는 경우 해당 **AT TIME ZONE** 절은 표준 시간대 변환 규칙을 사용하여 대상 표준 시간대로 변환합니다.  
  
 **AT TIME ZONE** 구현은 표준 시간대 전반에 **datetime** 값을 변환하기 위해 Windows 메커니즘을 따릅니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
inputdate AT TIME ZONE timezone  
```  
  
## <a name="arguments"></a>인수  
 *inputdate*  
 **smalldatetime**, **datetime**, **datetime2**, 또는 **datetimeoffset** 값으로 확인할 수 있는 식입니다.  
  
 *timezone*  
 대상 표준 시간대의 이름입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]은 Windows 레지스트리에 저장된 표준 시간대를 따릅니다. 컴퓨터에 설치되는 모든 표준 시간대는 다음 레지스트리 하이브(**KEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Time Zones**)에 저장됩니다. 설치된 표준 시간대의 목록은 [sys.time_zone_info &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-time-zone-info-transact-sql.md) 보기를 통해 공개됩니다.  
  
## <a name="return-types"></a>반환 형식  
 **datetimeoffset**의 데이터 형식 반환  
  
## <a name="return-value"></a>반환 값  
 대상 표준 시간대의 **datetimeoffset** 값입니다.  
  
## <a name="remarks"></a>Remarks  
 **AT TIME ZONE**은 DST 변경에서 영향을 받는 간격에 해당하는 **smalldatetime**, **datetime** 및 **datetime2** 데이터 형식의 입력 값을 변환하기 위한 특정 규칙을 적용합니다.  
  
-   클록을 앞당겨 설정한 경우 클록 조정 기간에 따라 기간이 달라지는 로컬 시간에 간격이 있게 됩니다(일반적으로 1시간이지만 표준 시간대에 따라 30분에서 45분이 될 수도 있습니다). 이 경우 이 간격에 속하는 시간대의 지점은 DST 변경 *후*에 오프셋으로 변환됩니다.  
  
    ```  
    /*  
        Moving to DST in "Central European Standard Time" zone: 
        offset changes from +01:00 -> +02:00   
        Change occurred on March 29th, 2015 at 02:00:00.   
        Adjusted local time became 2015-03-29 03:00:00.  
    */  
    
    --Time before DST change has standard time offset (+01:00)
    SELECT CONVERT(datetime2(0), '2015-03-29T01:01:00', 126)     
    AT TIME ZONE 'Central European Standard Time';  
    --Result: 2015-03-29 01:01:00 +01:00   
  
    /*
      Adjusted time from the "gap interval" (between 02:00 and 03:00)
      is moved 1 hour ahead and presented with the summer time offset
      (after the DST change) 
    */
    SELECT CONVERT(datetime2(0), '2015-03-29T02:01:00', 126)   
    AT TIME ZONE 'Central European Standard Time';  
    --Result: 2015-03-29 03:01:00 +02:00
      
    --Time after 03:00 is presented with the summer time offset (+02:00)
    SELECT CONVERT(datetime2(0), '2015-03-29T03:01:00', 126)   
    AT TIME ZONE 'Central European Standard Time';  
    --Result: 2015-03-29 03:01:00 +02:00  
  
    ```  
  
- 클록을 늦춰 설정한 경우 로컬 시간으로 2시간은 1시간과 겹칩니다.  이 경우 겹친 간격에 속하는 시간대의 지점은 클록 변경 *전*에 오프셋으로 표시됩니다.  
  
    ```  
    /*  
        Moving back from DST to standard time in 
        "Central European Standard Time" zone: 
        offset changes from +02:00 -> +01:00.  
        Change occurred on October 25th, 2015 at 03:00:00.   
        Adjusted local time became 2015-10-25 02:00:00   
    */  
    
    --Time before the change has DST offset (+02:00)
    SELECT CONVERT(datetime2(0), '2015-10-25T01:01:00', 126)      
    AT TIME ZONE 'Central European Standard Time';  
    --Result: 2015-10-25 01:01:00 +02:00  
    
    /*
      Time from the "overlapped interval" is presented with standard time 
      offset (before the change)    
    */
    SELECT CONVERT(datetime2(0), '2015-10-25T02:00:00', 126)   
    AT TIME ZONE 'Central European Standard Time';  
    --Result: 2015-10-25 02:00:00 +02:00  
    
    
    --Time after 03:00 is regularly presented with the standard time offset (+01:00)    
    SELECT CONVERT(datetime2(0), '2015-10-25T03:01:00', 126)   
    AT TIME ZONE 'Central European Standard Time';  
    --Result: 2015-10-25 03:01:00 +01:00
  
    ```  

일부 정보(표준 시간대 규칙 같은)는 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]의 외부에서 유지관리되고 가끔 변경의 대상이 되기 때문에 **AT TIME ZONE** 함수는 비결정적으로 분류됩니다. 
  
## <a name="examples"></a>예  
  
### <a name="a-add-target-time-zone-offset-to-datetime-without-offset-information"></a>1. 오프셋 정보 없는 날짜/시간에 대상 표준 시간대 오프셋 추가  
 원래 **datetime** 값이 동일한 표준 시간대에서 제공된다는 것을 아는 경우 **AT TIME ZONE**을 사용하여 표준 시간대 규칙에 기반한 오프셋을 추가합니다.  
  
```  
USE AdventureWorks2016;  
GO  
  
SELECT SalesOrderID, OrderDate,   
    OrderDate AT TIME ZONE 'Pacific Standard Time' AS OrderDate_TimeZonePST  
FROM Sales.SalesOrderHeader;  
```  
  
### <a name="b-convert-values-between-different-time-zones"></a>2. 다른 표준 시간대 사이의 값 변환  
 다음 예제에서는 다른 표준 시간대 사이의 값을 변환합니다.  
  
```  
USE AdventureWorks2016;  
GO  
  
SELECT SalesOrderID, OrderDate,   
    OrderDate AT TIME ZONE 'Pacific Standard Time' AS OrderDate_TimeZonePST,  
    OrderDate AT TIME ZONE 'Pacific Standard Time'   
    AT TIME ZONE 'Central European Standard Time' AS OrderDate_TimeZoneCET  
FROM Sales.SalesOrderHeader;  
```  
  
### <a name="c-query-temporal-tables-using-local-time-zone"></a>3. 로컬 표준 시간대를 사용한 쿼리 임시 테이블  
 다음 예제에서는 임시 테이블에서 데이터를 선택합니다.  
  
```  
USE AdventureWorks2016;  
GO  
  
DECLARE @ASOF datetimeoffset;  
SET @ASOF = DATEADD (month, -1, GETDATE()) AT TIME ZONE 'UTC';  
  
-- Query state of the table a month ago projecting period   
-- columns as Pacific Standard Time  
SELECT BusinessEntityID, PersonType, NameStyle, Title,   
    FirstName, MiddleName,  
    ValidFrom AT TIME ZONE 'Pacific Standard Time' 
FROM  Person.Person_Temporal  
FOR SYSTEM_TIME AS OF @ASOF;  
```  
  
## <a name="see-also"></a>참고 항목  
 [날짜 및 시간 형식](../../t-sql/data-types/date-and-time-types.md)   
 [날짜 및 시간 데이터 형식 및 함수 &#40;Transact-SQL&#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md)  
  
  
