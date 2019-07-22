---
title: FOR 절(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/08/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- FOR
- FOR CLAUSE
- FOR_TSQL
- FOR_CLAUSE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- XML option [SQL Server]
- BROWSE option
- FOR clause [Transact-SQL]
ms.assetid: 08a6f084-8f73-4f2a-bae4-3c7513dc99b9
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: ad3852f0bb935371fd141cc4ceb98f90c7aa9c19
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67904350"
---
# <a name="select---for-clause-transact-sql"></a>SELECT - FOR 절(Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

FOR 절을 사용하여 쿼리 결과에 대해 다음 옵션 중 하나를 지정합니다.
  
-   **FOR BROWSE**를 지정하여 찾아보기 모드 커서에서 쿼리 결과를 보는 동안 업데이트 할 수 있습니다.  
  
-   **FOR XML**을 지정하여 쿼리 결과를 XML로 서식 지정합니다.  
  
-   **FOR JSON**을 지정하여 쿼리 결과를 JSON으로 서식 저정합니다.  

![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```
[ FOR { BROWSE | <XML> | <JSON>} ]  
  
<XML> ::=  
XML   
{   
    { RAW [ ( 'ElementName' ) ] | AUTO }   
    [   
        <CommonDirectivesForXML>   
        [ , { XMLDATA | XMLSCHEMA [ ( 'TargetNameSpaceURI' ) ] } ]   
        [ , ELEMENTS [ XSINIL | ABSENT ]   
    ]  
  | EXPLICIT   
    [   
        <CommonDirectivesForXML>   
        [ , XMLDATA ]   
    ]  
  | PATH [ ( 'ElementName' ) ]   
    [  
        <CommonDirectivesForXML>   
        [ , ELEMENTS [ XSINIL | ABSENT ] ]  
    ]  
}   
  
<CommonDirectivesForXML> ::=   
[ , BINARY BASE64 ]  
[ , TYPE ]  
[ , ROOT [ ( 'RootName' ) ] ]  
  
<JSON> ::=  
JSON   
{   
    { AUTO | PATH }   
    [   
        [ , ROOT [ ( 'RootName' ) ] ]  
        [ , INCLUDE_NULL_VALUES ]  
        [ , WITHOUT_ARRAY_WRAPPER ]  
    ]  
  
}
```
  
## <a name="for-browse"></a>FOR BROWSE

 BROWSE  
 DB-Library 찾아보기 모드 커서에서 데이터를 표시하는 동안 업데이트를 허용하도록 지정합니다. 테이블에 **timestamp** 열이 있고 고유한 인덱스가 있으며 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스로 전송된 SELECT 문의 끝에 FOR BROWSE 옵션이 있으면 애플리케이션에서 테이블을 찾아볼 수 있습니다.  
  
> [!NOTE]
> FOR BROWSE 옵션을 포함하는 SELECT 문에서는 \<lock_hint> HOLDLOCK을 사용할 수 없습니다.
  
 FOR BROWSE는 UNION 연산자로 조인된 SELECT 문에는 표시되지 않습니다.  
  
> [!NOTE]
> 테이블의 고유 인덱스 키 열이 Null을 허용하고 테이블이 외부 조인의 내부 측면에 있으면 해당 인덱스는 찾아보기 모드에서 지원되지 않습니다.  
  
 찾아보기 모드에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블의 행을 검색하고 테이블의 데이터를 한 번에 한 행씩 업데이트할 수 있습니다. 애플리케이션에서 찾아보기 모드로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블에 액세스하려면 다음 두 가지 옵션 중 하나를 사용해야 합니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블에서 데이터에 액세스하는 데 사용하는 SELECT 문은 **FOR BROWSE** 키워드로 끝나야 합니다. **FOR BROWSE** 옵션을 설정하여 찾아보기 모드를 사용하는 경우 임시 테이블이 생성됩니다.  
  
-   **NO_BROWSETABLE** 옵션을 사용하여 찾아보기 모드를 설정하려면 다음과 같은 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 실행해야 합니다.  
  
    ```sql
    SET NO_BROWSETABLE ON  
    ```  
  
     **NO_BROWSETABLE** 옵션을 설정할 경우 모든 SELECT 문은 **FOR BROWSE** 옵션이 해당 문에 추가된 것처럼 동작합니다. 하지만 **NO_BROWSETABLE** 옵션은 **FOR BROWSE** 옵션이 일반적으로 애플리케이션에 결과를 보내기 위해 사용하는 임시 테이블을 만들지 않습니다.  
  
 찾아보기 모드에서 외부 조인 문을 포함하는 SELECT 쿼리를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블의 데이터에 액세스하려고 하는 경우 및 외부 조인 문의 내부에 존재하는 테이블에 고유 인덱스가 정의되어 있는 경우에는 찾아보기 모드가 고유 인덱스를 지원하지 않습니다. 찾아보기 모드에서는 모든 고유 인덱스 키 열에 Null 값을 사용할 수 있는 경우에만 고유 인덱스를 지원합니다. 찾아보기 모드에서는 다음과 같은 조건을 만족하는 경우 고유 인덱스를 지원하지 않습니다.  
  
-   찾아보기 모드에서 외부 조인 문을 포함하는 SELECT 쿼리를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블의 데이터에 액세스하려고 하는 경우.  
  
-   외부 조인 문의 내부에 있는 테이블에 고유 인덱스가 정의되어 있는 경우.  
  
 찾아보기 모드에서 이 동작을 재현하려면 다음 단계를 수행합니다.  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 SampleDB라는 이름의 데이터베이스를 만듭니다.  
  
2.  SampleDB 데이터베이스에서 c1이라는 단일 열을 각각 포함하는 tleft 테이블과 tright 테이블을 만듭니다. tleft 테이블의 c1 열에 대한 고유 인덱스를 정의하고, Null 값을 허용하도록 해당 열을 설정합니다. 이렇게 하려면 해당하는 쿼리 창에서 다음과 같은 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 실행합니다.  
  
    ```sql
    CREATE TABLE tleft(c1 INT NULL UNIQUE) ;  
    GO   
    CREATE TABLE tright(c1 INT NULL) ;  
    GO  
    ```  
  
3.  tleft 테이블과 tright 테이블에 여러 값을 삽입합니다. tleft 테이블에 Null 값을 삽입합니다. 이렇게 하려면 쿼리 창에서 다음과 같은 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 실행합니다.  
  
    ```sql
    INSERT INTO tleft VALUES(2) ;  
    INSERT INTO tleft VALUES(NULL) ;  
    INSERT INTO tright VALUES(1) ;  
    INSERT INTO tright VALUES(3) ;  
    INSERT INTO tright VALUES(NULL) ;  
    GO  
    ```  
  
4.  **NO_BROWSETABLE** 옵션을 켭니다. 이렇게 하려면 쿼리 창에서 다음과 같은 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 실행합니다.  
  
    ```sql
    SET NO_BROWSETABLE ON ;  
    GO  
    ```  
  
5.  SELECT 쿼리에서 외부 조인 문을 사용하여 tleft 테이블 및 tright 테이블의 데이터에 액세스합니다. tleft 테이블이 외부 조인 문의 내부에 있는지 확인합니다. 이렇게 하려면 쿼리 창에서 다음과 같은 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 실행합니다.  
  
    ```sql
    SELECT tleft.c1   
    FROM tleft   
    RIGHT JOIN tright   
    ON tleft.c1 = tright.c1   
    WHERE tright.c1 <> 2 ;
    ```  
  
     결과 창에서 다음과 같은 출력을 확인합니다.  
  
     c1  
  
     ---\-  
  
     NULL  
  
     NULL  
  
 찾아보기 모드에서 SELECT 쿼리를 실행하여 테이블에 액세스한 후에는 오른쪽 우선 외부 조인 문의 정의로 인해 SELECT 쿼리의 결과 집합에 tleft 테이블의 c1 열에 대한 두 Null 값이 포함됩니다. 따라서 결과 집합에서는 테이블에서 가져온 Null 값과 오른쪽 우선 외부 조인 문으로 인해 발생한 Null 값을 구분할 수 없습니다. 결과 집합의 Null 값을 무시하면 잘못된 결과를 얻을 수 있습니다.  
  
> [!NOTE]
> 고유 인덱스에 포함된 열이 Null 값을 허용하지 않는 경우 결과 집합의 모든 Null 값은 오른쪽 우선 외부 조인 문으로 인해 발생된 것입니다.  
  
## <a name="for-xml"></a>FOR XML

 XML  
 쿼리 결과를 XML 문서로 반환하도록 지정합니다. XML 모드는 RAW, AUTO, EXPLICIT 중 하나로 지정해야 합니다. FOR XML 데이터 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 대한 자세한 내용은 [FOR XML &#40;SQL Server&#41;](../../relational-databases/xml/for-xml-sql-server.md)을 참조하세요.  
  
 RAW [ **('** _ElementName_ **')** ]  
 쿼리 결과를 사용하여 결과 집합의 각 행을 요소 태그로 \<row /> 일반 식별자를 갖는 XML 요소로 변환합니다. 필요에 따라 행 요소에 대한 이름을 지정할 수 있습니다. 결과 XML 출력은 각 행에 대해 행 요소가 생성될 때 지정된 *ElementName* 을 사용합니다. 자세한 내용은 [FOR XML에서 RAW 모드 사용](../../relational-databases/xml/use-raw-mode-with-for-xml.md)을 참조하세요.
  
 AUTO  
 단순하게 중첩된 XML 트리로 쿼리 결과를 반환합니다. 최소한 한 개의 열이 SELECT 절에 나열되는 FROM 절의 각 테이블은 XML 요소로 표시됩니다. SELECT 절에 나열되는 열은 해당 요소의 특성에 매핑됩니다. 자세한 내용은 [FOR XML에서 AUTO 모드 사용](../../relational-databases/xml/use-auto-mode-with-for-xml.md)을 참조하세요.  
  
 EXPLICIT  
 결과 XML 트리 셰이프가 명시적으로 정의되도록 지정합니다. 쿼리는 이 모드를 사용하여 원하는 중첩에 대한 추가 정보가 명시적으로 지정되도록 특정 방식으로 작성되어야 합니다. 자세한 내용은 [FOR XML에서 EXPLICIT 모드 사용](../../relational-databases/xml/use-explicit-mode-with-for-xml.md)을 참조하세요.  
  
 XMLDATA  
 인라인 XDR 스키마를 반환하지만 결과에 루트 요소를 추가하지는 않습니다. XMLDATA를 지정하면 문서에 XDR 스키마가 첨부됩니다.  
  
> [!IMPORTANT]
> XMLDATA 지시문은 **더 이상 사용되지 않습니다**. RAW 및 AUTO 모드의 경우 XSD 생성을 사용하세요. EXPLICIT 모드의 XMLDATA 지시어의 경우에는 대체할 옵션이 없습니다. [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  

_원치 않는 줄 바꿈을 표시 안 함:_ SSMS(SQL Server Management Studio)를 사용하여 FOR XML 절을 사용하는 쿼리를 실행할 수 있습니다. 때로는 많은 양의 XML이 반환되어 하나의 그리드 셀에 표시됩니다. XML 문자열은 단일 줄에 보유할 수 있는 하나의 SSMS 그리드 셀보다 길 수 있습니다. 이러한 경우 SSMS는 전체 XML 문자열의 긴 세그먼트 사이에 줄 바꿈 문자를 삽입할 수 있습니다. 이러한 줄 바꿈은 줄을 분할하지 않아야 하는 하위 문자열의 중간에서 발생할 수 있습니다. 캐스트 AS XMLDATA를 사용하여 줄 바꿈을 방지할 수 있습니다. FOR JSON PATH를 사용하는 경우에 이 솔루션을 적용할 수도 있습니다. 이 기술은 Stack Overflow에서 설명되고 다음 Transact-SQL 샘플 SELECT 문에 표시됩니다.

- [SQL Server FOR XML 사용: 결과 데이터 형식을 Text/varchar/string으로 변환하시겠습니까?](https://stackoverflow.com/questions/5655332/using-sql-server-for-xml-convert-result-datatype-to-text-varchar-string-whate/5658758#5658758)

    ```sql
    SELECT CAST(
        (SELECT column1, column2
            FROM my_table
            FOR XML PATH('')
        )
            AS VARCHAR(MAX)
    ) AS XMLDATA ;
    ```

<!-- The preceding Stack Overflow example is per MicrosoftDocs/sql-docs Issue 1501.  2019-01-06 -->

 XMLSCHEMA [ **('** _TargetNameSpaceURI_ **')** ]  
 인라인 XSD 스키마를 반환합니다. 이 지시어를 지정할 때 스키마에 지정된 네임스페이스를 반환하는 대상 네임스페이스 URI를 필요에 따라 지정할 수 있습니다. 자세한 내용은 [인라인 XSD 스키마 생성](../../relational-databases/xml/generate-an-inline-xsd-schema.md)을 참조하세요.  
  
 ELEMENTS  
 열을 하위 요소로 반환하도록 지정합니다. 그렇지 않은 경우에는 XML 특성에 매핑됩니다. 이 옵션은 RAW, AUTO 및 PATH 모드에서만 지원됩니다. 자세한 내용은 [FOR XML에서 RAW 모드 사용](../../relational-databases/xml/use-raw-mode-with-for-xml.md)을 참조하세요.  
  
 XSINIL  
 **True**로 설정된 **xsi:nil** 특성이 있는 요소가 NULL 열 값에 대해 생성되도록 지정합니다. 이 옵션은 ELEMENTS 지시어에만 지정할 수 있습니다. 참조 항목:

- [XSINIL 매개 변수를 사용하여 NULL 값에 대한 요소를 생성합니다](../../relational-databases/xml/generate-elements-for-null-values-with-the-xsinil-parameter.md).
- [SELECT 문에 대한 FOR XML](../../relational-databases/xml/for-xml-sql-server.md)
  
 ABSENT  
 Null 열 값에서는 해당 XML 요소가 XML 결과에 추가되지 않음을 나타냅니다. 이 옵션은 ELEMENTS에만 지정하세요.  
  
 PATH [ **('** _ElementName_ **')** ]  
 결과 집합의 각 행에 대해 \<row> 요소 래퍼를 생성합니다. 필요에 따라 \<row> 요소 래퍼에 대한 요소 이름을 지정할 수 있습니다. FOR XML PATH( **''** )와 같은 빈 문자열이 지정된 경우 래퍼 요소가 생성되지 않습니다. EXPLICIT 지시어를 사용하여 작성된 쿼리 대신 PATH를 사용하는 것이 더 간단한 방법일 수 있습니다. 자세한 내용은 [FOR XML에서 PATH 모드 사용](../../relational-databases/xml/use-path-mode-with-for-xml.md)을 참조하세요.  
  
 BINARY BASE64  
 쿼리에서 이진 데이터를 이진 base64 인코드 형식으로 반환하도록 지정합니다. RAW 및 EXPLICIT 모드를 사용하여 이진 데이터를 검색하는 경우 이 옵션을 지정해야 합니다. 이 값은 AUTO 모드에서 기본값입니다.  
  
 TYPE  
 쿼리가 결과를 **xml** 형식으로 반환하도록 지정합니다. 자세한 내용은 [TYPE Directive in FOR XML Queries](../../relational-databases/xml/type-directive-in-for-xml-queries.md)를 참조하세요.  
  
 ROOT [ **('** _RootName_ **')** ]  
 단일 최상위 요소가 결과 XML에 추가되도록 지정합니다. 필요에 따라 생성할 루트 요소 이름을 지정할 수 있습니다. 선택 사항인 루트 이름을 지정하지 않으면 기본 \<root> 요소가 추가됩니다.  
  
 자세한 내용은 [FOR XML&#40;SQL Server&#41;](../../relational-databases/xml/for-xml-sql-server.md)을 참조하세요.  
  
 **FOR XML Example**  
  
 다음 예에서는 `FOR XML AUTO`를 `TYPE` 및 `XMLSCHEMA` 옵션을 사용하여 지정합니다. `TYPE` 옵션으로 인해 결과 집합은 **xml** 형식으로 클라이언트에 반환됩니다. `XMLSCHEMA` 옵션은 반환되는 XML 데이터에 인라인 XSD 스키마가 포함되도록 지정하며 `ELEMENTS` 옵션은 XML 결과가 요소 중심이 되도록 지정합니다.  
  
```sql
USE AdventureWorks2012;  
GO  
SELECT p.BusinessEntityID, FirstName, LastName, PhoneNumber AS Phone  
FROM Person.Person AS p  
JOIN Person.PersonPhone AS pph ON p.BusinessEntityID  = pph.BusinessEntityID  
WHERE LastName LIKE 'G%'  
ORDER BY LastName, FirstName   
FOR XML AUTO, TYPE, XMLSCHEMA, ELEMENTS XSINIL;  
```  
  
## <a name="for-json"></a>FOR JSON

 JSON  
 JSON 텍스트로 서식 지정된 쿼리의 결과를 반환하려면 FOR JSON을 지정합니다. 또한 다음 JSON 모드 중 하나를 지정해야 합니다. AUTO 또는 PATH. 자세한 내용은 **FOR JSON**을 사용하여 [쿼리 결과 서식을 JSON으로 지정&#40;SQL Server&#41;](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md)을 참조하세요.  
  
 AUTO  
 **SELECT** 문의 구조에 따라 JSON 출력 형식을 자동으로 서식 지정하려면  
            **FOR JSON AUTO**을 지정합니다. 자세한 내용과 예제는 [AUTO 모드를 사용하여 JSON 출력 형식 자동 지정&#40;SQL Server&#41;](../../relational-databases/json/format-json-output-automatically-with-auto-mode-sql-server.md)을 참조하세요.  
  
 PATH  
 JSON 출력의 형식을 완전하게 제어하려면   
            **FOR JSON PATH**를 지정합니다. **PATH** 모드를 통해 래퍼 개체를 만들고 복잡한 속성을 중첩할 수 있습니다. 자세한 내용과 예제는 [PATH 모드로 중첩 JSON 출력 서식 지정&#40;SQL Server&#41;](../../relational-databases/json/format-nested-json-output-with-path-mode-sql-server.md)을 참조하세요.  
  
 INCLUDE_NULL_VALUES  
 **FOR JSON** 절과 함께 **INCLUDE_NULL_VALUES** 옵션을 지정하여 JSON 출력에 null 값을 포함합니다. 이 옵션을 지정하지 않은 경우 쿼리 결과의 NULL 값에 대해서는 출력에 JSON 속성을 포함하지 않습니다. 자세한 내용 및 예제는 [INCLUDE_NULL_VALUES 옵션을 사용하여 JSON 출력에 Null 값 포함&#40;SQL Server&#41;](../../relational-databases/json/include-null-values-in-json-include-null-values-option.md)을 참조하세요.  
  
 ROOT [ **('** _RootName_ **')** ]  
 단일 최상위 요소를 JSON 출력에 추가하려면 **FOR JSON** 절을 사용하여 **ROOT** 옵션을 지정합니다. **ROOT** 옵션을 지정하지 않은 경우 JSON 출력에는 루트 요소가 없습니다. 자세한 내용 및 예제는 [ROOT 옵션을 사용하여 JSON 출력에 루트 노드 추가&#40;SQL Server&#41;](../../relational-databases/json/add-a-root-node-to-json-output-with-the-root-option-sql-server.md).  
  
 WITHOUT_ARRAY_WRAPPER  
 기본적으로 JSON 출력을 둘러싸고 있는 대괄호를 제거하려면 **FOR JSON** 절을 사용하여 **WITHOUT_ARRAY_WRAPPER** 옵션을 지정합니다. 이 옵션을 지정하지 않으면 JSON 출력은 대괄호로 묶입니다. 단일 JSON 객체를 출력으로 생성하려면 **WITHOUT_ARRAY_WRAPPER** 옵션을 사용합니다.  자세한 내용은 [WITHOUT_ARRAY_WRAPPER 옵션을 사용하여 JSON 출력에서 대괄호 제거&#40;SQL Server&#41;](../../relational-databases/json/remove-square-brackets-from-json-without-array-wrapper-option.md).  
  
 자세한 내용은 [FOR JSON을 사용하여 쿼리 결과를 JSON으로 서식 지정&#40;SQL Server&#41;](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목

 [SELECT&#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)

