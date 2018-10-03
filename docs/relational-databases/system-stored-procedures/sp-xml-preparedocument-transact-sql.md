---
title: sp_xml_preparedocument (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_xml_preparedocument_TSQL
- sp_xml_preparedocument
dev_langs:
- TSQL
helpviewer_keywords:
- sp_xml_preparedocument
ms.assetid: 95f41cff-c52a-4182-8ac6-bf49369d214c
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: c9b955f59cb1c7813be28c7edd46b32d0c8e44b1
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47735471"
---
# <a name="spxmlpreparedocument-transact-sql"></a>sp_xml_preparedocument(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  입력으로 제공되는 XML 텍스트를 읽고 MSXML 파서(Msxmlsql.dll)를 사용하여 이 텍스트의 구문을 분석한 다음 구문 분석된 문서를 사용할 수 있는 상태로 제공합니다. 이 구문 분석된 문서는 요소, 특성, 텍스트 및 주석 등 XML 문서의 다양한 노드를 트리로 나타낸 것입니다.  
  
 **sp_xml_preparedocument** XML 문서의 새로 생성된 된 내부 표현에 액세스를 사용할 수 있는 핸들을 반환 합니다. 이 핸들은 핸들을 실행 하 여 무효화 될 때까지 또는 세션의 기간 동안 유효 **sp_xml_removedocument**합니다.  
  
> [!NOTE]  
>  구문 분석된 문서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 내부 캐시에 저장됩니다. MSXML 파서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 사용할 수 있는 총 메모리의 8분의 1을 사용합니다. 메모리 부족을 방지 하려면 **sp_xml_removedocument** 메모리를 확보 합니다.  
  
> [!NOTE]  
>  에 대 한 이전 버전과 호환성을 위해 **sp_xml_preparedocument** 축소 (char(13)) 및 LF (이러한 문자를 엔터티 화 하는 경우에 특성에 char(10)) 문자가 있습니다.  
  
> [!NOTE]  
>  호출 하 여 XML 파서가 **sp_xml_preparedocument** 내부 Dtd 및 엔터티 선언을 구문 분석할 수 있습니다. Dtd 및 엔터티를 악의적으로 생성 되므로 선언 서비스 공격의 거부 하는 데 사용할 수, 사용자가 신뢰할 수 없는 소스에서 XML 문서를 직접적 통과 하는 것이 좋습니다 **sp_xml_preparedocument**합니다.  
>   
>  재귀 엔터티 확장 공격을 완화 하기 위해 **sp_xml_preparedocument** 문서의 최상위 수준에서 단일 엔터티에서 확장할 수 있는 엔터티 수를 최대 10,000 개로 제한 합니다. 문자 또는 숫자 엔터티에는 이 제한이 적용되지 않습니다. 이 제한은 많은 엔터티 참조가 포함된 문서의 저장을 허용하지만 하나의 엔터티가 10,000개 확장보다 긴 체인에서 재귀적으로 확장되는 것을 방지합니다.  
  
> [!NOTE]  
>  **sp_xml_preparedocument** 256 번 열 수 있는 요소의 수를 제한 합니다.  

 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_xml_preparedocument  
hdoc   
OUTPUT  
[ , xmltext ]  
[ , xpath_namespaces ]   
```  
  
## <a name="arguments"></a>인수  
 *hdoc*  
 새로 생성된 문서의 핸들입니다. *hdoc* 는 정수입니다.  
  
 [ *xmltext* ]  
 원본 XML 문서입니다. MSXML 파서는 이 XML 문서의 구문을 분석합니다. *xmltext* 는 텍스트 매개 변수: **char**를 **nchar**를 **varchar**를 **nvarchar**, **텍스트**하십시오 **ntext** 하거나 **xml**합니다. 기본값은 NULL이며 이 경우에는 빈 XML 문서의 내부 표현이 생성됩니다.  
  
> [!NOTE]  
>  **sp_xml_preparedocument** 텍스트 또는 형식화 되지 않은 XML만 처리할 수 있습니다. 입력으로 사용할 항목의 값이 형식화된 XML인 경우에는 먼저 형식화되지 않은 새로운 XML 항목 또는 문자열로 캐스팅한 다음 해당 값을 입력으로 전달합니다. 자세한 내용은 [형식화된 XML과 형식화되지 않은 XML 비교](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)를 참조하세요.  
  
 [ *xpath_namespaces* ]  
 OPENXML의 행과 열 XPath 식에 사용되는 네임스페이스 선언을 지정합니다. *xpath_namespaces* 는 텍스트 매개 변수: **char**, **nchar**를 **varchar**, **nvarchar**, **텍스트**하십시오 **ntext** 하거나 **xml**합니다.  
  
 기본값은  **\<xmlns:mp 루트 = "urn: 스키마-microsoft-com:xml-metaprop" >** 합니다. *xpath_namespaces* 올바른 형식의 XML 문서를 사용 하 여 OPENXML의 XPath 식에 사용 되는 접두사에 대 한 네임 스페이스 Uri를 제공 합니다. *xpath_namespaces* 네임 스페이스를 참조 하려면 사용 해야 하는 접두사를 선언 **urn: 스키마-microsoft-com:xml-metaprop**;이 구문 분석 된 XML 요소에 대 한 메타 데이터를 제공 합니다. 이 기술을 사용하여 메타 속성 네임스페이스의 네임스페이스 접두사를 다시 정의할 수 있지만 이 네임스페이스는 손실되지 않습니다. 접두사 **mp** 여전히 유효한 **urn: 스키마-microsoft-com:xml-metaprop** 경우에 *xpath_namespaces* 이러한 선언이 없는 포함 합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 >0(실패)  
  
## <a name="permissions"></a>사용 권한  
 **public** 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-preparing-an-internal-representation-for-a-well-formed-xml-document"></a>1. 올바른 형식의 XML 문서를 위한 내부 표현 준비  
 다음 예에서는 입력으로 제공된 XML 문서의 새로 생성된 내부 표현에 대한 핸들을 반환합니다. `sp_xml_preparedocument` 호출에서 기본 네임스페이스 접두사 매핑이 사용됩니다.  
  
```  
DECLARE @hdoc int;  
DECLARE @doc varchar(1000);  
SET @doc ='  
<ROOT>  
<Customer CustomerID="VINET" ContactName="Paul Henriot">  
   <Order CustomerID="VINET" EmployeeID="5" OrderDate="1996-07-04T00:00:00">  
      <OrderDetail OrderID="10248" ProductID="11" Quantity="12"/>  
      <OrderDetail OrderID="10248" ProductID="42" Quantity="10"/>  
   </Order>  
</Customer>  
<Customer CustomerID="LILAS" ContactName="Carlos Gonzlez">  
   <Order CustomerID="LILAS" EmployeeID="3" OrderDate="1996-08-16T00:00:00">  
      <OrderDetail OrderID="10283" ProductID="72" Quantity="3"/>  
   </Order>  
</Customer>  
</ROOT>';  
--Create an internal representation of the XML document.  
EXEC sp_xml_preparedocument @hdoc OUTPUT, @doc;  
-- Remove the internal representation.  
exec sp_xml_removedocument @hdoc;  
```  
  
### <a name="b-preparing-an-internal-representation-for-a-well-formed-xml-document-with-a-dtd"></a>2. DTD가 있는 올바른 형식의 XML 문서를 위한 내부 표현 준비  
 다음 예에서는 입력으로 제공된 XML 문서의 새로 생성된 내부 표현에 대한 핸들을 반환합니다. 저장 프로시저는 문서에 포함된 DTD에 대해 로드된 문서의 유효성을 검사합니다. `sp_xml_preparedocument` 호출에서 기본 네임스페이스 접두사 매핑이 사용됩니다.  
  
```  
DECLARE @hdoc int;  
DECLARE @doc varchar(2000);  
SET @doc = '  
<?xml version="1.0" encoding="UTF-8" ?>   
<!DOCTYPE root   
[<!ELEMENT root (Customers)*>  
<!ELEMENT Customers EMPTY>  
<!ATTLIST Customers CustomerID CDATA #IMPLIED ContactName CDATA #IMPLIED>]>  
<root>  
<Customers CustomerID="ALFKI" ContactName="Maria Anders"/>  
</root>';  
  
EXEC sp_xml_preparedocument @hdoc OUTPUT, @doc;  
```  
  
### <a name="c-specifying-a-namespace-uri"></a>3. 네임스페이스 URI 지정  
 다음 예에서는 입력으로 제공된 XML 문서의 새로 생성된 내부 표현에 대한 핸들을 반환합니다. 에 대 한 호출 `sp_xml_preparedocument` 유지 합니다 `mp` 메타 속성 네임 스페이스 매핑 접두사를 추가 합니다 `xyz` 네임 스페이스에 대 한 매핑 접두사 `urn:MyNamespace`합니다.  
  
```  
DECLARE @hdoc int;  
DECLARE @doc varchar(1000);  
SET @doc ='  
<ROOT>  
<Customer CustomerID="VINET" ContactName="Paul Henriot">  
   <Order CustomerID="VINET" EmployeeID="5"   
           OrderDate="1996-07-04T00:00:00">  
      <OrderDetail OrderID="10248" ProductID="11" Quantity="12"/>  
      <OrderDetail OrderID="10248" ProductID="42" Quantity="10"/>  
   </Order>  
</Customer>  
<Customer CustomerID="LILAS" ContactName="Carlos Gonzlez">  
   <Order CustomerID="LILAS" EmployeeID="3"   
           OrderDate="1996-08-16T00:00:00">  
      <OrderDetail OrderID="10283" ProductID="72" Quantity="3"/>  
   </Order>  
</Customer>  
</ROOT>'  
--Create an internal representation of the XML document.  
EXEC sp_xml_preparedocument @hdoc OUTPUT, @doc, '<ROOT xmlns:xyz="urn:MyNamespace"/>';  
```  
  
## <a name="see-also"></a>관련 항목  
 <br>[XML 저장 Procedures(Transact-SQL)](../../relational-databases/system-stored-procedures/xml-stored-procedures-transact-sql.md)
 <br>[시스템 저장 Procedures(Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)
 <br>[OPENXML(Transact-SQL)](../../t-sql/functions/openxml-transact-sql.md)
 <br>[sys.dm_exec_xml_handles (TRANSACT-SQL)](../system-dynamic-management-views/sys-dm-exec-xml-handles-transact-sql.md)
 <br>[sp_xml_removedocument (TRANSACT-SQL)](../../relational-databases/system-stored-procedures/sp-xml-removedocument-transact-sql.md)
  
  
