---
title: Expanded-qname (XQuery) | Microsoft Docs
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
- expanded-QName function
- fn:expanded-QName function
ms.assetid: b8377042-95cc-467b-9ada-fe43cebf4bc3
caps.latest.revision: 19
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: b76f85fae2f01322838c40b79227da896fabd01c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33077770"
---
# <a name="functions-related-to-qnames---expanded-qname"></a>관련 된 Qname-Expanded-qname 함수
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  URI에 지정 된 네임 스페이스를 가진 xs: qname 유형 값을 반환 된 *$paramURI* 에 지정 된 로컬 이름이 *$paramLocal*합니다. 경우 *$paramURI* 은 빈 문자열이 나 빈 시퀀스 이면 네임 스페이스를 나타냅니다.  
  
## <a name="syntax"></a>구문  
  
```  
fn:expanded-QName($paramURI as xs:string?, $paramLocal as xs:string?) as xs:QName?  
```  
  
## <a name="arguments"></a>인수  
 *$paramURI*  
 QName의 네임스페이스 URI입니다.  
  
 *$paramLocal*  
 QName의 로컬 이름 부분입니다.  
  
## <a name="remarks"></a>주의  
 다음에 적용 된 **expanded-qname ()** 함수:  
  
-   경우는 *$paramLocal* 지정한 값이 xs: ncname 유형에 맞는 어휘로 구성, 빈 시퀀스가 반환 되 고 동적 오류를 나타냅니다.  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서는 xs:QName 유형을 다른 유형으로 변환할 수 없습니다. 이 인해는 **expanded-qname ()** 함수는 XML 생성에 사용할 수 없습니다. 예를 들어 `<e> expanded-QName(…) </e>`과 같은 노드를 생성할 때 값은 형식화되지 않아야 합니다. 형식화되면 `expanded-QName()`이 반환한 xs:QName 유형 값을 xdt:untypedAtomic으로 변환해야 하기 때문입니다. 앞에서 말했듯이 변환 기능은 지원되지 않습니다. 해결 방법은 이 항목 뒷부분의 예에 나와 있습니다.  
  
-   기존의 QName 유형 값을 수정하거나 비교할 수 있습니다. 예를 들어 `/root[1]/e[1] eq expanded-QName("http://nsURI" "myNS")` 요소의 값과 비교 <`e`>를 반환한 QName과는 **expanded-qname ()** 함수입니다.  
  
## <a name="examples"></a>예  
 이 항목에서는 다양 한 저장 된 XML 인스턴스에 대 한 XQuery 예 **xml** 유형 열에는 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] 데이터베이스입니다.  
  
### <a name="a-replacing-a-qname-type-node-value"></a>1. QName 유형 노드 값 바꾸기  
 이 예에서는 QName 유형 요소 노드의 값을 수정하는 방법을 보여 줍니다. 이 예에서는 다음을 수행합니다.  
  
-   QName 유형의 요소를 정의하는 XML 스키마 컬렉션을 만듭니다.  
  
-   있는 테이블을 만듭니다는 **xml** XML 스키마 컬렉션을 사용 하 여 유형 열입니다.  
  
-   테이블에 XML 인스턴스를 저장합니다.  
  
-   사용 하 여는 **modify ()** 인스턴스에서 QName 유형 요소 값을 수정 하는 xml 데이터 형식의 메서드. **expanded-qname ()** 함수는 새 QName 유형 값을 생성 하는 데 사용 됩니다.  
  
```  
-- If XML schema collection (if exists)  
-- drop xml schema collection SC  
-- go  
-- Create XML schema collection  
CREATE XML SCHEMA COLLECTION SC AS N'  
<schema xmlns="http://www.w3.org/2001/XMLSchema"  
    xmlns:xs="http://www.w3.org/2001/XMLSchema"   
    targetNamespace="QNameXSD"   
      xmlns:xqo="QNameXSD" elementFormDefault="qualified">  
      <element name="Root" type="xqo:rootType" />  
      <complexType name="rootType">  
            <sequence minOccurs="1" maxOccurs="1">  
                        <element name="ElemQN" type="xs:QName" />  
            </sequence>  
      </complexType>  
</schema>'  
go  
-- Create table.  
CREATE TABLE T( XmlCol xml(SC) )  
-- Insert sample XML instnace  
INSERT INTO T VALUES ('  
<Root xmlns="QNameXSD" xmlns:ns="http://myURI">  
      <ElemQN>ns:someName</ElemQN>  
</Root>')  
go  
-- Verify the insertion  
SELECT * from T  
go  
-- Result  
<Root xmlns="QNameXSD" xmlns:ns="http://myURI">  
  <ElemQN>ns:someName</ElemQN>  
</Root>   
```  
  
 다음 쿼리에서 <`ElemQN`>를 사용 하 여 요소 값이 바뀝니다는 **modify ()** 하는 xml 데이터 형식 및 표시 된 것 처럼 XML DML의 대체 값입니다.  
  
