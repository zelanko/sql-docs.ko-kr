---
title: "형식화된 XML과 형식화되지 않은 XML 비교 | Microsoft 문서"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: xml
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- xml data type [SQL Server], variables
- parameters [XML in SQL Server]
- facets [XML in SQL Server]
- xml data type [SQL Server], columns
- untyped XML
- xml data type [SQL Server], typed xml
- XML [SQL Server], typed
- variables [XML in SQL Server], creating
- xml data type [SQL Server], untyped xml
- columns [XML in SQL Server], creating
- typed XML
- document mode processing [SQL Server]
- XML [SQL Server], untyped
- xml data type [SQL Server], parameters
ms.assetid: 4bc50af9-2f7d-49df-bb01-854d080c72c7
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: b40976e2a8efdaf0b41ede4f79786060b7e1163c
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/12/2018
---
# <a name="compare-typed-xml-to-untyped-xml"></a>형식화된 XML과 형식화되지 않은 XML 비교
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
**xml** 유형의 변수, 매개 변수 및 열을 만들 수 있습니다. 선택적으로 XML 스키마 컬렉션을 **xml** 유형의 변수, 매개 변수 또는 열과 연결할 수 있습니다. 이런 경우 **xml** 데이터 형식 인스턴스를 *형식화되었다*고 하고, 그 외의 경우에는 XML 인스턴스를 *형식화되지 않았다*고 합니다.  
  
## <a name="well-formed-xml-and-the-xml-data-type"></a>올바른 형식의 XML 및 xml 데이터 형식  
 **xml** 데이터 형식은 ISO 표준 **xml** 데이터 형식을 구현합니다. 따라서 올바른 형식의 XML 버전 1.0 문서를 저장할 수 있으며 텍스트 노드 및 형식화되지 않은 XML 열의 최상위 요소가 임의의 개수로 포함된 XML 내용 조각을 저장할 수 있습니다. 시스템은 데이터가 올바른 형식인지 확인하고, 열이 XML 스키마로 바인딩되도록 요구하지 않으며, 넓은 의미에서 올바른 형식이 아닌 데이터를 거부합니다. 형식화되지 않은 XML 변수 및 매개 변수도 여기에 해당됩니다.  
  
## <a name="xml-schemas"></a>XML 스키마  
 XML 스키마는 다음을 제공합니다.  
  
-   **유효성 검사 제약 조건** 형식화된 xml 인스턴스가 할당 또는 수정될 때마다 SQL Sever가 인스턴스의 유효성을 검사합니다.  
  
-   **데이터 형식 정보** 스키마는 **xml** 데이터 형식 인스턴스에 있는 특성 및 요소의 유형에 대한 정보를 제공합니다. 유형 정보는 인스턴스에 포함되어 있는 값에 대해 형식화되지 않은 **xml**에 있을 수 있는 것보다 정확한 작업 의미를 제공합니다. 예를 들어 숫자 산술 연산은 문자열 값이 10진수 값에서 수행할 수 있습니다. 따라서 형식화된 XML 저장소는 형식화되지 않은 XML보다 더욱 간결하게 만들 수 있습니다.  
  
## <a name="choosing-typed-or-untyped-xml"></a>형식화된 XML 또는 형식화되지 않은 XML 선택  
 다음 경우에 형식화되지 않은 **xml** 데이터 형식을 사용합니다.  
  
-   XML 데이터에 대한 스키마가 없습니다.  
  
-   스키마가 있지만 서버에서 데이터 유효성 검사를 수행하지 않습니다. 이러한 경우는 데이터를 서버에 저장하기 전에 응용 프로그램이 클라이언트 쪽 유효성 검사를 수행하거나, 스키마에 대해 유효하지 않은 XML 데이터를 임시적으로 저장하거나, 서버에서 지원되지 않는 스키마 구성 요소를 사용하는 경우입니다.  
  
 다음 경우에 형식화된 **xml** 데이터 형식을 사용합니다.  
  
-   XML 데이터에 대한 스키마가 있으며 이 XML 스키마에 따라 서버에서 XML 데이터의 유효성을 검사하려고 합니다.  
  
-   형식 정보에 따라 저장소 및 쿼리 최적화를 활용합니다.  
  
-   쿼리 컴파일 시 형식 정보를 더욱 활용합니다.  
  
 형식화된 XML 열, 매개 변수 및 변수는 XML 문서 또는 내용을 저장할 수 있습니다. 그러나 선언 시 문서를 저장하는지 아니면 내용을 저장하는지에 따라 플래그를 지정해야 합니다. 또한 XML 스키마의 컬렉션을 제공해야 합니다. 각 XML 인스턴스에 정확히 하나의 최상위 요소가 있는 경우 DOCUMENT를 지정합니다. 그렇지 않으면 CONTENT를 사용합니다. 쿼리 컴파일러는 쿼리 컴파일 중에 형식 검사에서 DOCUMENT 플래그를 사용하여 단일 항목인 최상위 요소를 유추합니다.  
  
