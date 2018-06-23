---
title: 형식화된 XML과 형식화되지 않은 XML 비교 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-xml
ms.tgt_pltfrm: ''
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
caps.latest.revision: 57
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 08e80c3a42406b11abc0a46ae7b4afc92d0a35e6
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36091695"
---
# <a name="compare-typed-xml-to-untyped-xml"></a>형식화된 XML과 형식화되지 않은 XML 비교
  `xml` 유형의 변수, 매개 변수 및 열을 만들 수 있습니다. 변수, 매개 변수 또는 열과 XML 스키마 컬렉션을 선택적으로 연결할 수 `xml` 유형입니다. 이 경우에 `xml` 데이터 형식 인스턴스에 라고 *입력*합니다. 그 외의 경우에는 XML 인스턴스를 *형식화되지 않았다*고 합니다.  
  
## <a name="well-formed-xml-and-the-xml-data-type"></a>올바른 형식의 XML 및 xml 데이터 형식  
 `xml` 데이터 형식은 ISO 표준 `xml` 데이터 형식을 구현합니다. 따라서 올바른 형식의 XML 버전 1.0 문서를 저장할 수 있으며 텍스트 노드 및 형식화되지 않은 XML 열의 최상위 요소가 임의의 개수로 포함된 XML 내용 조각을 저장할 수 있습니다. 시스템은 데이터가 올바른 형식인지 확인하고, 열이 XML 스키마로 바인딩되도록 요구하지 않으며, 넓은 의미에서 올바른 형식이 아닌 데이터를 거부합니다. 형식화되지 않은 XML 변수 및 매개 변수도 여기에 해당됩니다.  
  
## <a name="xml-schemas"></a>XML 스키마  
 XML 스키마는 다음을 제공합니다.  
  
-   **유효성 검사 제약 조건** 형식화된 xml 인스턴스가 할당 또는 수정될 때마다 SQL Sever가 인스턴스의 유효성을 검사합니다.  
  
-   **데이터 형식 정보** 스키마는 `xml` 데이터 형식 인스턴스에 있는 특성 및 요소의 유형에 대한 정보를 제공합니다. 유형 정보는 인스턴스에 포함되어 있는 값에 대해 형식화되지 않은 `xml`에 있을 수 있는 것보다 정확한 작업 의미를 제공합니다. 예를 들어 숫자 산술 연산은 문자열 값이 10진수 값에서 수행할 수 있습니다. 따라서 형식화된 XML 저장소는 형식화되지 않은 XML보다 더욱 간결하게 만들 수 있습니다.  
  
## <a name="choosing-typed-or-untyped-xml"></a>형식화된 XML 또는 형식화되지 않은 XML 선택  
 사용 하 여 형식화 되지 않은 `xml` 다음과 같은 상황에서 데이터 형식:  
  
-   XML 데이터에 대한 스키마가 없습니다.  
  
-   스키마가 있지만 서버에서 데이터 유효성 검사를 수행하지 않습니다. 이러한 경우는 데이터를 서버에 저장하기 전에 응용 프로그램이 클라이언트 쪽 유효성 검사를 수행하거나, 스키마에 대해 유효하지 않은 XML 데이터를 임시적으로 저장하거나, 서버에서 지원되지 않는 스키마 구성 요소를 사용하는 경우입니다.  
  
 사용 하 여 입력 한 `xml` 다음과 같은 상황에서 데이터 형식:  
  
-   XML 데이터에 대한 스키마가 있으며 이 XML 스키마에 따라 서버에서 XML 데이터의 유효성을 검사하려고 합니다.  
  
-   형식 정보에 따라 저장소 및 쿼리 최적화를 활용합니다.  
  
-   쿼리 컴파일 시 형식 정보를 더욱 활용합니다.  
  
 형식화된 XML 열, 매개 변수 및 변수는 XML 문서 또는 내용을 저장할 수 있습니다. 그러나 선언 시 문서를 저장하는지 아니면 내용을 저장하는지에 따라 플래그를 지정해야 합니다. 또한 XML 스키마의 컬렉션을 제공해야 합니다. 각 XML 인스턴스에 정확히 하나의 최상위 요소가 있는 경우 DOCUMENT를 지정합니다. 그렇지 않으면 CONTENT를 사용합니다. 쿼리 컴파일러는 쿼리 컴파일 중에 형식 검사에서 DOCUMENT 플래그를 사용하여 단일 항목인 최상위 요소를 유추합니다.  
  