```  
-- the value.  
UPDATE T   
SET XmlCol.modify('  
  declare default element namespace "QNameXSD";   
  replace value of /Root[1]/ElemQN   
  with expanded-QName("http://myURI", "myLocalName") ')  
go  
-- Verify the result  
SELECT * from T  
go  
```  
  
 다음은 결과입니다. QName 유형의 <`ElemQN`> 요소에 새로운 값이 있습니다.  
  
```  
<Root xmlns="QNameXSD" xmlns:ns="urn">  
  <ElemQN xmlns:p1="http://myURI">p1:myLocalName</ElemQN>  
</Root>  
```  
  
 다음 문에서는 예에 사용된 개체를 제거합니다.  
  
```  
-- Cleanup  
DROP TABLE T  
go  
drop xml schema collection SC  
go  
```  
  
### <a name="b-dealing-with-the-limitations-when-using-the-expanded-qname-function"></a>2. expanded-QName() 함수 사용 시 제한 사항 해결  
 **Expanded-qname** 함수는 XML 생성에 사용할 수 없습니다. 다음은 이에 대한 예입니다. 이 제한 사항을 해결하기 위해 이 예에서는 먼저 노드를 삽입한 다음 해당 노드를 수정합니다.  
  
```  
-- if exists drop the table T  
--drop table T  
-- go  
-- Create XML schema collection  
-- DROP XML SCHEMA COLLECTION SC  
-- go  
CREATE XML SCHEMA COLLECTION SC AS '  
<schema xmlns="http://www.w3.org/2001/XMLSchema">  
      <element name="root" type="QName" nillable="true"/>  
</schema>'  
go  
 -- Create table T with a typed xml column (using the XML schema collection)  
CREATE TABLE T (xmlCol XML(SC))  
go  
-- Insert an XML instance.  
insert into T values ('<root xmlns:a="http://someURI">a:b</root>')  
 go  
-- Verify  
SELECT *   
FROM T  
```  
  
 다음 예에서는 또 다른 <`root`> 요소를 추가하려고 하지만 XML 생성에는 expanded-QName() 함수가 지원되지 않으므로 실패합니다.  
  
```  
update T SET xmlCol.modify('  
insert <root>{expanded-QName("http://ns","someLocalName")}</root> as last into / ')  
go  
```  
  
 이에 대한 해결 방법은 먼저 <`root`> 요소의 값으로 인스턴스를 삽입한 다음 수정하는 것입니다. 이 예에서는 <`root`> 요소를 삽입할 때 nil 초기 값이 사용됩니다. 이 예의 XML 스키마 컬렉션에서는 <`root`> 요소에 nil 값을 사용할 수 있습니다.  
  
```  
update T SET xmlCol.modify('  
insert <root xsi:nil="true"/> as last into / ')  
go  
-- now replace the nil value with another QName.  
update T SET xmlCol.modify('  
replace value of /root[last()] with expanded-QName("http://ns","someLocalName") ')  
go  
 -- verify   
SELECT * FROM T  
go  
-- result  
<root>b</root>  
```  
  
 `<root xmlns:a="http://someURI">a:b</root>`  
  
 `<root xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:p1="http://ns">p1:someLocalName</root>`  
  
 다음 쿼리와 같이 QName 값을 비교할 수 있습니다. 쿼리는만 반환는 <`root`>에서 반환 된 값을 입력 하는 해당 값은 QName이 일치 하는 요소는 **expanded-qname ()** 함수.  
  
```  
SELECT xmlCol.query('  
    for $i in /root  
    return  
       if ($i eq expanded-QName("http://ns","someLocalName") ) then  
          $i  
       else  
          ()')  
FROM T  
```  
  
### <a name="implementation-limitations"></a>구현 시 제한 사항  
 한 가지 제한:는 **expanded-qname ()** 함수는 빈 시퀀스는 두 번째 인수로 사용 하며 두 번째 인수가 올바르지 않을 때 런타임 오류를 발생 시키는 대신 빈 반환 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Qname 관련 함수 &#40;XQuery&#41;](http://msdn.microsoft.com/library/7e07eb26-f551-4b63-ab77-861684faff71)  
  
  