## <a name="creating-typed-xml"></a>형식화된 XML 만들기  
 형식화된 **xml** 변수, 매개 변수 또는 열을 만들려면 먼저 [CREATE XML SCHEMA COLLECTION&#40;Transact-SQL&#41;](../../t-sql/statements/create-xml-schema-collection-transact-sql.md)에 따라 XML 스키마 컬렉션을 등록해야 합니다. 그런 다음 XML 스키마 컬렉션을 **xml** 데이터 형식의 변수, 매개 변수 또는 열과 연결할 수 있습니다.  
  
 다음 예에서는 XML 스키마 컬렉션 이름을 지정하기 위해 두 부분으로 된 명명 규칙이 사용됩니다. 첫 번째 부분은 스키마 이름이고 두 번째 부분은 XML 스키마 컬렉션 이름입니다.  
  
### <a name="example-associating-a-schema-collection-with-an-xml-type-variable"></a>예제: xml 유형 변수와 스키마 컬렉션 연결  
 다음 예제에서는 **xml** 형식 변수를 만들고 이를 스키마 컬렉션에 연결합니다. 이 예에서 지정된 스키마 컬렉션은 이미 **AdventureWorks** 데이터베이스로 가져온 상태입니다.  
  
```  
DECLARE @x xml (Production.ProductDescriptionSchemaCollection);   
```  
  
### <a name="example-specifying-a-schema-for-an-xml-type-column"></a>예제: xml 유형 열에 스키마 지정  
 다음 예에서는 **xml** 유형 열이 포함된 테이블을 만들고 이 열에 대한 스키마를 지정합니다.  
  
```  
CREATE TABLE T1(  
 Col1 int,   
 Col2 xml (Production.ProductDescriptionSchemaCollection)) ;  
```  
  
### <a name="example-passing-an-xml-type-parameter-to-a-stored-procedure"></a>예제: xml 유형 매개 변수를 저장 프로시저에 전달  
 다음 예에서는 **xml** 유형 매개 변수를 저장 프로시저에 전달하고 해당 변수에 대한 스키마를 지정합니다.  
  
```  
CREATE PROCEDURE SampleProc   
  @ProdDescription xml (Production.ProductDescriptionSchemaCollection)   
AS   
...  
```  
  
 XML 스키마 컬렉션에 대한 다음 내용에 유의하십시오.  
  
-   XML 스키마 컬렉션은 [XML 스키마 컬렉션 만들기](../../t-sql/statements/create-xml-schema-collection-transact-sql.md)를 사용하여 등록한 데이터베이스에서만 사용할 수 있습니다.  
  
-   또한 문자열을 형식화된 **xml** 데이터 형식으로 캐스팅하는 경우 구문 분석 시 지정된 컬렉션에 있는 XML 스키마 네임스페이스에 따라 유효성 검사와 형식 지정도 수행됩니다.  
  
-   형식화된 **xml** 데이터 형식을 형식화되지 않은 **xml** 데이터 형식으로 캐스팅하거나 그 반대로도 할 수 있습니다.  
  
 SQL Server에서 XML을 생성하는 다른 방법은 [XML 데이터 인스턴스 만들기](../../relational-databases/xml/create-instances-of-xml-data.md)를 참조하세요. XML을 생성한 후 **xml** 데이터 형식 변수에 할당하거나 **xml** 유형 열에 저장하여 추가 처리를 수행할 수 있습니다.  
  
 데이터 형식 계층에서 **xml** 데이터 형식은 **sql_variant** 및 사용자 정의 형식 아래, 기본 제공 유형 위에 표시됩니다.  
  
### <a name="example-specifying-facets-to-constrain-a-typed-xml-column"></a>예제: 형식화된 xml 열을 제한하기 위한 패싯 지정  
 형식화된 **xml** 열의 경우 열에 저장된 각 인스턴스에 대해 최상위의 단일 요소만 허용하도록 열을 제한할 수 있습니다. 이렇게 하려면 다음 예에서와 같이 테이블을 만들 때 선택 항목인 `DOCUMENT` 패싯을 지정합니다.  
  
```  
CREATE TABLE T(Col1 xml   
   (DOCUMENT Production.ProductDescriptionSchemaCollection));  
GO  
DROP TABLE T;  
GO  
```  
  
 기본적으로 형식화된 **xml** 열에 저장된 인스턴스는 XML 문서가 아닌 XML 콘텐츠로 저장됩니다. 이러한 설정은 다음의 경우에 허용됩니다.  
  
-   0개 이상의 최상위 요소  
  
-   최상위 요소에 있는 텍스트 노드  
  
 또한 다음 예에서와 같이 `CONTENT` 패싯을 추가하여 이 동작을 명시적으로 지정할 수 있습니다.  
  
```  
CREATE TABLE T(Col1 xml(CONTENT Production.ProductDescriptionSchemaCollection));  
GO -- Default  
```  
  
 **xml** 형식(형식화된 xml)을 정의할 때 항상 선택 항목인 DOCUMENT/CONTENT 패싯을 지정할 수 있습니다. 예를 들어 형식화된 **xml** 변수를 만들 때 다음과 같이 DOCUMENT/CONTENT 패싯을 추가할 수 있습니다.  
  
```  
declare @x xml (DOCUMENT Production.ProductDescriptionSchemaCollection);  
```  
  
## <a name="document-type-definition-dtd"></a>DTD(문서 유형 정의)  
 **xml** 데이터 형식의 열, 변수 및 매개 변수는 DTD가 아닌 XML 스키마를 사용하여 형식화될 수 있습니다. 하지만 인라인 DTD는 형식화되지 않은 XML 및 형식화된 XML에 모두 사용하여 기본값을 제공하고 엔터티 참조를 해당 확장 형식으로 바꿀 수 있습니다.  
  
 타사 도구를 사용하여 DTD를 XML 스키마 문서로 변환하고 XML 스키마를 데이터베이스에 로드할 수 있습니다.  
  
## <a name="upgrading-typed-xml-from-sql-server-2005"></a>SQL Server 2005에서 형식화된 XML 업그레이드  
 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 에서는 XML 스키마 지원이 여러 가지로 확대되었습니다. 여기에는 lax 유효성 검사에 대한 지원, 향상된 **xs:date**, **xs:time** 및 **xs:dateTime** 인스턴스 데이터 처리, 목록 유형 및 공용 구조체 유형에 대한 추가 지원이 포함됩니다. 대부분의 경우 변경 사항이 업그레이드에 영향을 주지 않습니다. 그러나 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] xs:date **,**xs:time **또는**xs:dateTime **형식이나 하위 형식의 값을 사용할 수 있는** 의 XML 스키마 컬렉션을 사용한 경우 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 데이터베이스를 그 이상의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]버전에 연결하면 다음 업그레이드 단계가 진행됩니다.  
  
