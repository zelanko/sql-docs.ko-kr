---
title: "SQL 이스케이프 시퀀스를 사용 하 여 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 00f9e25a-088e-4ac6-aa75-43eacace8f03
caps.latest.revision: "25"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: df370e44bf2af1a41d926866ea0c2427cccffe59
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/18/2017
---
# <a name="using-sql-escape-sequences"></a>SQL 이스케이프 시퀀스 사용
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] JDBC API에 정의 된 SQL 이스케이프 시퀀스 사용을 지원 합니다. 이스케이프 시퀀스는 SQL 문 내에서 SQL 문자열의 이스케이프 부분이 다르게 처리되었음을 드라이버에 알리는 데 사용됩니다. SQL 문자열의 이스케이프 부분은 JDBC 드라이버에서 처리될 때 SQL Server에서 이해할 수 있는 SQL 코드로 변환됩니다.  
  
 JDBC API에 필요한 이스케이프 시퀀스에는 다음 5가지 종류가 있으며 이들 모두 JDBC 드라이버에서 지원됩니다.  
  
-   LIKE 와일드카드 리터럴  
  
-   함수 처리  
  
-   날짜 및 시간 리터럴  
  
-   저장 프로시저 호출  
  
-   외부 조인  
  
-   Limit 이스케이프 구문  
  
 JDBC 드라이버에서 사용하는 이스케이프 시퀀스 구문은 다음과 같습니다.  
  
 `{keyword ...parameters...}`  
  
> [!NOTE]  
>  JDBC 드라이버의 경우 SQL 이스케이프 처리가 항상 설정되어 있습니다.  
  
 다음 섹션에서는 이스케이프 시퀀스의 5가지 종류와 JDBC 드라이버에서 이러한 이스케이프 시퀀스를 지원하는 방식에 대해 설명합니다.  
  
## <a name="like-wildcard-literals"></a>LIKE 와일드카드 리터럴  
 JDBC 드라이버가 지 원하는 `{escape 'escape character'}` LIKE 절 와일드 카드를 리터럴로 사용에 대 한 구문입니다. 예를 들어 다음 코드는 col3의 값을 반환하는데 여기서 col2의 값은 문자 그대로 밑줄(와일드카드를 사용하지 않음)로 시작됩니다.  
  
```  
ResultSet rst = stmt.executeQuery("SELECT col3 FROM test1 WHERE col2   
LIKE '\\_%' {escape '\\'}");  
```  
  
> [!NOTE]  
>  이스케이프 시퀀스는 SQL 문의 끝에 있어야 합니다. 명령 문자열에 SQL 문이 여러 개 있을 경우 이스케이프 시퀀스는 각 관련 SQL 문의 끝에 있어야 합니다.  
  
## <a name="function-handling"></a>함수 처리  
 JDBC 드라이버는 다음 구문을 사용하여 SQL 문에서 함수 이스케이프 시퀀스를 지원합니다.  
  
```  
{fn functionName}  
```  
  
 여기서 `functionName` 는 JDBC 드라이버에서 지원 되는 함수입니다. 예를 들어  
  
```  
SELECT {fn UCASE(Name)} FROM Employee  
```  
  
 다음 표는 함수 이스케이프 시퀀스를 사용할 때 JDBC 드라이버에서 지원하는 다양한 함수를 보여 줍니다.  
  
|문자열 함수|숫자 함수|Datetime 함수|시스템 함수|  
|----------------------|-----------------------|------------------------|----------------------|  
|ASCII<br /><br /> CHAR<br /><br /> CONCAT<br /><br /> DIFFERENCE<br /><br /> INSERT<br /><br /> LCASE<br /><br /> LEFT<br /><br /> LENGTH<br /><br /> LOCATE<br /><br /> LTRIM<br /><br /> REPEAT<br /><br /> REPLACE<br /><br /> RIGHT<br /><br /> RTRIM<br /><br /> SOUNDEX<br /><br /> SPACE<br /><br /> SUBSTRING<br /><br /> UCASE|ABS<br /><br /> ACOS<br /><br /> ASIN<br /><br /> ATAN<br /><br /> ATAN2<br /><br /> CEILING<br /><br /> COS<br /><br /> COT<br /><br /> DEGREES<br /><br /> EXP<br /><br /> FLOOR<br /><br /> LOG<br /><br /> LOG10<br /><br /> MOD<br /><br /> PI<br /><br /> POWER<br /><br /> RADIANS<br /><br /> RAND<br /><br /> ROUND<br /><br /> SIGN<br /><br /> SIN<br /><br /> SQRT<br /><br /> TAN<br /><br /> TRUNCATE|CURDATE<br /><br /> CURTIME<br /><br /> DAYNAME<br /><br /> DAYOFMONTH<br /><br /> DAYOFWEEK<br /><br /> DAYOFYEAR<br /><br /> EXTRACT<br /><br /> HOUR<br /><br /> MINUTE<br /><br /> MONTH<br /><br /> MONTHNAME<br /><br /> NOW<br /><br /> QUARTER<br /><br /> SECOND<br /><br /> TIMESTAMPADD<br /><br /> TIMESTAMPDIFF<br /><br /> WEEK<br /><br /> YEAR|DATABASE<br /><br /> IFNULL<br /><br /> User|  
  
