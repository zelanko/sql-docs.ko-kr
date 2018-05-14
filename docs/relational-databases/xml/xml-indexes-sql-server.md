---
title: XML 인덱스(SQL Server) | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: xml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- removing indexes
- deleting indexes
- secondary indexes [XML in SQL Server]
- xml data type [SQL Server], indexes
- dropping indexes
- PATH index
- DROP_EXISTING clause
- XML [SQL Server], indexes
- primary indexes [XML in SQL Server]
- indexes [SQL Server], XML
- XML indexes [SQL Server], secondary
- BLOBs, XML indexes
- disabling indexes
- XML indexes [SQL Server], modifying
- XML indexes [SQL Server]
- XML indexes [SQL Server], primary
- modifying indexes
- XML indexes [SQL Server], dropping
- VALUE index
- XML indexes [SQL Server], xml data type
- PROPERTY index
- XML indexes [SQL Server], creating
ms.assetid: f5c9209d-b3f3-4543-b30b-01365a5e7333
caps.latest.revision: 59
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 7b5109d315e3c4bafdf7af1d1c8b1bf3734e3e6d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="xml-indexes-sql-server"></a>XML 인덱스(SQL Server)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  XML 인덱스를 **xml** 데이터 형식의 열에 만들 수 있습니다. 그러면 열에 있는 XML 인스턴스에 대해 모든 태그, 값 및 경로가 인덱싱되어 쿼리 성능이 향상됩니다. 다음 경우에 응용 프로그램에서 XML 인덱스를 활용할 수 있습니다.  
  
-   XML 열의 쿼리가 작업에서 일반적입니다. 데이터를 수정하는 동안 XML 인덱스 유지 관리 비용이 고려되어야 합니다.  
  
-   XML 값이 비교적 크며 검색된 부분은 비교적 작습니다. 인덱스를 작성하면 런타임 시 전체 데이터의 구문 분석이 방지되므로 인덱스 조회를 통해 쿼리를 효율적으로 처리할 수 있습니다.  
  
 XML 인덱스는 다음 범주로 구분됩니다.  
  
-   기본 XML 인덱스  
  
-   보조 XML 인덱스  
  
 **xml** 형식 열의 첫 번째 인덱스는 기본 XML 인덱스여야 합니다. 기본 XML 인덱스를 사용하면 PATH, VALUE 및 PROPERTY 형식의 보조 인덱스가 지원됩니다. 이러한 보조 인덱스는 쿼리 유형에 따라 쿼리 성능을 향상시킬 수 있습니다.  
  
> [!NOTE]  
>  데이터베이스 옵션이 **xml** 데이터 형식 작업에 대해 제대로 설정되지 않을 경우 XML 인덱스를 만들거나 수정할 수 없습니다. 자세한 내용은 [XML 열에 전체 텍스트 검색 사용](../../relational-databases/xml/use-full-text-search-with-xml-columns.md)을 참조하세요.  
  
 XML 인스턴스는 BLOB(Binary Large Object)으로 **xml** 형식 열에 저장되어 있습니다. 이러한 XML 인스턴스는 크기가 클 수 있으며 **xml** 데이터 형식 인스턴스의 저장된 이진 표현은 최대 2GB까지 될 수 있습니다. 이러한 BLOB은 인덱스 없이 런타임 시 단편화되어 쿼리를 계산할 수 있습니다. 이 단편화 작업에는 시간이 많이 걸릴 수 있습니다. 예를 들어 다음 쿼리를 참조하십시오.  
  
