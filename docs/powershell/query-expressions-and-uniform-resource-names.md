---
title: "쿼리 식 및 URN | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: powershell
ms.service: 
ms.component: powershell
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- query expressions
- unique resource names
- URN
ms.assetid: e0d30dbe-7daf-47eb-8412-1b96792b6fb9
caps.latest.revision: 14
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 70426dcb9e6ca23d3e8de717fe7b9430155c7243
ms.contentlocale: ko-kr
ms.lasthandoff: 07/31/2017

---
# <a name="query-expressions-and-uniform-resource-names"></a>쿼리 식 및 URN
  SMO( [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Management Object) 모델 및 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] PowerShell 스냅인은 XPath 식과 유사한 두 가지 유형의 식 문자열을 사용합니다. 쿼리 식은 개체 모델 계층 구조에 있는 하나 이상의 개체를 열거하는 데 사용되는 조건 집합을 지정하는 문자열입니다. URN(Uniform Resource Name)은 단일 개체를 고유하게 식별하는 특정 유형의 쿼리 식 문자열입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Object1[<FilterExpression1>]/ ... /ObjectN[<FilterExpressionN>]  
  
<FilterExpression>::=  
<PropertyExpression> [and <PropertyExpression>][...n]  
  
<PropertyExpression>::=  
      @BooleanPropertyName=true()  
 | @BooleanPropertyName=false()  
 | contains(@StringPropertyName, 'PatternString')  
  | @StringPropertyName='String'  
 | @DatePropertyName=datetime('DateString')  
 | is_null(@PropertyName)  
 | not(<PropertyExpression>)  
  
