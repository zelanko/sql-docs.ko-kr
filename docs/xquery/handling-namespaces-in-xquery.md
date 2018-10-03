---
title: XQuery의 네임 스페이스 처리 | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- declaring namespaces
- namespaces [XQuery]
- XQuery, namespaces
ms.assetid: 542b63da-4d3d-4ad5-acea-f577730688f1
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 7bbed133da510d27ddfb985a508184ba1cbd94e1
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47730531"
---
# <a name="handling-namespaces-in-xquery"></a>XQuery의 네임스페이스 처리
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  이 항목에서는 쿼리에 있는 네임스페이스를 처리하기 위한 예제를 제공합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-declaring-a-namespace"></a>1. 네임스페이스 선언  
 다음 쿼리는 특정 제품 모델의 제조 단계를 검색합니다.  
  
```  
SELECT Instructions.query('  
     declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
        /AWMI:root/AWMI:Location[1]/AWMI:step  
    ') as x  
FROM Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 다음은 결과의 일부입니다.  
  
```  
<AWMI:step xmlns:AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions">Insert <AWMI:material>aluminum sheet MS-2341</AWMI:material> into the <AWMI:tool>T-85A framing tool</AWMI:tool>. </AWMI:step>  
…  
```  
  
 유의 합니다 **네임 스페이스** 키워드 새 네임 스페이스 접두사를 정의 하는 "AWMI:". 그런 다음 해당 네임스페이스의 범위에 포함되는 모든 요소에 대해 쿼리에서 이 접두사를 사용해야 합니다.  
  
### <a name="b-declaring-a-default-namespace"></a>2. 기본 네임스페이스 선언  
 이전 쿼리에서는 새로운 네임스페이스 접두사가 정의되었습니다. 그런 다음 원하는 XML 구조를 선택하기 위해 쿼리에서 이 접두사를 사용해야 했습니다. 이 방법 외에 다음 수정된 쿼리에서와 같이 네임스페이스를 기본 네임스페이스로 선언할 수 있습니다.  
  
```  
SELECT Instructions.query('  
     declare default element namespace "http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
        /root/Location[1]/step  
    ') as x  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
 다음은 결과입니다.  
  
```  
<step xmlns="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions">Insert <material>aluminum sheet MS-2341</material> into the <tool>T-85A framing tool</tool>. </step>  
…  
```  
  
 이 예에서 정의된 네임스페이스 `"http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions"`는 기본 네임스페이스 또는 비어 있는 네임스페이스를 무시하도록 만들어져 있습니다. 이 때문에 쿼리에 사용된 경로 식에 네임스페이스 접두사가 더 이상 없습니다. 또한 결과에 표시되는 요소 이름에도 네임스페이스 접두사가 더 이상 없습니다. 또한 기본 네임스페이스는 해당 특성을 제외한 모든 요소에 적용됩니다.  
  
### <a name="c-using-namespaces-in-xml-construction"></a>3. XML 생성에 네임스페이스 사용  
 새로운 네임스페이스를 정의할 때 이러한 네임스페이스의 범위에는 쿼리 뿐만 아니라 생성 범위도 포함됩니다. 예를 들어 XML 생성 시 "`declare namespace ...`" 선언을 사용하여 새로운 네임스페이스를 정의한 다음 쿼리 결과 내에 표시되도록 생성하는 모든 요소 및 특성에서 해당 네임스페이스를 사용할 수 있습니다.  
  
```  
SELECT CatalogDescription.query('  
     declare default element namespace "http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     declare namespace myNS="uri:SomeNamespace";<myNS:Result>  
          { /ProductDescription/Summary }  
       </myNS:Result>  
  
    ') as Result  
FROM Production.ProductModel  
where ProductModelID=19  
```  
  
 다음은 결과입니다.  
  
```  
  
      <myNS:Result xmlns:myNS="uri:SomeNamespace">  
  <Summary xmlns="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription">  
   <p1:p xmlns:p1="http://www.w3.org/1999/xhtml">  
     Our top-of-the-line competition mountain bike. Performance-enhancing   
     options include the innovative HL Frame, super-smooth front   
     suspension, and traction for all terrain.</p1:p>  
  </Summary>  
</myNS:Result>  
```  
  
 또는 다음 쿼리에서와 같이 XML 생성의 일부로 사용되는 각 지점에서 네임스페이스를 명시적으로 정의할 수도 있습니다.  
  
```  
SELECT CatalogDescription.query('  
     declare default element namespace "http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
       <myNS:Result xmlns:myNS="uri:SomeNamespace">  
          { /ProductDescription/Summary }  
       </myNS:Result>  
    ') as Result  
FROM Production.ProductModel  
where ProductModelID=19  
```  
  
### <a name="d-construction-using-default-namespaces"></a>4. 기본 네임스페이스를 사용하여 생성  
 또한 생성된 XML에서 사용할 기본 네임스페이스를 정의할 수 있습니다. 예를 들어 다음 쿼리는 기본 네임 스페이스 "uri: somenamespace"를 지정 하는 방법 표시\\와 같은 생성 된 로컬로 명명 된 요소에 대 한 기본값으로 사용 하는 `<Result>` 요소입니다.  
  
```  
SELECT CatalogDescription.query('  
      declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
      declare default element namespace "uri:SomeNamespace";<Result>  
          { /PD:ProductDescription/PD:Summary }  
       </Result>  
  
    ') as Result  
FROM Production.ProductModel  
where ProductModelID=19  
```  
  
 다음은 결과입니다.  
  
```  
  
      <Result xmlns="uri:SomeNamespace">  
  <PD:Summary xmlns:PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription">  
   <p1:p xmlns:p1="http://www.w3.org/1999/xhtml">  
         Our top-of-the-line competition mountain bike. Performance-  
         enhancing options include the innovative HL Frame, super-smooth   
         front suspension, and traction for all terrain.</p1:p>  
  </PD:Summary>  
</Result>  
```  
  
 기본 요소 네임스페이스 또는 빈 네임스페이스를 무시하면 생성된 XML에 있는 모든 로컬로 명명된 요소가 이후에 대체되는 기본 네임스페이스로 바인딩됩니다. 따라서 빈 네임스페이스를 사용할 수 있도록 생성 중인 XML에 유연성이 필요하면 기본 요소 네임스페이스를 무시하지 마십시오.  
  
## <a name="see-also"></a>관련 항목  
 [WITH XMLNAMESPACES를 사용하여 쿼리에 네임스페이스 추가](../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md)   
 [XML 데이터&#40;SQL Server&#41;](../relational-databases/xml/xml-data-sql-server.md)   
 [XQuery 언어 참조&#40;SQL Server&#41;](../xquery/xquery-language-reference-sql-server.md)  
  
  