```  
WITH XMLNAMESPACES ('http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS "PD")  
  
SELECT CatalogDescription.query('  
  /PD:ProductDescription/PD:Summary  
') as Result  
FROM Production.ProductModel  
WHERE CatalogDescription.exist ('/PD:ProductDescription/@ProductModelID[.="19"]') = 1  
```  
  
 `WHERE` 절의 조건에 맞는 XML 인스턴스를 선택할 수 있도록 `Production.ProductModel` 테이블의 각 행에서 XML BLOB이 런타임 시 단편화됩니다. 그런 다음 `(/PD:ProductDescription/@ProductModelID[.="19"]`메서드의 `exist()` ) 식이 계산됩니다. 이러한 런타임 단편화는 열에 저장된 인스턴스의 크기와 수에 따라 비용이 많이 들 수 있습니다.  
  
 XML BLOB을 쿼리하는 것이 사용자의 응용 프로그램 환경에서 일반적인 경우 이것은 **xml** 형식 열을 인덱싱하는 데 도움이 됩니다. 그러나 데이터 수정 중 인덱스를 유지 관리하는 비용이 듭니다.  
  
## <a name="primary-xml-index"></a>기본 XML 인덱스  
 기본 XML 인덱스는 XML의 XML 인스턴스 내에 있는 모든 태그, 값 및 경로를 인덱싱합니다. 기본 XML 인덱스를 만들려면 XML 열이 발생하는 테이블에는 테이블의 기본 키에 클러스터링된 인덱스가 있어야 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 이 기본 키를 사용하여 기본 XML 인덱스에 있는 행과 XML 열을 포함하는 테이블에 있는 행의 상관 관계를 지정할 수 있습니다.  
  
 기본 XML 인덱스는 **xml** 데이터 형식 열의 XML BLOB을 지속적인 단편 형태로 표현한 것입니다. 인덱스는 열의 XML BLOB(Binary Large Object)마다 여러 개의 데이터 행을 만듭니다. 인덱스의 행 수는 대략 XML BLOB의 노드 수와 같습니다. 쿼리가 전체 XML 인스턴스를 검색할 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 XML 열의 인스턴스를 제공합니다. XML 인스턴스 내의 쿼리에서는 기본 XML 인덱스를 사용하고 인덱스 자체를 사용하여 스칼라 값이나 XML 하위 트리를 반환할 수 있습니다.  
  
 각 행에는 다음 노드 정보를 저장합니다.  
  
-   요소 또는 특성 이름과 같은 태그 이름  
  
-   노드 값  
  
-   요소 노드, 특성 노드 또는 텍스트 노드와 같은 노드 유형  
  
-   내부 노드 식별자에 의해 표현되는 문서 순서 정보  
  
-   각 노드에서 XML 트리의 루트에 대한 경로. 이 열은 쿼리의 경로 식으로 검색됩니다.  
  
-   기본 테이블의 기본 키. 기본 테이블의 기본 키는 기본 테이블과 백 조인을 위한 기본 XML 인덱스에 복제되고 해당 기본 테이블의 기본 키에 있는 최대 열 수는 15개로 제한됩니다.  
  
 이 노드 정보는 지정된 쿼리에 대해 XML 결과를 계산 및 구성하는 데 사용됩니다. 최적화를 위해 태그 이름과 노드 유형 정보는 정수 값으로 인코딩되고 경로 열에서는 같은 인코딩을 사용합니다. 또한 경로는 경로 접미사가 알려져 있는 경우에만 경로에 일치할 수 있도록 반대 순서로 저장됩니다. 예를 들어 다음과 같이 사용할 수 있습니다.  
  
-   `//ContactRecord/PhoneNumber` - 마지막 두 단계만 알려져 있는 경우  
  
 또는  
  
-   `/Book/*/Title` 와일드카드 문자(`*`)가 식 중간에 지정되어 있는 경우  
  
 쿼리 프로세서에서는 [xml Data Type Methods](../../t-sql/xml/xml-data-type-methods.md) 를 포함하는 쿼리에 대해 기본 XML 인덱스를 사용하고 기본 인덱스 자체에서 스칼라 값이나 XML 하위 트리를 반환합니다. 이 인덱스는 XML 인스턴스를 재구성하는 데 필요한 모든 정보를 저장합니다.  
  
 예를 들어 다음 쿼리는 `ProductModel` 테이블의 `CatalogDescription`**xml** 형식 열에 저장된 요약 정보를 반환합니다. 이 쿼리는 카탈로그 설명에 <`Features`> 설명도 저장되어 있는 제품 모델에 대해서만 <`Summary`> 정보를 반환합니다.  
  
