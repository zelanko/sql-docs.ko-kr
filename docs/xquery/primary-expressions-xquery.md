---
title: 기본 식 (XQuery) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql
ms.component: xquery
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
dev_langs:
- XML
helpviewer_keywords:
- variable references [XQuery]
- primary expressions [XQuery]
- function calls [XQuery]
- expressions [XQuery], primary
- literals [XQuery]
- context item expressions [XQuery]
ms.assetid: d4183c3e-12b5-4ca0-8413-edb0230cb159
caps.latest.revision: 20
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: d7f9fdcd3eaa54b74366f90891893c88cbf1aa32
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="primary-expressions-xquery"></a>기본 식(XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  XQuery 기본 식에는 리터럴, 변수 참조, 컨텍스트 항목 식, 생성자 및 함수 호출이 들어 있습니다.  
  
## <a name="literals"></a>리터럴  
 XQuery 리터럴은 숫자 또는 문자열 리터럴이 될 수 있습니다. 문자열 리터럴에는 미리 정의된 엔터티 참조를 포함할 수 있는데 엔터티 참조는 문자 시퀀스입니다. 이 시퀀스는 구문상의 의미를 내포할 수도 있는 단일 문자를 나타내는 앰퍼샌드로 시작됩니다. 다음은 XQuery에 대해 미리 정의된 엔터티 참조입니다.  
  
|엔터티 참조|나타내는 대상|  
|----------------------|----------------|  
|&lt;|\<|  
|&gt;|>|  
|&amp;|&|  
|&quot;|"|  
|&apos;|'|  
  
 문자열 리터럴은 문자 참조 즉 유니코드 문자에 대한 XML 스타일의 참조도 포함할 수 있습니다. 이 참조는 해당 10진수 또는 16진수 코드 포인트로 식별됩니다. 유로 기호 문자 참조로 나타낼 수는 예를 들어 "&\#8364;"입니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서는 구문을 분석할 때 기본적으로 XML 버전 1.0을 사용합니다.  
  
### <a name="examples"></a>예  
 다음 예에서는 리터럴과 엔터티 및 문자 참조의 사용법을 보여 줍니다.  
  
 `<'` 및 `'>` 문자에 특별한 의미가 있기 때문에 이 코드는 오류를 반환합니다.  
  
```  
DECLARE @var XML  
SET @var = ''  
SELECT @var.query(' <SalaryRange>Salary > 50000 and < 100000</SalaryRange>')  
GO  
```  
  
 대신 엔터티 참조를 사용하더라도 쿼리는 작동합니다.  
  
```  
DECLARE @var XML  
SET @var = ''  
SELECT @var.query(' <SalaryRange>Salary > 50000 and < 100000</SalaryRange>')  
GO  
```  
  
 다음 예에서는 문자 참조를 사용하여 유로 기호를 나타내는 방법을 보여 줍니다.  
  
```  
DECLARE @var XML  
SET @var = ''  
SELECT @var.query(' <a>€12.50</a>')  
```  
  
 다음은 결과입니다.  
  
 `<a>€12.50</a>`  
  
 다음 예에서 쿼리는 아포스트로피로 구분됩니다. 따라서 문자열 값의 아포스트로피는 두 개의 인접한 아포스트로피로 표시됩니다.  
  
```  
DECLARE @var XML  
SET @var = ''  
SELECT @var.query('<a>I don''t know</a>')  
Go  
```  
  
 다음은 결과입니다.  
  
 `<a>I don't know</a>`  
  
 기본 제공 부울 함수 **true ()** 및 **false ()**, 다음 예제에 나와 있는 것 처럼 부울 값을 나타내기 위해 사용할 수 있습니다.  
  
```  
DECLARE @var XML  
SET @var = ''  
SELECT @var.query('<a>{true()}</a>')  
GO  
```  
  
 직접 요소 생성자는 중괄호 안에서 식을 지정합니다. 그러면 결과 XML에서 해당 값으로 대체됩니다.  
  
 다음은 결과입니다.  
  
 `<a>true</a>`  
  
## <a name="variable-references"></a>변수 참조  
 XQuery의 변수 참조는 $ 부호 다음에 오는 QName입니다. 이러한 구현을 통해 접두사가 없는 변수 참조만 지원됩니다. 예를 들어 다음 쿼리는 FLWOR 식에서 `$i` 변수를 정의합니다.  
  
```  
DECLARE @var XML  
SET @var = '<root>1</root>'  
SELECT @var.query('  
 for $i in /root return data($i)')  
GO  
```  
  
 다음 쿼리는 변수 이름에 네임스페이스 접두사가 추가되었기 때문에 작동하지 않습니다.  
  
```  
DECLARE @var XML  
SET @var = '<root>1</root>'  
SELECT @var.query('  
DECLARE namespace x="http://X";  
for $x:i in /root return data($x:i)')  
GO  
```  
  
 다음 쿼리에서와 같이 SQL 변수를 가리키는 variable () 확장 기능을 사용할 수 있습니다.  
  
```  
DECLARE @price money  
SET @price=2500  
DECLARE @x xml  
SET @x = ''  
SELECT @x.query('<value>{sql:variable("@price") }</value>')  
```  
  
 다음은 결과입니다.  
  
 `<value>2500</value>`  
  
#### <a name="implementation-limitations"></a>구현 시 제한 사항  
 구현 제한 사항은 다음과 같습니다.  
  
-   네임스페이스 접두사가 있는 변수는 지원되지 않습니다.  
  
-   모듈 가져오기는 지원되지 않습니다.  
  
-   외부 변수 선언은 지원되지 않습니다. 이 해결 방법은 사용 하 여 [variable () 함수](../xquery/xquery-extension-functions-sql-variable.md)합니다.  
  
## <a name="context-item-expressions"></a>컨텍스트 항목 식  
 컨텍스트 항목은 현재 경로 식의 컨텍스트에서 처리 중인 항목입니다. 이 항목 식은 문서 노드가 있는 NULL이 아닌 XML 데이터 형식 인스턴스에서 초기화됩니다. XPath 식의 컨텍스트 또는 조건자에 nodes () 메서드에서 변경할 수도 있습니다.  
  
 컨텍스트 항목은 점(.)이 포함된 식에 의해 반환됩니다. 예를 들어 다음 쿼리는 각 <`a`> 요소를 평가하여 `attr` 특성이 있는지 확인합니다. 특성이 존재하면 요소가 반환됩니다. 조건부의 조건은 컨텍스트 노드가 하나의 마침표로 지정되도록 지정합니다.  
  
```  
DECLARE @var XML  
SET @var = '<ROOT>  
<a>1</a>  
<a attr="1">2</a>  
</ROOT>'  
SELECT @var.query('/ROOT[1]/a[./@attr]')  
```  
  
 다음은 결과입니다.  
  
 `<a attr="1">2</a>`  
  
## <a name="function-calls"></a>함수 호출  
 기본 제공 XQuery 함수를 호출할 수 있습니다 및 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] variable () 및 sql: column 함수입니다. 구현 되는 함수의 목록에 대 한 참조 [xml 데이터 형식에 대 한 XQuery 함수](../xquery/xquery-functions-against-the-xml-data-type.md)합니다.  
  
#### <a name="implementation-limitations"></a>구현 시 제한 사항  
 구현 제한 사항은 다음과 같습니다.  
  
-   XQuery 프롤로그의 함수 선언은 지원되지 않습니다.  
  
-   함수 가져오기는 지원되지 않습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [XML 생성 &#40;XQuery&#41;](../xquery/xml-construction-xquery.md)  
  
  
