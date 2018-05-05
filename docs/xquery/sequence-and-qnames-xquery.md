---
title: 시퀀스 및 Qname (XQuery) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql
ms.service: ''
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
- sequence [XQuery]
- XQuery, sequence
- QName [XQuery]
- predefined namespaces [XML in SQL Server]
ms.assetid: 3593ac26-dd78-4bf0-bb87-64fbcac5f026
caps.latest.revision: 22
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 8779198816a05844969d269dea8667736c144248
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sequence-and-qnames-xquery"></a>시퀀스 및 QName(XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  이 항목에서는 XQuery의 다음 기본 개념에 대해 설명합니다.  
  
-   시퀀스  
  
-   QName 및 미리 정의된 네임스페이스  
  
## <a name="sequence"></a>시퀀스  
 XQuery에서 식 결과는 XML 노드 목록 및 XSD 원자 유형의 인스턴스로 구성된 시퀀스입니다. 시퀀스의 개별 항목은 항목으로 참조됩니다. 시퀀스의 항목은 다음 중 하나일 수 있습니다.  
  
-   요소, 특성, 텍스트, 처리 명령, 주석 또는 문서와 같은 노드  
  
-   XSD 예제 유형의 인스턴스와 같은 원자 값  
  
 예를 들어 다음 쿼리는 두 개의 요소 노드 항목의 시퀀스를 생성합니다.  
  
```  
SELECT Instructions.query('  
     <step1> Step 1 description goes here</step1>,  
     <step2> Step 2 description goes here </step2>  
') AS Result  
FROM Production.ProductModel  
WHERE ProductModelID=7;  
  
```  
  
 다음은 결과입니다.  
  
```  
<step1> Step 1 description goes here </step1>  
<step2> Step 2 description goes here </step2>   
```  
  
 이전 쿼리에서 `,` 구조의 끝에 있는 쉼표(`<step1>`)는 시퀀스 생성자이며 필수 요소입니다. 결과에 있는 공백은 설명용으로만 추가된 것이며 이 설명서의 모든 결과 예에 포함되어 있습니다.  
  
 다음은 시퀀스에 대해 알아야 하는 추가 정보입니다.  
  
-   시퀀스 내의 쿼리 결과에 다른 시퀀스가 포함된 경우 포함된 시퀀스는 컨테이너 시퀀스에 결합됩니다. 예를 들어 시퀀스 ((1,2, (3,4,5)),6)은 데이터 모델에 (1, 2, 3, 4, 5, 6)으로 결합됩니다.  
  
    ```  
    DECLARE @x xml;  
    SET @x = '';  
    SELECT @x.query('(1,2, (3,4,5)),6');  
    ```  
  
-   빈 시퀀스는 항목이 포함되지 않은 시퀀스입니다. 이러한 시퀀스는 "()"로 표시됩니다.  
  
-   항목이 하나만 있는 시퀀스는 원자 값으로 취급되며 그 반대도 마찬가지입니다. 즉, (1) = 1입니다.  
  
 이 구현에서 시퀀스는 유형이 같아야 합니다. 즉, 원자 값의 시퀀스나 노드 시퀀스가 포함됩니다. 예를 들어 다음은 유효한 시퀀스입니다.  
  
```  
DECLARE @x xml;  
SET @x = '';  
-- Expression returns a sequence of 1 text node (singleton).  
SELECT @x.query('1');  
-- Expression returns a sequence of 2 text nodes  
SELECT @x.query('"abc", "xyz"');  
-- Expression returns a sequence of one atomic value. data() returns  
-- typed value of the node.  
SELECT @x.query('data(1)');  
-- Expression returns a sequence of one element node.   
-- In the expression XML construction is used to construct an element.  
SELECT @x.query('<x> {1+2} </x>');  
```  
  
 다음 쿼리에서는 유형이 다른 시퀀스가 지원되지 않기 때문에 오류를 반환합니다.  
  
```  
SELECT @x.query('<x>11</x>, 22');  
```  
  
## <a name="qname"></a>QName  
 XQuery의 모든 식별자는 QName입니다. QName은 네임스페이스 접두사 및 로컬 이름으로 구성됩니다. 이 구현에서 XQuery에 있는 변수 이름은 QName이며 접두사가 포함될 수 없습니다.  
  
 예를 들어 다음 쿼리가 지정 되어에 대해 형식화 되지 않은 **xml** 변수:  
  
```  
DECLARE @x xml;  
SET @x = '<Root><a>111</a></Root>';  
SELECT @x.query('/Root/a');  
```  
  
 식(`/Root/a`)에서 `Root` 및 `a`는 QName입니다.  
  
 다음 예제에서는 쿼리를 지정에 대해 형식화 된 **xml** 열입니다. 쿼리는 모든 반복 \<단계 > 첫 번째 작업 센터 위치에 있는 요소입니다.  
  
```  
SELECT Instructions.query('  
   declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
for $Step in /AWMI:root/AWMI:Location[1]/AWMI:step  
      return  
           string($Step)   
') AS Result  
FROM Production.ProductModel  
WHERE ProductModelID=7;  
```  
  
 쿼리 식에서 다음에 유의하십시오.  
  
-   `AWMI root`, `AWMI:Location`, `AWMI:step` 및 `$Step`은 모두 QName입니다. `AWMI`는 접두사이고 `root`, `Location` 및 `Step`은 모두 로컬 이름입니다.  
  
-   `$step` 변수는 QName이며 접두사가 없습니다.  
  
 다음 네임스페이스는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 지원되는 XQuery에서 사용하도록 미리 정의되어 있습니다.  
  
|접두사|URI|  
|------------|---------|  
|xs|http://www.w3.org/2001/XMLSchema|  
|xsi|http://www.w3.org/2001/XMLSchema-instance|  
|xdt|http://www.w3.org/2004/07/xpath-datatypes|  
|fn|http://www.w3.org/2004/07/xpath-functions|  
|(접두사 없음)|`urn:schemas-microsoft-com:xml-sql`|  
|sqltypes|http://schemas.microsoft.com/sqlserver/2004/sqltypes|  
|xml|`http://www.w3.org/XML/1998/namespace`|  
|(접두사 없음)|`http://schemas.microsoft.com/sqlserver/2004/SOAP`|  
  
 사용자가 만드는 모든 데이터베이스에는 **sys** XML 스키마 컬렉션입니다. 이 컬렉션은 사용자가 만든 XML 스키마 컬렉션에서 액세스할 수 있도록 이러한 스키마를 준비해 둡니다.  
  
> [!NOTE]  
>  이 구현은 지원 하지 않습니다는 `local` 에 있는 XQuery 사양에 설명 된 대로 접두사 http://www.w3.org/2004/07/xquery-local-functions합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [XQuery 기초](../xquery/xquery-basics.md)  
  
  