```  
WITH XMLNAMESPACES ('http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS "PD")SELECT CatalogDescription.query('  /PD:ProductDescription/PD:Summary') as ResultFROM Production.ProductModelWHERE CatalogDescription.exist ('/PD:ProductDescription/PD:Features') = 1  
```  
  
 기본 XML 인덱스에 관해 기본 테이블에서 각 XML BLOB 인스턴스를 단편화하는 대신, 각 XML BLOB에 해당하는 인덱스의 행이 `exist()` 메서드에 지정된 식에 대해 순서대로 검색됩니다. 경로를 인덱스의 경로 열에서 찾은 경우 <`Summary`> 요소와 그 하위 트리는 기본 XML 인덱스에서 함께 검색되고 `query()` 메서드의 결과로 XML BLOB로 변환됩니다.  
  
 전체 XML 인스턴스를 검색할 때는 기본 XML 인덱스가 사용되지 않습니다. 예를 들어 다음 쿼리는 테이블에서 특정 제품 모델에 대한 제조 지침을 나타내는 전체 XML 인스턴스를 검색합니다.  
  
```  
USE AdventureWorks2012;SELECT InstructionsFROM Production.ProductModel WHERE ProductModelID=7;  
```  
  
## <a name="secondary-xml-indexes"></a>보조 XML 인덱스  
 검색 성능을 향상시키기 위해 보조 XML 인덱스를 만들 수 있습니다. 기본 XML 인덱스가 있어야 보조 인덱스를 만들 수 있습니다. 유형은 다음과 같습니다.  
  
-   PATH 보조 XML 인덱스  
  
-   VALUE 보조 XML 인덱스  
  
-   PROPERTY 보조 XML 인덱스  
  
 다음은 하나 이상의 보조 인덱스를 만드는 데에 대한 몇 가지 지침입니다.  
  
-   작업에서 XML 열에 경로 식이 중요하게 사용되는 경우 PATH 보조 XML 인덱스는 작업 속도를 높일 수 있습니다. 가장 일반적인 경우는 Transact-SQL의 WHERE 절에서 XML 열에 대해 **exist()** 메서드를 사용하는 것입니다.  
  
-   작업에 경로 식을 사용하여 개별적인 XML 인스턴스로부터 여러 값을 검색하는 경우 PROPERTY 인덱스에 있는 각 XML 인스턴스 내의 경로를 클러스터링하면 도움이 될 수 있습니다. 이러한 시나리오는 개체의 속성이 인출되고 해당 기본 키 값이 알려진 속성 모음 시나리오에서 일반적으로 발생합니다.  
  
-   작업에 해당 값이 포함된 요소 또는 특성 이름을 알지 못하는 상태에서 XML 인스턴스 내의 값을 쿼리하는 작업이 포함되는 경우 VALUE 인덱스를 만들 수 있습니다. 이러한 경우는 //author[last-name="Howard"]\(\<author> 요소는 계층의 임의 수준에서 발생 가능)와 같은 하위 항목 축 조회 시에 일반적으로 발생합니다. 또한 /book [@* = "novel"]\(쿼리가 "novel" 값이 있는 일부 특성을 포함하는 \<book> 요소 조회)과 같은 와일드카드 쿼리에서 발생합니다.  
  
