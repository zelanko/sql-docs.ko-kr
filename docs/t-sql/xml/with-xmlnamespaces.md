---
title: WITH XMLNAMESPACES(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- WITH_XMLNAMESPACES_TSQL
- WITH XMLNAMESPACES
dev_langs:
- TSQL
helpviewer_keywords:
- adding XML namespaces
- XML namespace declarations [SQL Server]
- clauses [SQL Server], WITH XMLNAMESPACES
- WITH XMLNAMESPACES clause
- declaring XML namespaces
ms.assetid: 3b32662b-566f-454d-b7ca-e247002a9a0b
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: fbc0773b08ea682a9bc8e4803572b9ceae3d28d3
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47808171"
---
# <a name="with-xmlnamespaces"></a>WITH XMLNAMESPACES
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  하나 이상의 XML 네임스페이스를 선언합니다.  
  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
WITH XMLNAMESPACES ( <XML namespace declaration item>  
[ { , <XML namespace declaration item> }...] )   
  
<XML namespace declaration item> ::=  
<xml_namespace_uri> AS <xml_namespace_prefix>  
| <XML default namespace declaration item>  
<xml_namespace_uri> ::= <character string literal>  
```  
  
```  
  
<xml_namespace_prefix> ::= <identifier>  
```  
  
```  
  
<XML default namespace declaration item> ::=  
DEFAULT <xml_namespace_uri>  
  
```  
  
## <a name="arguments"></a>인수  
 *xml_namespace_uri*  
 선언할 XML 네임스페이스를 식별하는 URI(Uniform Resource Identifier)입니다. *xml_namespace_uri*는 SQL 문자열입니다.  
  
 *xml_namespace_prefix*  
 *xml_namespace_uri*에 지정된 네임스페이스 URI 값과 매핑하여 연결할 접두어를 지정합니다. *xml_namespace_prefix*는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 식별자이어야 합니다.  
  
## <a name="remarks"></a>Remarks  
 공통 테이블 식이 포함된 문에 WITH XMLNAMESPACES 절을 사용하는 경우 문에서 WITH XMLNAMESPACES 절이 공통 테이블 식 앞에 와야 합니다.  
  
 다음은 WITH XMLNAMESPACES 절을 사용할 때 적용되는 일반 구문 규칙입니다.  
  
-   각 XML 네임스페이스 선언은 적어도 하나의 XML 기본 네임스페이스 선언 항목을 포함해야 합니다.  
  
-   사용된 각 XML 네임스페이스 접두어는 이름에 콜론(:)이 포함되지 않은 NCName(콜론 없는 이름)이어야 합니다.  
  
-   네임스페이스 접두어를 두 번 정의할 수 없습니다.  
  
-   XML 네임스페이스 접두어와 URI는 대소문자를 구분합니다.  
  
-   XML 네임스페이스 접두어 `xmlns`는 선언할 수 없습니다.  
  
-   XML 네임스페이스 접두어 `xml`은 네임스페이스 URI `'http://www.w3.org/XML/1998/namespace'` 이외의 네임스페이스로 무시할 수 없으며 이 URI에는 다른 접두어를 할당할 수 없습니다.  
  
-   XML 네임스페이스 접두어 `xsi`는 쿼리에서 ELEMENTS XSINIL 지시어를 사용하고 있는 경우 다시 선언할 수 없습니다.  
  
-   URI 문자열 값은 현재 데이터베이스 데이터 정렬 코드 페이지에 따라 인코딩되며 내부적으로 유니코드로 변환됩니다.  
  
-   XML 네임스페이스 URI는 **xs:anyURI**에 사용되는 XSD 공백 축소 규칙에 따라 공백이 축소됩니다. 또한 XML 네임스페이스 URI 값에 대해서는 유효화 또는 비유효화가 수행되지 않습니다.  
  
-   XML 네임스페이스 URI는 유효하지 않은 XML 1.0 문자에 대해 검사되며 U+0007 같은 유효하지 않은 문자가 있을 경우 오류가 발생합니다.  
  
-   XML 네임스페이스 URI는 모든 공백이 축소된 후 길이가 0인 문자열이 될 수 없으며 길이가 0일 경우 "유효하지 않은 빈 네임스페이스 URI" 오류가 발생합니다.  
  
-   XMLNAMESPACES 키워드는 WITH 절의 컨텍스트에서 예약됩니다.  
  
## <a name="examples"></a>예  
 예를 들어 [WITH XMLNAMESPACES를 사용하여 쿼리에 네임스페이스 추가](../../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [XQuery 언어 참조&#40;SQL Server&#41;](../../xquery/xquery-language-reference-sql-server.md)  
  
  