> [!NOTE]  
>  데이터베이스에서 지원하지 않는 함수를 사용하려고 하면 오류가 발생합니다.  
  
## <a name="date-and-time-literals"></a>날짜 및 시간 리터럴  
 날짜, 시간 및 타임스탬프 리터럴에 대한 이스케이프 구문은 다음과 같습니다.  
  
```  
{literal-type 'value'}  
```  
  
 여기서 `literal-type` 다음 중 하나입니다.  
  
|리터럴 형식|Description|값 형식|  
|------------------|-----------------|------------------|  
|d|날짜|yyyy-mm-dd|  
|t|Time|hh:mm:ss [1]|  
|ts|타임스탬프|yyyy-mm-dd hh:mm:ss[.f...]|  
  
 예를 들어  
  
```  
UPDATE Orders SET OpenDate={d '2005-01-31'}   
WHERE OrderID=1025  
```  
  
## <a name="stored-procedure-calls"></a>저장 프로시저 호출  
 JDBC 드라이버가 지 원하는 `{? = call proc_name(?,...)}` 및 `{call proc_name(?,...)}` 이스케이프 구문을 반환 매개 변수를 처리 해야 하는지 여부에 따라 저장된 프로시저 호출에 대 한 합니다.  
  
 프로시저는 데이터베이스에 저장된 실행 가능한 개체로서 일반적으로 미리 컴파일된 하나 이상의 SQL 문입니다. 저장 프로시저 호출을 위한 이스케이프 시퀀스 구문은 다음과 같습니다.  
  
```  
{[?=]call procedure-name[([parameter][,[parameter]]...)]}  
```  
  
 여기서 `procedure-name` 저장된 프로시저의 이름을 지정 하 고 `parameter` 저장된 프로시저 매개 변수를 지정 합니다.  
  
 사용 하는 방법에 대 한 자세한 내용은 `call` 이스케이프 시퀀스 저장된 프로시저를 참조 하십시오. [저장 프로시저와 함께 Using 문을](../../connect/jdbc/using-statements-with-stored-procedures.md)합니다.  
  
## <a name="outer-joins"></a>외부 조인  
 JDBC 드라이버는 SQL92 LEFT, RIGHT 및 FULL OUTER JOIN 구문을 지원합니다. 외부 조인에 대한 이스케이프 시퀀스는 다음과 같습니다.  
  
```  
{oj outer-join}  
```  
  
 여기서 outer-join은 다음과 같습니다.  
  
```  
table-reference {LEFT | RIGHT | FULL} OUTER JOIN    
{table-reference | outer-join} ON search-condition  
```  
  
 여기서 `table-reference` 은 테이블 이름 및 `search-condition` 이 테이블에 대 한 사용 하려는 조인 조건입니다.  
  
 예를 들어  
  
```  
SELECT Customers.CustID, Customers.Name, Orders.OrderID, Orders.Status   
   FROM {oj Customers LEFT OUTER JOIN   
      Orders ON Customers.CustID=Orders.CustID}   
   WHERE Orders.Status='OPEN'  
```  
  
 JDBC 드라이버에서 지원하는 외부 조인 이스케이프 시퀀스는 다음과 같습니다.  
  
-   왼쪽 우선 외부 조인  
  
-   오른쪽 우선 외부 조인  
  
-   완전 외부 조인  
  
-   중첩된 외부 조인  
  
## <a name="limit-escape-syntax"></a>Limit 이스케이프 구문  
  
> [!NOTE]  
>  LIMIT 이스케이프 구문만 지원 됩니다 Microsoft JDBC Driver 4.2에서 (또는 그 이상) for SQL Server JDBC 4.1 이상을 사용 하는 경우.  
  
 LIMIT에 대한 이스케이프 구문은 다음과 같습니다.  
  
```  
LIMIT <rows> [OFFSET <row offset>]  
```  
  
 이스케이프 구문은 두 부분으로 구성 되어 있습니다: \< *행*> 필수 이며 반환할 행 수를 지정 합니다. 오프셋 및 \< *행 오프셋*> 선택 사항이 며 행 반환을 시작 하기 전에 건너뛸 행 수를 지정 합니다. JDBC 드라이버는 LIMIT 대신 TOP를 사용하도록 쿼리를 변환하여 필수 요소만 지원합니다. SQL Server는 LIMIT 절을 지원하지 않습니다. **JDBC 드라이버에서 선택적 없는지 \<r o w > 및 사용 하는 경우 드라이버에서 예외가 throw 됩니다**합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [JDBC 드라이버에서 문 사용](../../connect/jdbc/using-statements-with-the-jdbc-driver.md)  
  
  