### <a name="path-secondary-xml-index"></a>PATH 보조 XML 인덱스  
 쿼리에서 일반적으로 **xml** 유형 열에 경로 식을 지정하는 경우에는 PATH 보조 인덱스로 검색 속도를 높일 수도 있습니다. 이 항목의 앞에서 설명한 대로 기본 인덱스는 **exist()** 메서드를 WHERE 절에 지정하는 쿼리가 있는 경우에 유용합니다. 또한 PATH 보조 인덱스를 추가하면 이러한 쿼리에서 검색 성능을 향상시킬 수 있습니다.  
  
 기본 XML 인덱스에서 런타임 시 XML BLOB의 단편화는 피할 수 있지만 경로 식을 사용하는 쿼리의 최대 성능은 제공할 수 없습니다. XML BLOB에 해당하는 기본 XML 인덱스의 모든 행이 대규모의 XML 인스턴스에 대해 순서대로 검색되기 때문에 순차적 검색의 속도가 느려질 수 있습니다. 이 경우 기본 인덱스의 경로 값과 노드 값에 보조 인덱스를 만들면 인덱스 검색의 속도가 현저히 빨라질 수 있습니다. PATH 보조 인덱스에서 경로 값 및 노드 값은 경로 검색 시 효율적으로 검색할 수 있는 키 열입니다. 쿼리 최적화 프로그램에서는 다음과 같은 식에 대해 PATH 인덱스를 사용할 수 있습니다.  
  
-   `/root/Location` - 경로만 지정한 경우  
  
 또는  
  
-   `/root/Location/@LocationID[.="10"]` - 경로 값과 노드 값이 모두 지정되어 있는 경우  
  
 다음 쿼리에서는 PATH 인덱스가 유용하게 사용되는 경우를 보여 줍니다.  
  
```  
WITH XMLNAMESPACES ('http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS "PD")  
  
SELECT CatalogDescription.query('  
  /PD:ProductDescription/PD:Summary  
') AS Result  
FROM Production.ProductModel  
WHERE CatalogDescription.exist ('/PD:ProductDescription/@ProductModelID[.="19"]') = 1  
```  
  
 쿼리에서 `/PD:ProductDescription/@ProductModelID` 메서드의 경로 식 `"19"` 및 `exist()` 값은 PATH 인덱스의 키 필드에 해당합니다. 따라서 PATH 인덱스에서 직접 찾을 수 있고 기본 인덱스의 경로 값에 대한 순차적 검색보다 더 나은 검색 성능을 제공합니다.  
  
### <a name="value-secondary-xml-index"></a>VALUE 보조 XML 인덱스  
 예를 들어 쿼리가 값을 기반으로 하는 `/Root/ProductDescription/@*[. = "Mountain Bike"]` 또는 `//ProductDescription[@Name = "Mountain Bike"]`이고 경로가 완전히 지정되지 않거나 와일드카드를 포함하는 경우에는 기본 XML 인덱스의 노드 값에 보조 XML 인덱스를 만들어 더 빠른 결과를 얻을 수 있습니다.  
  
 VALUE 인덱스의 키 열은 기본 XML 인덱스의 노드 값 및 경로입니다. 값을 포함하는 요소 또는 특성 이름을 알 필요 없이 XML 인스턴스에서 해당 값을 쿼리하는 작업이 포함되는 경우 VALUE 인덱스가 유용합니다. 예를 들어 다음 식에 VALUE 인덱스가 있는 것이 좋습니다.  
  
-   `//author[LastName="someName"]` - <`LastName`> 요소의 값은 알지만 <`author`> 부모가 아무 곳에서나 발생할 수 있는 경우  
  
-   `/book[@* = "someValue"]` - 쿼리가 `"someValue"` 값이 있는 일부 특성을 가진 <`book`> 요소를 찾는 경우  
  
 다음 쿼리에서는 `ContactID` 테이블에서 `Contact` 를 반환합니다. `WHERE` 절은 `AdditionalContactInfo`**xml** 유형 열에서 값을 찾는 필터를 지정합니다. 연락처 ID는 해당되는 추가 연락처 정보 XML BLOB에 특정 전화 번호가 포함되는 경우에만 반환됩니다. <`telephoneNumber`> 요소가 XML의 아무 위치에서나 나타날 수 있기 때문에 경로 식은 하위 또는 자체 축을 지정합니다.  
  
