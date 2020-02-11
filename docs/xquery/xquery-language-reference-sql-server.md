---
title: XQuery 언어 참조 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
helpviewer_keywords:
- XQuery
- XQuery, about XQuery
- xml data type [SQL Server], XQuery
- XML [SQL Server], XQuery
- queries [XML in SQL Server], XQuery
ms.assetid: 8a69344f-2990-4357-8160-cb26aac95b91
author: rothja
ms.author: jroth
ms.openlocfilehash: 87edbeaac26ca1c332efe981901cbf0bc57fed30
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67945963"
---
# <a name="xquery-language-reference-sql-server"></a>XQuery 언어 참조(SQL Server)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[tsql](../includes/tsql-md.md)]는 **xml** 데이터 형식을 쿼리 하는 데 사용 되는 XQuery 언어의 하위 집합을 지원 합니다. 이 XQuery 구현은 XQuery에 대한 2004년 7월 초안을 따릅니다. 이 언어는 Microsoft를 비롯한 주요 데이터베이스 공급업체의 참여 하에 W3C(World Wide Web Consortium)에서 개발 중에 있습니다. W3C 사양은 W3C 권장 사양이 되기 전에 향후 개정을 거칠 수 있기 때문에 이 구현은 최종 권장 사양과 다를 수 있습니다. 이 항목에서는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 지원되는 XQuery의 하위 집합에 대한 의미 및 구문에 대해 간단히 설명합니다.  
  
 자세한 내용은 [W3C XQuery 1.0 언어 사양](https://go.microsoft.com/fwlink/?LinkId=48846)을 참조 하세요.  
  
 XQuery는 구조화되었거나 반구조화된 XML 데이터를 쿼리할 수 있는 언어입니다. 에서 제공 하는 **xml** 데이터 형식 지원을 사용 [!INCLUDE[ssDE](../includes/ssde-md.md)]하면 문서를 데이터베이스에 저장 한 다음 XQuery를 사용 하 여 쿼리할 수 있습니다.  
  
 XQuery는 기존의 XPath 쿼리 언어를 기반으로 더 나은 반복 성능 및 정렬 결과를 위한 지원이 추가되었으며 필요한 XML을 생성할 수 있는 기능이 지원됩니다. XQuery는 XQuery 데이터 모델에서 작동합니다. 이러한 모델은 XML 문서에 대한 추상적 표현이며 XQuery 결과는 형식화되거나 형식화되지 않을 수 있습니다. 유형 정보는 W3C XML 스키마 언어에서 제공되는 유형을 기반으로 합니다. 형식화 정보가 제공되지 않은 경우 XQuery는 데이터를 형식화되지 않은 것으로 처리합니다. 이는 XPath 버전 1.0에서 XML을 처리하는 방법과 비슷합니다.  
  
 **Xml 형식의 변수** 또는 열에 저장 된 xml 인스턴스를 쿼리하려면 [Xml 데이터 형식 메서드](../t-sql/xml/xml-data-type-methods.md)를 사용 합니다. 예를 들어 **xml 형식의 변수** 를 선언 하 고 **xml** 데이터 형식의 **query ()** 메서드를 사용 하 여 쿼리할 수 있습니다.  
  
```sql
DECLARE @x xml  
SET @x = '<ROOT><a>111</a></ROOT>'  
SELECT @x.query('/ROOT/a')  
```  
  
 다음 예에서는 AdventureWorks 데이터베이스의 제품 모델 테이블에 있는 **xml** 유형의 명령 열에 대해 쿼리를 지정 합니다.  
  
```sql
SELECT Instructions.query('declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";           
    /AWMI:root/AWMI:Location[@LocationID=10]  
') as Result   
FROM  Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 XQuery에는 네임 스페이스 선언 `declare namespace``AWMI=...`, 및 쿼리 식가 `/AWMI:root/AWMI:Location[@LocationID=10]`포함 되어 있습니다.  
  
 XQuery는 **xml** 유형의 명령 열에 대해 지정 됩니다. Xml 데이터 형식의 [query () 메서드](../t-sql/xml/query-method-xml-data-type.md) 는 XQuery를 지정 하는 데 사용 됩니다.  
  
 다음 표에서는 [!INCLUDE[ssDE](../includes/ssde-md.md)]의 XQuery 구현 방식을 이해하는 데 도움이 될 수 있는 관련 항목들이 나열되어 있습니다.  
  
|항목|Description|  
|-----------|-----------------|  
|[XML 데이터&#40;SQL Server&#41;](../relational-databases/xml/xml-data-sql-server.md)|에서 **xml**데이터 형식에 대 한 지원 [!INCLUDE[ssDE](../includes/ssde-md.md)] 및이 데이터 형식에 사용할 수 있는 메서드를 설명 합니다. **Xml** 데이터 형식은 xquery 식이 실행 되는 입력 xquery 데이터 모델을 형성 합니다.|  
|[XML 스키마 컬렉션&#40;SQL Server&#41;](../relational-databases/xml/xml-schema-collections-sql-server.md)|데이터베이스에 저장된 XML 인스턴스를 형식화하는 방법을 설명합니다. 즉, xml 스키마 컬렉션과 **xml** 유형 열을 연결할 수 있습니다. 열에 저장된 모든 항목은 유효성이 검사되고 컬렉션에 있는 스키마에 대해 형식화되며 XQuery에 대한 유형 정보를 제공합니다.|  
|||  
  
> [!NOTE]  
>  이 섹션의 구성은 W3C(World Wide Web Consortium) XQuery 초안 사양을 기반으로 합니다. 이 섹션에서 제공되는 일부 다이어그램은 이 사양에서 가져온 것입니다. 이 섹션에서는 Microsoft XQuery 구현과 W3C 사양을 비교하고 Microsoft XQuery와 W3C의 다른 점을 설명하고 지원되지 않는 W3C 기능에 대해 설명합니다. W3C 사양은에서 [http://www.w3.org/TR/2004/WD-xquery-20040723](https://go.microsoft.com/fwlink/?LinkId=48846)사용할 수 있습니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
|항목|Description|  
|-----------|-----------------|  
|[XQuery 기초](../xquery/xquery-basics.md)|XQuery 개념에 대한 기본 개여는 물론 식 평가(정적 및 동적 컨텍스트), 원자화, 효율적인 부울 값, XQuery 유형 시스템, 시퀀스 유형 일치 및 오류 처리 등을 제공합니다.|  
|[XQuery 식](../xquery/xquery-expressions.md)|XQuery 기본 식, 경로 식, 시퀀스 식, 산술 비교 및 논리 식, XQuery 구성, FLWOR 식, 조건 및 한정 식, 시퀀스 유형의 여러 식에 대해 설명합니다.|  
|[모듈 및 Prologs &#40;XQuery&#41;](../xquery/modules-and-prologs-xquery.md)|XQuery 프롤로그에 대해 설명합니다.|  
|[xml 데이터 형식에 대한 XQuery 함수](../xquery/xquery-functions-against-the-xml-data-type.md)|지원되는 XQuery 함수 목록에 대해 설명합니다.|  
|[xml 데이터 형식에 대한 XQuery 연산자](../xquery/xquery-operators-against-the-xml-data-type.md)|지원되는 XQuery 연산자에 대해 설명합니다.|  
|[xml 데이터 형식에 대한 추가 예제 XQuery](../xquery/additional-sample-xqueries-against-the-xml-data-type.md)|추가 XQuery 예제를 제공합니다.|  
  
## <a name="see-also"></a>참고 항목  
 [XML 데이터&#40;SQL Server&#41;](../relational-databases/xml/xml-data-sql-server.md)   
 [XML 스키마 컬렉션&#40;SQL Server&#41;](../relational-databases/xml/xml-schema-collections-sql-server.md)   
 [XML 문서 대량 가져오기 및 내보내기 예제&#40;SQL Server&#41;](../relational-databases/import-export/examples-of-bulk-import-and-export-of-xml-documents-sql-server.md)  
  
  
