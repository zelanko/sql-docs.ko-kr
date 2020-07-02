---
title: 오류 처리 (XQuery) | Microsoft Docs
description: XQuery의 오류 처리에 대해 알아보고 동적 오류를 처리 하는 예제를 확인 합니다.
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- static errors
- errors [XQuery]
- XQuery, error handling
- dynamic errors [XQuery]
ms.assetid: 7dee3c11-aea0-4d10-9126-d54db19448f2
author: rothja
ms.author: jroth
ms.openlocfilehash: e7afd7743a7a158738b7b88cd20d33be3220ece0
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85753644"
---
# <a name="error-handling-xquery"></a>오류 처리(XQuery)
[!INCLUDE [SQL Server Azure SQL Database ](../includes/applies-to-version/sqlserver.md)]

  W3C 사양에서는 형식 지정 오류를 정적 또는 동적으로 발생시키고 정적, 동적 및 형식 지정 오류를 정의합니다.  
  
## <a name="compilation-and-error-handling"></a>컴파일 및 오류 처리  
 컴파일 오류는 구문이 잘못된 XQuery 식 및 XML DML 문으로부터 반환됩니다. 컴파일 단계에서는 XQuery 식 및 DML 문의 정적 유형이 올바른지 여부를 확인하고 형식화된 XML에 대한 유형 추론을 위해 XML 스키마를 사용합니다. 유형 안전성 위반으로 인해 런타임에 식이 실패할 수 있는 경우 정적 유형 오류가 발생합니다. 정적 오류는 정수에 문자열을 추가하는 경우와 형식화된 데이터에 대해 존재하지 않는 노드를 쿼리하는 경우를 예로 들 수 있습니다.  
  
 W3C 표준에서 벗어나는 XQuery 런타임 오류는 빈 시퀀스로 변환됩니다. 이러한 시퀀스는 호출 컨텍스트에 따라 빈 XML 또는 NULL로 쿼리 결과에 전파될 수 있습니다.  
  
 올바른 유형으로 명시적으로 캐스팅하면 런타임 캐스트 오류가 빈 시퀀스로 전송되더라도 사용자가 정적 오류를 해결할 수 있습니다.  
  
## <a name="static-errors"></a>정적 오류  
 정적 오류는 [!INCLUDE[tsql](../includes/tsql-md.md)] 오류 메커니즘을 사용하여 반환됩니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 XQuery 형식 지정 오류는 정적으로 반환됩니다. 자세한 내용은 [XQuery 및 정적 형식](../xquery/xquery-and-static-typing.md)지정을 참조 하세요.  
  
## <a name="dynamic-errors"></a>동적 오류  
 XQuery에서 대부분의 동적 오류는 빈 시퀀스("()")로 매핑됩니다. 그러나 XQuery 집계 함수 및 XML DML 유효성 검사 오류의 오버플로 조건 이라는 두 가지 예외가 있습니다. 대부분의 동적 오류는 빈 시퀀스로 매핑됩니다. 그렇지 않으면 XML 인덱스를 활용하는 쿼리 실행 시 오류가 발생할 수 있습니다. 따라서 오류를 발생시키지 않고 효율적으로 쿼리를 실행하기 위해 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]은 동적 오류를 ()로 매핑합니다.  
  
 동적 오류가 조건자 내에서 발생하는 경우에는 오류가 발생하지 않아도 ()가 False로 매핑되기 때문에 의미가 변경되지 않는 경우가 많습니다. 하지만 일부 경우 동적 오류 대신 ()를 반환하면 예기치 않은 결과가 발생할 수 있습니다. 다음은 이를 보여 주는 예입니다.  
  
### <a name="example-using-the-avg-function-with-a-string"></a>예: avg () 함수를 문자열에 사용  
 다음 예에서는 [avg 함수](../xquery/aggregate-functions-avg.md) 를 호출 하 여 세 값의 평균을 계산 합니다. 이들 값 중 하나는 문자열입니다. 이 경우 XML 인스턴스는 형식화되지 않았기 때문에 이 인스턴스의 모든 데이터는 형식화되지 않은 원자 유형입니다. **Avg ()** 함수는 평균을 계산 하기 전에 먼저 이러한 값을 **xs: double** 로 캐스팅 합니다. 그러나 값을 `"Hello"` **xs: double** 로 캐스팅 하 고 동적 오류를 만들 수는 없습니다. 이 경우 동적 오류를 반환 하는 대신 `"Hello"` **xs: double** 로 캐스팅 하면 빈 시퀀스가 발생 합니다. **Avg ()** 함수는이 값을 무시 하 고, 다른 두 값의 평균을 계산 하 고, 150을 반환 합니다.  
  
```  
DECLARE @x xml  
SET @x=N'<root xmlns:myNS="test">  
 <a>100</a>  
 <b>200</b>  
 <c>Hello</c>  
</root>'  
SELECT @x.query('avg(//*)')  
```  
  
### <a name="example-using-the-not-function"></a>예: not 함수 사용  
 조건자에서 [not 함수](../xquery/functions-on-boolean-values-not-function.md) 를 사용 하 `/SomeNode[not(Expression)]` 고 식에서 동적 오류를 발생 시키는 경우 오류 대신 빈 시퀀스가 반환 됩니다. **Not ()** 을 빈 시퀀스에 적용 하면 오류가 아닌 True가 반환 됩니다.  
  
### <a name="example-casting-a-string"></a>예: 문자열 캐스팅  
 다음 예에서 리터럴 문자열 "NaN"은 xs:string으로 캐스팅된 다음 xs:double로 캐스팅됩니다. 결과는 빈 행 집합입니다. 문자열 "NaN"은 xs:double로 성공적으로 캐스팅할 수 없지만 문자열이 먼저 xs:string으로 캐스팅되기 때문에 런타임 전까지는 이를 확인할 수 없습니다.  
  
```  
DECLARE @x XML  
SET @x = ''  
SELECT @x.query(' xs:double(xs:string("NaN")) ')  
GO  
```  
  
 하지만 이 예에서는 정적 형식 지정 오류가 발생합니다.  
  
```  
DECLARE @x XML  
SET @x = ''  
SELECT @x.query(' xs:double("NaN") ')  
GO  
```  
  
#### <a name="implementation-limitations"></a>구현 시 제한 사항  
 **Fn: error ()** 함수는 지원 되지 않습니다.  
  
## <a name="see-also"></a>참고 항목  
 [XQuery 언어 참조 &#40;SQL Server&#41;](../xquery/xquery-language-reference-sql-server.md)   
 [XQuery 기초](../xquery/xquery-basics.md)  
  
  
