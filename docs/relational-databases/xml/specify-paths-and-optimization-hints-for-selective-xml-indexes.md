---
title: 선택적 XML 인덱스에 대한 경로 및 최적화 힌트 지정 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
ms.assetid: 486ee339-165b-4aeb-b760-d2ba023d7d0a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2763cd39d1be3318bfa297539f56720838cde6d9
ms.sourcegitcommit: cff8dd63959d7a45c5446cadf1f5d15ae08406d8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2019
ms.locfileid: "67584415"
---
# <a name="specify-paths-and-optimization-hints-for-selective-xml-indexes"></a>선택적 XML 인덱스에 대한 경로 및 최적화 힌트 지정
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  이 항목에서는 선택적 XML 인덱스를 만들거나 변경할 때 인덱싱할 노드 경로 및 인덱싱에 대한 최적화 힌트를 지정합니다.  
  
 노드 경로 및 최적화 힌트는 다음 문 중 하나에 동시에 지정합니다.  
  
-   **CREATE** 문의 **FOR** 절 자세한 내용은 [CREATE SELECTIVE XML INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/create-selective-xml-index-transact-sql.md)를 참조하세요.  
  
-   **ALTER** 문의 **ADD** 절 자세한 내용은 [ALTER INDEX&#40;선택적 XML 인덱스&#41;](../../t-sql/statements/alter-index-selective-xml-indexes.md)를 참조하세요.  
  
 선택적 XML 인덱스에 대한 자세한 내용은 [SXI&#40;선택적 XML 인덱스&#41;](../../relational-databases/xml/selective-xml-indexes-sxi.md)를 참조하세요.  
  
##  <a name="untyped"></a> 형식화된 XML의 XQuery 및 SQL Server 유형 이해  
 선택적 XML 인덱스는 두 가지 유형 시스템, XQuery 유형 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유형을 지원합니다. 인덱싱된 경로는 XQuery 식을 일치시키거나 XML 데이터 형식의 value() 메서드에 대한 반환 형식을 일치시키는 데 사용할 수 있습니다.  
  
-   인덱싱할 경로에 주석이 지정되어 있지 않거나 XQUERY 키워드로 주석이 지정된 경우 해당 경로는 XQuery 식과 일치합니다. XQUERY로 주석이 지정된 노드 경로에는 다음과 같은 두 가지 변형이 있습니다.  
  
    -   XQUERY 키워드 및 XQuery 데이터 형식을 지정하지 않으면 기본 매핑이 사용됩니다. 이 경우 일반적으로 성능 및 스토리지는 효율적이지 않습니다.  
  
    -   XQUERY 키워드 및 XQuery 데이터 형식을 지정하고 선택적으로 다른 최적화 옵션을 지정하면 가능한 최상의 성능과 가능한 가장 효율적인 스토리지를 얻을 수 있습니다. 캐스팅은 실패할 수 있습니다.  
  
-   인덱싱할 경로에 SQL 키워드로 주석이 지정된 경우 해당 경로는 XML 데이터 형식의 value() 메서드에 대한 반환 형식과 일치합니다. value() 메서드의 반환 형식인 적절한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식을 지정하십시오.  
  
 XML 데이터 형식의 value() 메서드에 적용되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유형 시스템과 XQuery 식 XML 유형 시스템과 간에는 약간의 차이가 있습니다. 이러한 차이점은 다음과 같습니다.  
  
-   XQuery 유형 시스템은 후행 공백을 인식합니다. 예를 들어 XQuery 유형 의미 체계에서는 문자열 "abc"와 "abc "가 같은 문자열이 아니지만 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 이러한 문자열이 같은 문자열입니다.  
  
-   XQuery 부동 소수점 데이터 형식에서는 +/- 0 및 +/- 무한대와 같은 특수 값이 지원되지만 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 부동 소수점 데이터 형식에서는 이러한 특수 값이 지원되지 않습니다.  
  
### <a name="xquery-types-in-untyped-xml"></a>형식화되지 않은 XML의 XQuery 유형  
  
-   XQuery 유형은 value() 메서드를 비롯한 XML 데이터 형식의 모든 메서드에 있는 XQuery 식과 일치합니다.  
  
-   XQuery 유형은 node(), SINGLETON, DATA TYPE 및 MAXLENGTH 최적화 힌트를 지원합니다.  
  
 형식화되지 않은 XML에 대한 XQuery 식의 작업 모드는 다음 두 가지 중에서 선택할 수 있습니다.  
  
-   **기본 매핑 모드**. 이 모드에서는 선택적 XML 인덱스를 만들 때만 경로를 지정합니다.  
  
-   **사용자 지정 매핑 모드**. 이 모드에서는 선택적 최적화 힌트와 경로를 둘 다 지정합니다.  
  
 기본 매핑 모드에서는 안전하고 일반적인 스토리지 옵션을 사용합니다. 따라서 경로가 모든 식 유형과 일치할 수 있습니다. 런타임 캐스팅이 더 많이 필요하고 보조 인덱스를 사용할 수 없기 때문에 기본 매핑 모드의 제한은 최상의 성능보다 낮습니다.  
  
 다음은 기본 매핑을 사용하여 만든 선택적 XML 인덱스의 예입니다. 세 경로 모두에 기본 노드 형식(**xs:untypedAtomic**) 및 카디널리티가 사용됩니다.  
  
```sql  
CREATE SELECTIVE XML INDEX example_sxi_UX_default  
ON Tbl(xmlcol)  
FOR  
(  
mypath01 =  '/a/b',  
mypath02 = '/a/b/c',  
mypath03 = '/a/b/d'  
)  
```  
  
 사용자 지정 매핑 모드를 사용하면 더 나은 성능을 얻기 위해 노드에 유형 및 카디널리티를 지정할 수 있습니다. 그러나 캐스팅이 실패할 수 있고 지정된 유형만 선택적 XML 인덱스와 일치하므로 이 향상된 성능은 보안의 희생을 통해 얻어집니다.  
  
 형식화되지 않은 XML에 대해 지원되는 XQuery 형식은 다음과 같습니다.  
  
-   **xs:boolean**  
  
-   **xs:double**  
  
-   **xs:string**  
  
-   **xs:date**  
  
-   **xs:time**  
  
-   **xs:dateTime**  
  
 노드에 유형을 지정하지 않으면 해당 노드는 **xs:untypedAtomic** 데이터 형식인 것으로 간주됩니다.  
  
 다음과 같은 방법으로 선택적 XML 인덱스를 최적화할 수 있습니다.  
  
```sql  
CREATE SELECTIVE XML INDEX example_sxi_UX_optimized  
ON Tbl(xmlcol)  
FOR  
(  
mypath= '/a/b' as XQUERY 'node()',  
pathX = '/a/b/c' as XQUERY 'xs:double' SINGLETON,  
pathY = '/a/b/d' as XQUERY 'xs:string' MAXLENGTH(200) SINGLETON  
)  
-- mypath - Only the node value is needed; storage is saved.  
-- pathX - Performance is improved; secondary indexes are possible.  
-- pathY - Performance is improved; secondary indexes are possible; storage is saved.  
```  
  
### <a name="sql-server-types-in-untyped-xml"></a>형식화되지 않은 XML의 SQL Server 유형  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유형은 value() 메서드의 반환 값과 일치합니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유형은 SINGLETON 최적화 힌트를 지원합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유형을 반환하는 경로에는 유형을 반드시 지정해야 합니다. 이 경우 value() 메서드에서 사용하는 것과 동일한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유형을 지정해야 합니다.  
  
 다음 쿼리를 살펴보십시오.  
  
```sql  
SELECT T.record,  
    T.xmldata.value('(/a/b/d)[1]', 'NVARCHAR(200)')  
FROM myXMLTable T  
```  
  
 지정된 쿼리는 NVARCHAR(200) 데이터 형식으로 압축된 `/a/b/d` 경로에서 값을 반환하기 때문에 노드에 지정할 데이터 형식이 분명합니다. 그러나 형식화되지 않은 XML로 노드의 카디널리티를 지정할 수 있는 스키마는 없습니다. `d` 노드가 해당 부모 노드인 `b`에 최대 한 번만 표시되도록 지정하려면 다음과 같이 SINGLETON 최적화 힌트를 사용하는 선택적 XML 인덱스를 만듭니다.  
  
```sql  
CREATE SELECTIVE XML INDEX example_sxi_US  
ON Tbl(xmlcol)  
FOR  
(  
node1223 = '/a/b/d' as SQL NVARCHAR(200) SINGLETON  
)  
```  
  
  
##  <a name="typed"></a> 형식화된 XML에 대한 선택적 XML 인덱스 지원 이해  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 형식화된 XML은 지정된 XML 문서와 연결된 스키마입니다. 스키마는 전체 문서 구조와 노드 유형을 정의합니다. 스키마가 있으면 사용자가 경로를 승격시킬 때 선택적 XML 인덱스가 해당 스키마 구조를 적용하기 때문에 경로에 대한 XQUERY 유형을 지정할 필요가 없습니다.  
  
 선택적 XML 인덱스는 다음 XSD 유형을 지원합니다.  
  
-   **xs:anyUri**  
  
-   **xs:boolean**  
  
-   **xs:date**  
  
-   **xs:dateTime**  
  
-   **xs:day**  
  
-   **xs:decimal**  
  
-   **xs:double**  
  
-   **xs:float**  
  
-   **xs:int**  
  
-   **xs:integer**  
  
-   **xs:language**  
  
-   **xs:long**  
  
-   **xs:name**  
  
-   **xs:NCName**  
  
-   **xs:negativeInteger**  
  
-   **xs:nmtoken**  
  
-   **xs:nonNegativeInteger**  
  
-   **xs:nonPositiveInteger**  
  
-   **xs:positiveInteger**  
  
-   **xs:qname**  
  
-   **xs:short**  
  
-   **xs:string**  
  
-   **xs:time**  
  
-   **xs:token**  
  
-   **xs:unsignedByte**  
  
-   **xs:unsignedInt**  
  
-   **xs:unsignedLong**  
  
-   **xs:unsignedShort**  
  
 스키마가 연결되어 있는 문서에 대해 선택적 XML 인덱스를 만드는 경우 인덱스를 만들거나 변경할 때 XQUERY 유형을 지정하면 오류가 반환됩니다. 사용자는 경로 승격 부분에 SQL 유형 주석을 사용할 수 있습니다. SQL 유형은 스키마에 정의된 XSD 유형으로부터의 유효한 변환이어야 합니다. 그렇지 않으면 예외가 발생합니다. 날짜/시간 유형을 제외하고 XSD로 적절하게 표현된 모든 SQL 유형이 지원됩니다.  
  
> [!NOTE]  
>  선택적 인덱스는 선택적 XML 인덱스 경로 승격에 지정된 유형이 value() 메서드 반환 값과 같을 경우 사용됩니다.  
  
 다음은 형식화된 XML 문서에서 사용할 수 있는 최적화 힌트입니다.  
  
-   node() 최적화 힌트  
  
-   MAXLENGTH 최적화 힌트는 인덱싱된 값을 줄이기 위해 xs:string 유형과 함께 사용될 수 있습니다.  
  
 최적화 힌트에 대한 자세한 내용은 [최적화 힌트 지정](#hints)을 참조하십시오.  
  
##  <a name="paths"></a> 경로 지정  
 선택적 XML 인덱스를 사용하면 저장된 XML 데이터에서 실행할 쿼리와 관련 있는 노드의 하위 집합만 인덱싱할 수 있습니다. 관련 노드의 하위 집합이 XML 문서에 있는 총 노드 수보다 훨씬 적을 경우 선택적 XML 인덱스는 관련 노드만 저장합니다. 선택적 XML 인덱스를 사용하려면 인덱싱할 노드의 올바른 하위 집합을 식별해야 합니다.  
  
### <a name="choosing-the-nodes-to-index"></a>인덱싱할 노드 선택  
 다음과 같은 두 가지 간단한 원칙을 사용하여 선택적 XML 인덱스에 추가할 노드의 올바른 하위 집합을 식별할 수 있습니다.  
  
1.  **원칙 1**: 지정된 XQuery 식을 평가하려면 검사할 모든 노드를 인덱싱합니다.  
  
    -   존재 여부 또는 값이 XQuery 식에 사용되는 모든 노드를 인덱싱합니다.  
  
    -   XQuery 조건자가 적용되는 XQuery 식의 모든 노드를 인덱싱합니다.  
  
     이 항목의 [샘플 XML 문서](#sample) 에 대한 다음과 같은 간단한 쿼리를 살펴보십시오.  
  
    ```sql  
    SELECT T.record FROM myXMLTable T  
    WHERE T.xmldata.exist('/a/b[./c = "43"]') = 1  
    ```  
  
     아 쿼리를 만족하는 XML 인스턴스를 반환하려면 선택적 XML 인덱스가 각 XML 인스턴스에서 다음 두 노드를 검사해야 합니다.  
  
    -   `c`노드(해당 값이 XQuery 식에 사용되므로)  
  
    -   `b`노드(XQuery 식에서`b` 노드에 대해 조건자가 적용되므로)  
  
2.  **원칙 2**: 최상의 성능을 위해 지정된 XQuery 식을 평가하는 데 필요한 모든 노드를 인덱싱합니다. 이러한 노드 중 일부만 인덱싱할 경우 선택적 XML 인덱스가 인덱싱된 노드만 포함하는 하위 식의 평가를 향상시킵니다.  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

 위에 표시된 SELECT 문의 성능을 향상시키기 위해 다음과 같은 선택적 XML 인덱스를 만들 수 있습니다.  
  
```sql  
CREATE SELECTIVE XML INDEX simple_sxi  
ON Tbl(xmlcol)  
FOR  
(  
    path123 =  '/a/b',  
    path124 =  '/a/b/c'  
)  
```  
  
### <a name="indexing-identical-paths"></a>동일한 경로 인덱싱  
 동일한 경로를 서로 다른 경로 이름을 사용하는 동일한 데이터 형식으로 승격시킬 수 없습니다. 예를 들어 다음 쿼리를 실행하면 `pathOne` 과 `pathTwo` 가 동일하기 때문에 오류가 발생합니다.  
  
```sql  
CREATE SELECTIVE INDEX test_simple_sxi ON T1(xmlCol)  
FOR  
(  
    pathOne = 'book/authors/authorID' AS XQUERY 'xs:string',  
    pathTwo = 'book/authors/authorID' AS XQUERY 'xs:string'  
)  
```  
  
 그러나 동일한 경로를 서로 다른 이름을 사용하는 서로 다른 데이터 형식으로는 승격시킬 수 있습니다. 예를 들어 다음 쿼리는 데이터 형식이 다르기 때문에 허용될 수 있습니다.  
  
```sql  
CREATE SELECTIVE INDEX test_simple_sxi ON T1(xmlCol)  
FOR  
(  
    pathOne = 'book/authors/authorID' AS XQUERY 'xs:double',  
    pathTwo = 'book/authors/authorID' AS XQUERY 'xs:string'  
)  
```  
  
### <a name="examples"></a>예  
 다음은 서로 다른 XQuery 형식에 대해 인덱싱할 올바른 노드를 선택하는 몇 가지 추가 예입니다.  
  
 **예제 1**  
  
 다음은 exist() 메서드를 사용하는 간단한 XQuery입니다.  
  
```sql  
SELECT T.record FROM myXMLTable T  
WHERE T.xmldata.exist('/a/b/c/d/e/h') = 1  
```  
  
 다음 표에서는 이 쿼리가 선택적 XML 인덱스를 사용할 수 있도록 하기 위해 인덱싱해야 하는 노드를 보여 줍니다.  
  
|인덱스에 포함할 열|이 노드를 인덱싱하는 이유|  
|----------------------------------|-----------------------------------|  
|**/a/b/c/d/e/h**|`h` 노드의 존재 여부가 exist() 메서드에서 평가됩니다.|  
  
 **예제 2**  
  
 다음은 조건자가 적용된 이전 XQuery의 보다 복잡한 변형입니다.  
  
```sql  
SELECT T.record FROM myXMLTable T  
WHERE T.xmldata.exist('/a/b/c/d/e[./f = "SQL"]') = 1  
```  
  
 다음 표에서는 이 쿼리가 선택적 XML 인덱스를 사용할 수 있도록 하기 위해 인덱싱해야 하는 노드를 보여 줍니다.  
  
|인덱스에 포함할 열|이 노드를 인덱싱하는 이유|  
|----------------------------------|-----------------------------------|  
|**/a/b/c/d/e**|조건자가 `e`노드를 통해 적용됩니다.|  
|**/a/b/c/d/e/f**|`f` 노드의 값이 조건자 내에서 평가됩니다.|  
  
 **예 3**  
  
 다음은 value() 절이 포함된 보다 복잡한 쿼리입니다.  
  
```sql  
SELECT T.record,  
    T.xmldata.value('(/a/b/c/d/e[./f = "SQL"]/g)[1]', 'nvarchar(100)')  
FROM myXMLTable T  
```  
  
 다음 표에서는 이 쿼리가 선택적 XML 인덱스를 사용할 수 있도록 하기 위해 인덱싱해야 하는 노드를 보여 줍니다.  
  
|인덱스에 포함할 열|이 노드를 인덱싱하는 이유|  
|----------------------------------|-----------------------------------|  
|**/a/b/c/d/e**|조건자가 `e`노드를 통해 적용됩니다.|  
|**/a/b/c/d/e/f**|`f` 노드의 값이 조건자 내에서 평가됩니다.|  
|**/a/b/c/d/e/g**|`g` 노드의 값이 value() 메서드에 의해 반환됩니다.|  
  
 **예제 4**  
  
 다음은 exist() 절 내의 FLWOR 절을 사용하는 쿼리입니다. (FLWOR이라는 이름은 XQuery FLWOR 식을 구성하는 다섯 개의 절인 for, let, where, order by 및 return에서 따온 것입니다.)  
  
```sql  
SELECT T.record FROM myXMLTable T  
WHERE T.xmldata.exist('  
  For $x in /a/b/c/d/e  
  Where $x/f = "SQL"  
  Return $x/g  
') = 1  
```  
  
 다음 표에서는 이 쿼리가 선택적 XML 인덱스를 사용할 수 있도록 하기 위해 인덱싱해야 하는 노드를 보여 줍니다.  
  
|인덱스에 포함할 열|이 노드를 인덱싱하는 이유|  
|----------------------------------|-----------------------------------|  
|**/a/b/c/d/e**|`e` 노드의 존재 여부가 FLWOR 절에서 평가됩니다.|  
|**/a/b/c/d/e/f**|`f` 노드의 값이 FLWOR 절에서 평가됩니다.|  
|**/a/b/c/d/e/g**|`g` 노드의 존재 여부가 exist() 메서드에 의해 평가됩니다.|  
  
  
##  <a name="hints"></a> 최적화 힌트 지정  
 선택적 최적화 힌트를 사용하여 선택적 XML 인덱스에 의해 인덱싱되는 노드에 대한 추가 매핑 정보를 지정할 수 있습니다. 예를 들어 노드의 데이터 형식과 카디널리티, 그리고 데이터의 구조에 대한 특정 정보를 지정할 수 있습니다. 이 추가 정보를 사용하면 매핑이 향상될 뿐 아니라 성능과 스토리지의 저장 능력도 향상됩니다.  
  
 최적화 힌트의 사용은 선택 사항입니다. 언제든지 기본 매핑을 그대로 사용할 수 있습니다. 그러나 기본 매핑을 사용하면 안정적이기는 하지만 최적의 성능과 스토리지를 사용하지 못할 수도 있습니다.  
  
 SINGLETON 힌트와 같은 일부 최적화 힌트는 데이터에 대한 제약 조건을 소개합니다. 경우에 따라 이러한 제약 조건을 충족하지 못할 경우 오류가 발생할 수 있습니다.  
  
### <a name="benefits-of-optimization-hints"></a>최적화 힌트의 이점  
 다음 표에서는 보다 효율적인 스토리지 및 향상된 성능을 지원하는 최적화 힌트를 보여 줍니다.  
  
|최적화 힌트|보다 효율적인 스토리지|성능 향상|  
|-----------------------|----------------------------|--------------------------|  
|**node()**|예|아니오|  
|**SINGLETON**|아니오|예|  
|**DATA TYPE**|예|예|  
|**MAXLENGTH**|예|예|  
  
### <a name="optimization-hints-and-data-types"></a>최적화 힌트 및 데이터 형식  
 노드를 XQuery 데이터 형식 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식으로 인덱싱할 수 있습니다. 다음 표에서는 각 데이터 형식에서 지원되는 최적화 힌트를 보여 줍니다.  
  
|최적화 힌트|XQuery 데이터 형식|SQL 데이터 형식|  
|-----------------------|-----------------------|--------------------|  
|**node()**|예|아니오|  
|**SINGLETON**|예|예|  
|**DATA TYPE**|예|아니오|  
|**MAXLENGTH**|예|아니오|  
  
### <a name="node-optimization-hint"></a>node() 최적화 힌트  
 적용 대상: XQuery 데이터 형식  
  
 node() 최적화를 사용하여 일반 쿼리를 평가하는 데 필요 없는 값을 가진 노드를 지정합니다. 이 힌트는 일반 쿼리가 노드의 존재 여부를 평가하기만 하면 될 때 스토리지 요구 사항을 줄여줍니다. 기본적으로 선택적 XML 인덱스는 복잡한 노드 유형을 제외하고 승격된 모든 노드의 값을 저장합니다.  
  
 다음 예를 살펴 보십시오.  
  
```sql  
SELECT T.record FROM myXMLTable T  
WHERE T.xmldata.exist('/a/b[./c=5]') = 1  
```  
  
 선택적 XML 인덱스를 사용하여 이 쿼리를 평가하려면 `b` 및 `c`노드를 승격시킵니다. 그러나 `b` 노드의 값이 필요 없기 때문에 node() 힌트를 다음 구문과 함께 사용할 수 있습니다.  
  
 `/a/b/ as node()`  
  
 쿼리에 node() 힌트를 사용하여 인덱싱된 노드의 값이 필요한 경우에는 선택적 XML 인덱스를 사용할 수 없습니다.  
  
### <a name="singleton-optimization-hint"></a>SINGLETON 최적화 힌트  
 적용 대상: XQuery 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식  
  
 SINGLETON 최적화 힌트는 노드의 카디널리티를 지정합니다. 이 힌트를 사용하면 노드가 해당 부모 노드 또는 상위 항목에 최대 한 번만 표시된다는 것을 미리 알 수 있기 때문에 쿼리 성능이 향상됩니다.  
  
 이 항목의 [샘플 XML 문서](#sample) 를 살펴보십시오.  
  
 선택적 XML 인덱스를 사용하여 이 문서를 쿼리하려면 `d` 노드에 대해 SINGLETON 힌트를 지정하면 됩니다. 이는 이 노드가 해당 부모 노드에 최대 한 번만 표시되기 때문입니다.  
  
 SINGLETON 힌트가 지정되었지만 노드가 해당 부모 노드 또는 상위 항목에 두 번 이상 표시되면 기존 데이터에 대한 인덱스를 만들거나 새 데이터에 대한 쿼리를 실행할 때 오류가 발생합니다.  
  
### <a name="data-type-optimization-hint"></a>DATA TYPE 최적화 힌트  
 적용 대상: XQuery 데이터 형식  
  
 DATA TYPE 최적화 힌트를 사용하면 인덱싱된 노드에 대해 XQuery 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식을 지정할 수 있습니다. 이 데이터 형식은 선택적 XML 인덱스의 데이터 테이블에서 인덱싱된 노드에 해당하는 열에 사용됩니다.  
  
 기존 값을 지정된 데이터 형식으로 캐스팅하는 작업이 실패해도 인덱스에 대한 삽입 작업은 실패하지 않지만 인덱스의 데이터 테이블에 null 값이 삽입됩니다.  
  
### <a name="maxlength-optimization-hint"></a>MAXLENGTH 최적화 힌트  
 적용 대상: XQuery 데이터 형식  
  
 MAXLENGTH 최적화 힌트를 사용하면 xs:string 데이터의 길이를 제한할 수 있습니다. VARCHAR 또는 NVARCHAR 데이터 형식을 지정할 때 길이를 지정하므로 MAXLENGTH는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식과는 관련이 없습니다.  
  
 기존 문자열이 지정된 MAXLENGTH보다 길면 인덱스에 값을 삽입하는 작업이 실패합니다.  
  
  
##  <a name="sample"></a> 예제용 샘플 XML 문서  
 다음 샘플 XML 문서는 이 항목의 예에서 참조됩니다.  
  
```xml  
<a>  
    <b>  
         <c atc="aa">10</c>  
         <c atc="bb">15</c>  
         <d atd1="dd" atd2="ddd">md </d>  
    </b>  
     <b>  
        <c></c>  
        <c atc="">117</c>  
     </b>  
</a>  
```  
  
  
## <a name="see-also"></a>참고 항목  
 [SXI&#40;선택적 XML 인덱스&#41;](../../relational-databases/xml/selective-xml-indexes-sxi.md)   
 [선택적 XML 인덱스 만들기, 변경 및 삭제](../../relational-databases/xml/create-alter-and-drop-selective-xml-indexes.md)  
  
  