## <a name="creating-typed-xml"></a>형식화된 XML 만들기  
 형식화 된 만들기 전에 `xml` 변수, 매개 변수 또는 열을 사용 하 여 XML 스키마 컬렉션을 먼저 등록 해야 [CREATE XML SCHEMA COLLECTION &#40;TRANSACT-SQL&#41;](/sql/t-sql/statements/create-xml-schema-collection-transact-sql)합니다. XML 스키마 컬렉션 변수, 매개 변수 또는 열과 연결할 수 있습니다는 `xml` 데이터 형식입니다.  
  
 다음 예에서는 XML 스키마 컬렉션 이름을 지정하기 위해 두 부분으로 된 명명 규칙이 사용됩니다. 첫 번째 부분은 스키마 이름이고 두 번째 부분은 XML 스키마 컬렉션 이름입니다.  
  
### <a name="example-associating-a-schema-collection-with-an-xml-type-variable"></a>예제: xml 유형 변수와 스키마 컬렉션 연결  
 다음 예제에서는`xml` 유형 변수에 스키마 컬렉션을 연결 합니다. 이 예에서 지정된 스키마 컬렉션은 이미 **AdventureWorks** 데이터베이스로 가져온 상태입니다.  
  
```  
DECLARE @x xml (Production.ProductDescriptionSchemaCollection);   
```  
  
### <a name="example-specifying-a-schema-for-an-xml-type-column"></a>예제: xml 유형 열에 스키마 지정  
 다음 예제에서는 있는 테이블을 만듭니다는 `xml` 열을 입력 하 고 열에 대 한 스키마를 지정 합니다.  
  
```  
CREATE TABLE T1(  
 Col1 int,   
 Col2 xml (Production.ProductDescriptionSchemaCollection)) ;  
```  
  
### <a name="example-passing-an-xml-type-parameter-to-a-stored-procedure"></a>예제: xml 유형 매개 변수를 저장 프로시저에 전달  
 다음 예제에서는 전달 된 `xml` 저장된 프로시저에 매개 변수를 입력 하 고 해당 변수에 대 한 스키마를 지정 합니다.  
  
```  
CREATE PROCEDURE SampleProc   
  @ProdDescription xml (Production.ProductDescriptionSchemaCollection)   
AS   
...  
```  
  
 XML 스키마 컬렉션에 대한 다음 내용에 유의하십시오.  
  
-   XML 스키마 컬렉션은 [XML 스키마 컬렉션 만들기](/sql/t-sql/statements/create-xml-schema-collection-transact-sql)를 사용하여 등록한 데이터베이스에서만 사용할 수 있습니다.  
  
-   문자열에서을 형식화 된 캐스팅 하는 경우 `xml` 데이터 형식으로 구문 분석 유효성 검사와 지정 된 컬렉션에 있는 XML 스키마 네임 스페이스에 따라 형식 지정도 수행 됩니다.  
  
-   형식화된 `xml` 데이터 형식을 형식화되지 않은 `xml` 데이터 형식으로 캐스팅하거나 그 반대로도 할 수 있습니다.  
  
 SQL Server에서 XML을 생성하는 다른 방법은 [XML 데이터 인스턴스 만들기](create-instances-of-xml-data.md)를 참조하세요. XML을 생성 한 후 할당 될 수 하는 `xml` 데이터 형식에 저장 된 변수에 `xml` 추가 처리에 대 한 열을 입력 합니다.  
  
 데이터 형식 계층 구조에는 `xml` 데이터 형식 아래 표시 `sql_variant` 및 사용자 정의 형식을 기본 제공 유형 위에 합니다.  
  
### <a name="example-specifying-facets-to-constrain-a-typed-xml-column"></a>예제: 형식화된 xml 열을 제한하기 위한 패싯 지정  
 형식화 된 `xml` 열에 저장 된 각 인스턴스에 대해 최상위의 단일 요소만 허용 하도록 열을 제한할 수 있습니다. 이렇게 하려면 다음 예에서와 같이 테이블을 만들 때 선택 항목인 `DOCUMENT` 패싯을 지정합니다.  
  
```  
CREATE TABLE T(Col1 xml   
   (DOCUMENT Production.ProductDescriptionSchemaCollection));  
GO  
DROP TABLE T;  
GO  
```  
  
 기본적으로 형식화 된에 저장 된 인스턴스 `xml` 열 XML 문서가 아닌 XML 콘텐츠로 저장 됩니다. 이러한 설정은 다음의 경우에 허용됩니다.  
  
-   0개 이상의 최상위 요소  
  
-   최상위 요소에 있는 텍스트 노드  
  
 또한 다음 예에서와 같이 `CONTENT` 패싯을 추가하여 이 동작을 명시적으로 지정할 수 있습니다.  
  
```  
CREATE TABLE T(Col1 xml(CONTENT Production.ProductDescriptionSchemaCollection));  
GO -- Default  
```  
  
 `xml` 유형(형식화된 xml)을 정의할 때 항상 선택 항목인 DOCUMENT/CONTENT 패싯을 지정할 수 있습니다. 예를 들어 만들 때 형식화 된 `xml` 변수를 추가할 수 있습니다 DOCUMENT/CONTENT 패싯을 다음과 같이 합니다.  
  
```  
declare @x xml (DOCUMENT Production.ProductDescriptionSchemaCollection);  
```  
  
## <a name="document-type-definition-dtd"></a>DTD(문서 유형 정의)  
 `xml` 데이터 형식의 열, 변수 및 매개 변수는 DTD가 아닌 XML 스키마를 사용하여 형식화될 수 있습니다. 하지만 인라인 DTD는 형식화되지 않은 XML 및 형식화된 XML에 모두 사용하여 기본값을 제공하고 엔터티 참조를 해당 확장 형식으로 바꿀 수 있습니다.  
  
 타사 도구를 사용하여 DTD를 XML 스키마 문서로 변환하고 XML 스키마를 데이터베이스에 로드할 수 있습니다.  
  
## <a name="upgrading-typed-xml-from-sql-server-2005"></a>SQL Server 2005에서 형식화된 XML 업그레이드  
 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 에서는 XML 스키마 지원이 여러 가지로 확대되었습니다. 여기에는 lax 유효성 검사에 대한 지원, 향상된 **xs:date**, **xs:time** 및 **xs:dateTime** 인스턴스 데이터 처리, 목록 유형 및 공용 구조체 유형에 대한 추가 지원이 포함됩니다. 대부분의 경우 변경 사항이 업그레이드에 영향을 주지 않습니다. 그러나 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] xs:date **,** xs:time **또는**xs:dateTime **형식이나 하위 형식의 값을 사용할 수 있는** 의 XML 스키마 컬렉션을 사용한 경우 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 데이터베이스를 그 이상의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]버전에 연결하면 다음 업그레이드 단계가 진행됩니다.  
  