```  
  
## <a name="arguments"></a>인수  
 *개체*  
 식 문자열의 Object 노드에서 나타내는 개체 유형을 지정합니다. 각 개체는 이러한 SMO 개체 모델 네임스페이스의 컬렉션 클래스를 나타냅니다.  
  
 <xref:Microsoft.SqlServer.Management.Smo>  
  
 <xref:Microsoft.SqlServer.Management.Smo.Agent>  
  
 <xref:Microsoft.SqlServer.Management.Smo.Broker>  
  
 <xref:Microsoft.SqlServer.Management.Smo.Mail>  
  
 <xref:Microsoft.SqlServer.Management.Dmf>  
  
 <xref:Microsoft.SqlServer.Management.Facets>  
  
 <xref:Microsoft.SqlServer.Management.RegisteredServers>  
  
 <xref:Microsoft.SqlServer.Management.Smo.RegSvrEnum>  
  
 예를 들어 **ServerCollection** 클래스에 대한 서버, **DatabaseCollection** 클래스에 대한 데이터베이스를 지정합니다.  
  
 @*PropertyName*  
 *Object*에서 지정된 개체와 연결되는 클래스 속성 중 하나의 이름을 지정합니다. 속성 이름은 @ 문자로 시작해야 합니다. 예를 들어 **Database** 클래스 속성인 **IsAnsiNull**에 대해 @IsAnsiNull을 지정합니다.  
  
 @*BooleanPropertyName*=true()  
 지정된 부울 속성이 TRUE로 설정된 개체를 모두 열거합니다.  
  
 @*BooleanPropertyName*=false()  
 지정된 부울 속성이 FALSE로 설정된 개체를 모두 열거합니다.  
  
 contains(@*StringPropertyName*, '*PatternString*')  
 지정된 문자열 속성에 '*PatternString*'에 지정된 문자열 집합이 하나 이상 포함되어 있는 개체를 모두 열거합니다.  
  
 @*StringPropertyName*='*PatternString*'  
 지정된 문자열 속성 값이 '*PatternString*'에 지정된 문자 패턴과 정확하게 같은 개체를 모두 열거합니다.  
  
 @*DatePropertyName*= datetime('*DateString*')  
 지정된 날짜 속성 값이 '*DateString*'에 지정된 날짜와 일치하는 개체를 모두 열거합니다. *DateString* 은 yyyy-mm-dd hh:mi:ss.mmm 형식을 따라야 합니다.  
  
|||  
|-|-|  
|yyyy|4자리 연도|  
|mm|두 자리 월(01 - 12)|  
|dd|두 자리 날짜(01 - 31)|  
|hh|24시간제를 사용하는 두 자리 시간(01 - 23)|  
|mi|두 자리 분(01 - 59)|  
|ss|두 자리 초(01 - 59)|  
|mmm|밀리초 수(001 - 999)|  
  
 이 형식으로 지정된 날짜를 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에 저장된 모든 날짜 형식에 대해 평가할 수 있습니다.  
  
 is_null(@*PropertyName*)  
 지정된 속성 값이 NULL인 개체를 모두 열거합니다.  
  
 not(\<*PropertyExpression*>)  
 *PropertyExpression*의 평가 값을 부정하고 *PropertyExpression*에 지정된 조건과 일치하지 않는 개체를 모두 열거합니다. 예를 들어 not(contains(@Name, 'xyz'))는 이름에 xyz 문자열이 없는 개체를 모두 열거합니다.  
  
## <a name="remarks"></a>주의  
 쿼리 식은 SMO 모델 계층 구조에 있는 노드를 열거하는 문자열입니다. 각 노드에는 해당 노드에서 열거되는 개체를 결정하는 조건을 지정하는 필터 식이 있습니다. 쿼리 식은 XPath 식 언어에서 모델링됩니다. 쿼리 식은 XPath에서 지원하는 작은 식 집합을 구현하고 XPath에 없는 일부 확장도 포함합니다. XPath 식은 XML 문서에서 하나 이상의 태그를 열거하는 데 사용되는 조건 집합을 지정하는 문자열입니다. XPath에 대한 자세한 내용은 [W3C XPath Language](http://www.w3.org/TR/xpath20/)를 참조하십시오.  
  
 쿼리 식은 Server 개체에 대한 절대 참조로 시작해야 합니다. /로 시작하는 상대 식은 사용할 수 없습니다. 쿼리 식에 지정된 개체 시퀀스는 관련 개체 모델에 있는 컬렉션 개체의 계층 구조를 따라야 합니다. 예를 들어 Microsoft.SqlServer.Management.Smo 네임스페이스의 개체를 참조하는 쿼리 식은 Server 노드로 시작하고 그 다음에 Database 노드 등이 와야 합니다.  
  
 개체에 대해 *\<FilterExpression>*이 지정되지 않은 경우 해당 노드의 개체가 모두 열거됩니다.  
  
## <a name="uniform-resource-names-urn"></a>URN(Uniform Resource Name)  
 URN은 쿼리 식의 하위 집합입니다. 각 URN은 단일 개체에 대한 정규화된 참조를 형성합니다. 일반적인 URN에서는 Name 속성을 사용하여 각 노드의 단일 개체를 식별합니다. 예를 들어 이 URN은 특정 열을 참조합니다.  
  
```  
Server[@Name='MYCOMPUTER']/Database[@Name='AdventureWorks2012']/Table[@Name='SalesPerson' and @Schema='Sales']/Column[@Name='SalesPersonID']  
```  
  
## <a name="examples"></a>예  
  
### <a name="a-enumerating-objects-using-false"></a>1. false()를 사용하여 개체 열거  
 이 쿼리 식은 **MyComputer** 의 기본 인스턴스에서 **AutoClose**특성이 false로 설정된 데이터베이스를 모두 열거합니다.  
  
```  
Server[@Name='MYCOMPUTER']/Database[@AutoClose=false()]  
```  
  
### <a name="b-enumerating-objects-using-contains"></a>2. contains를 사용하여 개체 열거  
 이 쿼리 식은 대/소문자를 구분하지 않고 이름에 'm' 문자가 있는 데이터베이스를 모두 열거합니다.  
  
```  
Server[@Name='MYCOMPUTER']/Database[@CaseSensitive=false() and contains(@Name, 'm')]   
```  
  
### <a name="c-enumerating-objects-using-not"></a>3. not을 사용하여 개체 열거  
 이 쿼리 식은 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] Production **스키마에 없으며 테이블 이름에 History라는 단어를 포함하는** 테이블을 모두 열거합니다.  
  
```  
Server[@Name='MYCOMPUTER']/Database[@Name='AdventureWorks2012']/Table[not(@Schema='Production') and contains(@Name, 'History')]  
```  
  
### <a name="d-not-supplying-a-filter-expression-for-the-final-node"></a>4. 최종 노드에 대한 필터 식 제공 안 함  
 이 쿼리 식은 **AdventureWorks2012.Sales.SalesPerson** 테이블에서 모든 열을 열거합니다.  
  
```  
Server[@Name='MYCOMPUTER']/Database[@Name='AdventureWorks2012"]/Table[@Schema='Sales' and @Name='SalesPerson']/Columns  
```  
  
### <a name="e-enumerating-objects-using-datetime"></a>5. datetime을 사용하여 개체 열거  
 이 쿼리 식은 특정 시간에 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] 데이터베이스에서 만든 테이블을 모두 열거합니다.  
  
```  
Server[@Name='MYCOMPUTER']/Database[@Name='AdventureWorks2012"]/Table[@CreateDate=datetime('2008-03-21 19:49:32.647')]  
```  
  
### <a name="f-enumerating-objects-using-isnull"></a>6. is_null을 사용하여 개체 열거  
 이 쿼리 식은 마지막 수정 날짜 속성에 대한 NULL이 없는 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] 데이터베이스의 테이블을 모두 열거합니다.  
  
```  
Server[@Name='MYCOMPUTER']/Database[@Name='AdventureWorks2012"]/Table[Not(is_null(@DateLastModified))]  
```  
  
## <a name="see-also"></a>참고 항목  
 [Invoke-PolicyEvaluation cmdlet](../powershell/invoke-policyevaluation-cmdlet.md)   
 [SQL Server Audit&#40;데이터베이스 엔진&#41;](../relational-databases/security/auditing/sql-server-audit-database-engine.md)  
  
  