1.  모든 XML 열의 경우, 이 열이 **xs:anyType**, **xs:anySimpleType**, **xs:date** 또는 해당 하위 유형, **xs:time** 또는 해당 하위 유형, **xs:dateTime** 또는 해당 하위 유형으로 형식화되거나 이러한 유형이 포함된 공용 구조체나 목록 유형으로 형식화된 요소나 특성이 들어 있는 XML 스키마 컬렉션으로 형식화되면 다음과 같은 상황이 발생합니다.  
  
    1.  열의 모든 XML 인덱스가 사용할 수 없게 됩니다.  
  
    2.  모든 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 값이 Z 표준 시간대로 표준화되었으므로 이 값이 Z 표준 시간대로 계속 표시됩니다.  
  
    3.  일 년 중 1월 1일보다 작은 **xs:date** 또는 **xs:dateTime** 값은 인덱스가 다시 작성되거나 XQuery 또는 XML-DML 문이 해당 값을 포함하는 XML 데이터 형식에 대해 실행되면 런타임 오류를 일으킵니다.  
  
2.  **xs:date** 또는 **xs:dateTime** 패싯의 음수 연도나 XML 스키마 컬렉션의 기본값은 기본 **xs:date** 또는 **xs:dateTime** 형식(예: **xs:dateTime**의 경우 0001-01-01T00:00:00.0000000Z)에 의해 허용되는 최소값으로 자동 업데이트됩니다.  
  
 간단한 SQL SELECT 문을 계속 사용하면 음수 연도가 포함될 경우에도 전체 XML 데이터 형식을 검색할 수 있습니다. 음수 연도를 새로 지원되는 범위에 있는 연도로 대체하거나 해당 요소나 특성의 유형을 **xs:string**으로 변경하는 것이 좋습니다.  
  
## <a name="see-also"></a>참고 항목  
 [XML 데이터 인스턴스 만들기](../../relational-databases/xml/create-instances-of-xml-data.md)   
 [xml 데이터 형식 메서드](../../t-sql/xml/xml-data-type-methods.md)   
 [XML DML&#40;XML 데이터 수정 언어&#41;](../../t-sql/xml/xml-data-modification-language-xml-dml.md)   
 [XML 데이터&#40;SQL Server&#41;](../../relational-databases/xml/xml-data-sql-server.md)  
  
  
