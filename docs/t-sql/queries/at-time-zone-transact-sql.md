---
title: "표준 시간대 (Transact SQL)에서 | Microsoft Docs"
ms.date: 11/16/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- AT TIME ZONE
- AT_TIME_ZONE_TSQL
helpviewer_keywords:
- AT TIME ZONE function
ms.assetid: 311f682f-7f1b-43b6-9ea0-24e36b64f73a
caps.latest.revision: 13
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f0983cbd76b1ec3a71985537f098f8faf002b93e
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="at-time-zone-transact-sql"></a>표준시 (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  변환는 *inputdate* 해당 요소에 *datetimeoffset* 대상 표준 시간대에는 값입니다. 경우 *inputdate* 함수를 오프셋된 정보 없이 가정 하 고 표준 시간대 오프셋을 적용 하는 제공 된 *inputdate* 대상 표준 시간대에 값을 제공 합니다. 경우 *inputdate* 으로 제공 되는 *datetimeoffset* 값 보다 **AT TIME ZONE** 절 표준 시간대 변환 규칙을 사용 하 여 대상 표준 시간대로 변환 합니다.  
  
 **표준 시간대에** 구현은 변환 하는 Windows 메커니즘에 의존 **datetime** 시간대에 따른 값입니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
inputdate AT TIME ZONE timezone  
```  
  
## <a name="arguments"></a>인수  
 *inputdate*  
 식으로 확인 될 수 있는 한 **smalldatetime**, **datetime**, **datetime2**, 또는 **datetimeoffset** 값입니다.  
  
 *표준 시간대*  
 대상 표준 시간대의 이름입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Windows 레지스트리에 저장 된 표준 시간대에 의존 합니다. 컴퓨터에 설치 하는 모든 표준 시간대는 다음 레지스트리 하이브에 저장 됩니다: **KEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Time 영역**합니다. 통해 설치 된 표준 시간대의 목록도 표시 되는 [sys.time_zone_info&#40; Transact SQL &#41; ](../../relational-databases/system-catalog-views/sys-time-zone-info-transact-sql.md) 보기.  
  
## <a name="return-types"></a>반환 형식  
 데이터 형식을 반환 **datetimeoffset**  
  
## <a name="return-value"></a>반환 값  
 **datetimeoffset** 대상 표준 시간대에는 값입니다.  
  
## <a name="remarks"></a>주의  
 **표준 시간대에** 변환의 입력된 값에 대 한 특정 규칙을 적용 **smalldatetime**, **datetime** 및 **datetime2** 에 속하는 데이터 형식은 영향을 받는 간격 DST 변경:  
  
-   현지 시간 클록 조정 기간에 따라 달라 집니다 어떤 기간에에서 간격이 클록 미리 설정 된 경우 (일반적으로 1 시간, 하지만 가능 시간대에 따라 30 개 45 분)입니다. 이 간격에 속하는 지정 시간 오프셋으로 변환 되는 경우 *후* DST 변경 합니다.  
  
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
  
- 시계가 다시 설정 하 고, 경우에 1 시간에 현지 시간의 2 시간 상태가 됩니다.  이 경우 겹쳐진된 간격에 속하는 지정 시간 오프셋 표시 됩니다 *전에* 클록 변경:  
  
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

외부 (예: 표준 시간대 규칙) 일부 정보는 유지 관리 하므로 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 가끔 변경 될 수는 **AT TIME ZONE** 함수는 비결 정적으로 분류 됩니다. 
  
## <a name="examples"></a>예  
  
### <a name="a-add-target-time-zone-offset-to-datetime-without-offset-information"></a>1. 날짜 및 시간 오프셋된 정보 없이 대상 표준 시간대 오프셋 추가  
 사용 하 여 **AT TIME ZONE** 것을 알고 있다면 때 시간대 규칙에 따라 오프셋을 추가 하려면 원래 **datetime** 동일한 표준 시간대 값은 제공:  
  
```  
USE AdventureWorks2016;  
GO  
  
SELECT SalesOrderID, OrderDate,   
    OrderDate AT TIME ZONE 'Pacific Standard Time' AS OrderDate_TimeZonePST  
FROM Sales.SalesOrderHeader;  
```  
  
### <a name="b-convert-values-between-different-time-zones"></a>2. 다른 표준 시간대 사이의 값으로 변환  
 다음 예제에서는 서로 다른 표준 시간대 사이의 값으로 변환합니다.  
  
```  
USE AdventureWorks2016;  
GO  
  
SELECT SalesOrderID, OrderDate,   
    OrderDate AT TIME ZONE 'Pacific Standard Time' AS OrderDate_TimeZonePST,  
    OrderDate AT TIME ZONE 'Pacific Standard Time'   
    AT TIME ZONE 'Central European Standard Time' AS OrderDate_TimeZoneCET  
FROM Sales.SalesOrderHeader;  
```  
  
### <a name="c-query-temporal-tables-using-local-time-zone"></a>3. 현지 표준 시간대를 사용 하 여 임시 테이블 쿼리  
 다음 예에서는 예에서는 임시 테이블에서 데이터를 선택 합니다.  
  
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
  
## <a name="see-also"></a>관련 항목:  
 [날짜 및 시간 형식](../../t-sql/data-types/date-and-time-types.md)   
 [날짜 및 시간 데이터 형식 및 함수 &#40; Transact SQL &#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md)  
  
  

