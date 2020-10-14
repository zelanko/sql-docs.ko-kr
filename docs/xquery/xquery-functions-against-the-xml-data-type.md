---
title: Xml 데이터 형식에 대 한 XQuery 함수 | Microsoft Docs
description: Xml 데이터 형식에 대해 사용 하도록 지원 되는 XQuery 함수에 대해 알아봅니다.
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- XQuery, functions
- xml data type [SQL Server], XQuery
- functions [SQL Server], XQuery
ms.assetid: 8df0877d-a03f-4ca9-b84e-908c4bb42b5e
author: rothja
ms.author: jroth
ms.openlocfilehash: 8e92148b5a85ced147599eafe09156cf41c47021
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/14/2020
ms.locfileid: "92037016"
---
# <a name="xquery-functions-against-the-xml-data-type"></a>xml 데이터 형식에 대한 XQuery 함수
[!INCLUDE [SQL Server Azure SQL Database ](../includes/applies-to-version/sqlserver.md)]

  이 항목 및 하위 항목에서는 **xml** 데이터 형식에 대해 XQuery를 지정할 때 사용할 수 있는 함수에 대해 설명 합니다. W3C 사양에 대해서는을 참조 하십시오 [http://www.w3.org/TR/2004/WD-xpath-functions-20040723](https://go.microsoft.com/fwlink/?LinkId=4873) .  
  
 XQuery 함수는 http://www.w3.org/2004/07/xpath-functions 네임 스페이스에 속합니다. W3C 사양에서는 "fn:" 네임스페이스 접두사를 사용하여 이러한 함수를 기술합니다. 함수를 사용할 때는 "fn:" 네임스페이스 접두사를 명시적으로 지정할 필요가 없습니다. 이러한 이유로 인해 그리고 가독성을 위해 네임스페이스 접두사는 일반적으로 이 설명서에서 사용되지 않습니다.  
  
 다음 표에서는 **xml**데이터 형식에 대해 지원 되는 XQuery 함수를 보여 줍니다.  
  
|범주|함수 이름|  
|--------------|-------------------|  
|[숫자 값에 대 한 함수]()|[ceiling](../xquery/numeric-values-functions-ceiling.md)|  
||[평면](../xquery/numeric-values-functions-floor.md)|  
||[둥근](../xquery/numeric-values-functions-round.md)|  
|[문자열 값의 XQuery 함수]()|[concat](../xquery/functions-on-string-values-concat.md)|  
||[contains](../xquery/functions-on-string-values-contains.md)|  
||[substring](../xquery/functions-on-string-values-substring.md)|  
||[낮은 case 함수 &#40;XQuery&#41;](../xquery/functions-on-string-values-lower-case.md)|  
||[문자열 길이](../xquery/functions-on-string-values-string-length.md)|  
||[대문자 함수 &#40;XQuery&#41;](../xquery/functions-on-string-values-upper-case.md)|  
|부울 값 함수|[not](../xquery/functions-on-boolean-values-not-function.md)|  
|[노드의 함수]()|[number](../xquery/functions-on-nodes-number.md)|  
||[local-name 함수(XQuery)](../xquery/functions-on-nodes-local-name.md)|  
||[namespace-uri 함수(XQuery)](../xquery/functions-on-nodes-namespace-uri.md)|  
|[컨텍스트 함수]()|[last](../xquery/context-functions-last-xquery.md)|  
||[position](../xquery/context-functions-position-xquery.md)|  
|[시퀀스 함수]()|[empty](../xquery/functions-on-sequences-empty.md)|  
||[distinct-values](../xquery/functions-on-sequences-distinct-values.md)|  
||[id 함수(XQuery)](../xquery/functions-on-sequences-id.md)|  
|[집계 함수 &#40;XQuery&#41;]()|[count](../xquery/aggregate-functions-count.md)|  
||[avg](../xquery/aggregate-functions-avg.md)|  
||[min](../xquery/aggregate-functions-min.md)|  
||[max](../xquery/aggregate-functions-max.md)|  
||[sum](../xquery/aggregate-functions-sum.md)|  
|[생성자 함수는 XQuery를 &#40;&#41;](../xquery/constructor-functions-xquery.md)|[생성자 함수](../xquery/constructor-functions-xquery.md)|  
|[데이터 접근자 함수](../xquery/data-accessor-functions.md)|[string](../xquery/data-accessor-functions-string-xquery.md)|  
||[data](../xquery/data-accessor-functions-data-xquery.md)|  
|[부울 생성자 함수는 XQuery를 &#40;&#41;]()|[true 함수(XQuery)](../xquery/boolean-constructor-functions-true-xquery.md)|  
||[false 함수(XQuery)](../xquery/boolean-constructor-functions-false-xquery.md)|  
|[Qname &#40;XQuery&#41;와 관련 된 함수 ](./functions-related-to-qnames-expanded-qname.md)|[expanded-QName(XQuery)](../xquery/functions-related-to-qnames-expanded-qname.md)|  
||[local-name-from-QName(XQuery)](../xquery/functions-related-to-qnames-local-name-from-qname.md)|  
||[namespace-uri-from-QName(XQuery)](../xquery/functions-related-to-qnames-namespace-uri-from-qname.md)|  
|[SQL Server XQuery 확장 함수](./xquery-extension-functions-sql-column.md)|[sql:column() 함수(XQuery)](../xquery/xquery-extension-functions-sql-column.md)|  
||[sql:variable() 함수(XQuery)](../xquery/xquery-extension-functions-sql-variable.md)|  
  
## <a name="see-also"></a>참고 항목  
 [xml 데이터 형식 메서드](../t-sql/xml/xml-data-type-methods.md)   
 [XQuery 언어 참조&#40;SQL Server&#41;](../xquery/xquery-language-reference-sql-server.md)   
 [XML 데이터&#40;SQL Server&#41;](../relational-databases/xml/xml-data-sql-server.md)  
  