1.  모든 XML 열의 경우, 이 열이 **xs:anyType**, **xs:anySimpleType**, **xs:date** 또는 해당 하위 유형, **xs:time** 또는 해당 하위 유형, **xs:dateTime** 또는 해당 하위 유형으로 형식화되거나 이러한 유형이 포함된 공용 구조체나 목록 유형으로 형식화된 요소나 특성이 들어 있는 XML 스키마 컬렉션으로 형식화되면 다음과 같은 상황이 발생합니다.  
  
    1.  열의 모든 XML 인덱스가 사용할 수 없게 됩니다.  
  
    2.  모든 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 값이 Z 표준 시간대로 표준화되었으므로 이 값이 Z 표준 시간대로 계속 표시됩니다.  
  
    3.  일 년 중 1월 1일보다 작은 **xs:date** 또는 **xs:dateTime** 값은 인덱스가 다시 작성되거나 XQuery 또는 XML-DML 문이 해당 값을 포함하는 XML 데이터 형식에 대해 실행되면 런타임 오류를 일으킵니다.  
  
2.  **xs:date** 또는 **xs:dateTime** 패싯의 음수 연도나 XML 스키마 컬렉션의 기본값은 기본 **xs:date** 또는 **xs:dateTime** 형식(예: **xs:dateTime**의 경우 0001-01-01T00:00:00.0000000Z)에 의해 허용되는 최소값으로 자동 업데이트됩니다.  
  
 간단한 SQL SELECT 문을 계속 사용하면 음수 연도가 포함될 경우에도 전체 XML 데이터 형식을 검색할 수 있습니다. 음수 연도를 새로 지원되는 범위에 있는 연도로 대체하거나 해당 요소나 특성의 유형을 **xs:string**으로 변경하는 것이 좋습니다.  
  
## <a name="see-also"></a>관련 항목  
 [XML 데이터 인스턴스 만들기](create-instances-of-xml-data.md)   
 [xml 데이터 형식 메서드](/sql/t-sql/xml/xml-data-type-methods)   
 [XML DML&#40;XML 데이터 수정 언어&#41;](/sql/t-sql/xml/xml-data-modification-language-xml-dml)   
 [XML 데이터&#40;SQL Server&#41;](xml-data-sql-server.md)  
  
  