```  
WITH XMLNAMESPACES (  
  'http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactInfo' AS CI,  
  'http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes' AS ACT)  
  
SELECT ContactID   
FROM   Person.Contact  
WHERE  AdditionalContactInfo.exist('//ACT:telephoneNumber/ACT:number[.="111-111-1111"]') = 1  
```  
  
 이 경우 <`number`>에 대한 검색 값을 알지만 이 값은 <`telephoneNumber`> 요소의 자식으로 XML 인스턴스의 아무 위치에서나 나타날 수 있습니다. 이러한 유형의 쿼리를 사용하면 특정 값에 기반한 인덱스 조회의 장점을 활용할 수 있습니다.  
  
### <a name="property-secondary-index"></a>PROPERTY 보조 인덱스  
 개별 XML 인스턴스에서 하나 이상의 값을 검색하는 쿼리는 PROPERTY 인덱스의 장점을 활용할 수 있습니다. 이 시나리오는 사용자가 **xml** 유형의 **value()** 메서드를 사용하여 개체 속성을 검색할 때 및 개체의 기본 키 값이 알려져 있을 때 발생합니다.  
  
 PK가 기본 테이블의 기본 키인 기본 XML 인덱스의 열(PK, 경로 및 노드 값)에 PROPERTY XML 인덱스를 만듭니다.  
  
 예를 들어 제품 모델 `19`의 경우 다음 쿼리는 `ProductModelID` 메서드를 사용하여 `ProductModelName` 및 `value()` 특성 값을 검색합니다. 기본 XML 인덱스 또는 기타 보조 XML 인덱스를 사용하는 대신 PROPERTY 인덱스를 사용하면 더 빨리 실행될 수 있습니다.  
  
```  
WITH XMLNAMESPACES ('http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS "PD")  
  
SELECT CatalogDescription.value('(/PD:ProductDescription/@ProductModelID)[1]', 'int') as ModelID,  
       CatalogDescription.value('(/PD:ProductDescription/@ProductModelName)[1]', 'varchar(30)') as ModelName          
FROM Production.ProductModel     
WHERE ProductModelID = 19  
```  
  
 이 항목의 후반부에서 설명하는 차이점을 제외하면**xml** 유형 열에 XML 인덱스를 만드는 것은 비**xml** 유형 열에 인덱스를 만드는 것과 비슷합니다. 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] DDL 문은 XML 인덱스의 작성 및 관리에 사용될 수 있습니다.  
  
-   [CREATE INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)  
  
-   [ALTER INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)  
  
-   [DROP INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/drop-index-transact-sql.md)  
  
## <a name="getting-information-about-xml-indexes"></a>XML 인덱스에 대한 정보 가져오기  
 XML 인덱스 항목은 인덱스 "type"이 3인 카탈로그 뷰 sys.indexes에 표시됩니다. 이름 열에는 XML 인덱스의 이름이 포함됩니다.  
  
 XML 인덱스는 또한 카탈로그 뷰 sys.xml_indexes에 기록됩니다. 여기에는 sys.indexes의 모든 열과 XML 인덱스에 유용한 특정 열이 포함됩니다. secondary_type 열에 있는 NULL 값은 기본 XML 인덱스를 나타냅니다. 'P', 'R' 및 'V' 값은 각각 PATH, PROPERTY 및 VALUE 보조 XML 인덱스를 나타냅니다.  
  
 XML 인덱스의 공간 사용은 [sys.dm_db_index_physical_stats](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)테이블 반환 함수에서 찾을 수 있습니다. 이 함수는 모든 인덱스 유형에 대해 사용된 디스크 페이지 수, 평균 행 크기(바이트) 및 레코드 수와 같은 정보를 제공합니다. 여기에는 XML 인덱스도 포함됩니다. 이 정보는 각 데이터베이스 파티션에서 사용할 수 있습니다. XML 인덱스는 기본 테이블과 동일한 파티션 구성표 및 파티션 함수를 사용합니다.  
  
## <a name="see-also"></a>참고 항목  
 [sys.dm_db_index_physical_stats&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)   
 [XML 데이터&#40;SQL Server&#41;](../../relational-databases/xml/xml-data-sql-server.md)  
  
  
