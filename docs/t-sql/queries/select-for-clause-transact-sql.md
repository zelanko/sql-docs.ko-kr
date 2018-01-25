---
title: "FOR 절 (Transact SQL) | Microsoft Docs"
ms.custom: 
ms.date: 08/09/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|queries
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- FOR
- FOR CLAUSE
- FOR_TSQL
- FOR_CLAUSE_TSQL
dev_langs: TSQL
helpviewer_keywords:
- XML option [SQL Server]
- BROWSE option
- FOR clause [Transact-SQL]
ms.assetid: 08a6f084-8f73-4f2a-bae4-3c7513dc99b9
caps.latest.revision: "54"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 085a9c7f6422c70cc43086d2174a5c7aa485040e
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="select---for-clause-transact-sql"></a>선택-FOR 절 (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  FOR 절을 사용 하 여 쿼리 결과 대해 다음 옵션 중 하나를 지정 합니다.  
  
-   찾아보기 모드 커서에서 지정 하 여 쿼리 결과 보는 동안 업데이트 허용 **FOR BROWSE**합니다.  
  
-   지정 하 여 XML 쿼리 결과 서식을 **FOR XML**합니다.  
  
-   지정 하 여 쿼리 결과 JSON으로 서식 지정 **FOR JSON**합니다.  
  
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
 DB-Library 찾아보기 모드 커서에서 데이터를 표시하는 동안 업데이트를 허용하도록 지정합니다. 테이블에 포함 된 경우 응용 프로그램에서 테이블을 찾아볼 수 있습니다는 **타임 스탬프** 열, 테이블에 고유 인덱스 및의 인스턴스로 전송 된 SELECT 문의 끝에 FOR BROWSE 옵션은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.  
  
> [!NOTE]  
>  사용할 수 없습니다는 \<c k _ h > FOR BROWSE 옵션이 포함 된 SELECT 문에서 HOLDLOCK입니다.
  
 FOR BROWSE는 UNION 연산자로 조인된 SELECT 문에는 표시되지 않습니다.  
  
> [!NOTE]  
>  테이블의 고유 인덱스 키 열이 Null을 허용하고 테이블이 외부 조인의 내부 측면에 있으면 해당 인덱스는 찾아보기 모드에서 지원되지 않습니다.  
  
 찾아보기 모드에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블의 행을 검색하고 테이블의 데이터를 한 번에 한 행씩 업데이트할 수 있습니다. 액세스는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블 찾아보기 모드에서 응용 프로그램에서 사용 해야 다음 두 가지 옵션 중 하나:  
  
-   데이터에 액세스를 사용 하는 SELECT 문에서 프로그램 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 키워드로 끝나야 합니다. 테이블 **FOR BROWSE**합니다. 켜면는 **FOR BROWSE** 찾아보기 모드를 사용 하도록 옵션을 임시 테이블이 만들어집니다.  
  
-   다음을 실행 해야 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 사용 하 여 찾아보기 모드 설정에 **NO_BROWSETABLE** 옵션:  
  
    ```  
    SET NO_BROWSETABLE ON  
    ```  
  
     켜면는 **NO_BROWSETABLE** 작동 하는 SELECT 문의 모든 옵션 처럼는 **FOR BROWSE** 옵션이 해당 문에 추가 됩니다. 그러나는 **NO_BROWSETABLE** 옵션 만들어지지 않습니다 임시 테이블 하는 **FOR BROWSE** 옵션 일반적으로 사용 하 여 응용 프로그램에 결과 보냅니다.  
  
 데이터에 액세스 하려고 하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 외부 조인 문을 포함 하는 SELECT 쿼리를 사용 하 여 찾아보기 모드에서 테이블 및 찾아보기 모드 sup 하지 않는 외부 조인 문의 내부 측면에 있는 테이블에 고유 인덱스가 정의 고유 인덱스 포트입니다. 찾아보기 모드에서는 모든 고유 인덱스 키 열에 Null 값을 사용할 수 있는 경우에만 고유 인덱스를 지원합니다. 찾아보기 모드에서는 다음과 같은 조건을 만족하는 경우 고유 인덱스를 지원하지 않습니다.  
  
-   데이터에 액세스 하려고 하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 외부 조인 문을 포함 하는 SELECT 쿼리를 사용 하 여 찾아보기 모드에 있는 테이블입니다.  
  
-   외부 조인 문의 내부에 있는 테이블에 고유 인덱스가 정의되어 있는 경우.  
  
 찾아보기 모드에서 이 동작을 재현하려면 다음 단계를 수행합니다.  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 SampleDB라는 이름의 데이터베이스를 만듭니다.  
  
2.  SampleDB 데이터베이스에서 c1이라는 단일 열을 각각 포함하는 tleft 테이블과 tright 테이블을 만듭니다. tleft 테이블의 c1 열에 대한 고유 인덱스를 정의하고, Null 값을 허용하도록 해당 열을 설정합니다. 이렇게 하려면 해당하는 쿼리 창에서 다음과 같은 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 실행합니다.  
  
    ```  
    CREATE TABLE tleft(c1 INT NULL UNIQUE) ;  
    GO   
    CREATE TABLE tright(c1 INT NULL) ;  
    GO  
    ```  
  
3.  tleft 테이블과 tright 테이블에 여러 값을 삽입합니다. tleft 테이블에 Null 값을 삽입합니다. 이렇게 하려면 쿼리 창에서 다음과 같은 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 실행합니다.  
  
    ```  
    INSERT INTO tleft VALUES(2) ;  
    INSERT INTO tleft VALUES(NULL) ;  
    INSERT INTO tright VALUES(1) ;  
    INSERT INTO tright VALUES(3) ;  
    INSERT INTO tright VALUES(NULL) ;  
    GO  
    ```  
  
4.  설정의 **NO_BROWSETABLE** 옵션입니다. 이렇게 하려면 쿼리 창에서 다음과 같은 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 실행합니다.  
  
    ```  
    SET NO_BROWSETABLE ON ;  
    GO  
    ```  
  
5.  SELECT 쿼리에서 외부 조인 문을 사용하여 tleft 테이블 및 tright 테이블의 데이터에 액세스합니다. tleft 테이블이 외부 조인 문의 내부에 있는지 확인합니다. 이렇게 하려면 쿼리 창에서 다음과 같은 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 실행합니다.  
  
    ```  
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
>  고유 인덱스에 포함된 열이 Null 값을 허용하지 않는 경우 결과 집합의 모든 Null 값은 오른쪽 우선 외부 조인 문으로 인해 발생된 것입니다.  
  
## <a name="for-xml"></a>FOR XML  
 XML  
 쿼리 결과를 XML 문서로 반환하도록 지정합니다. XML 모드 중 하나를 지정 해야 합니다: RAW, AUTO, EXPLICIT입니다. XML 데이터에 대 한 자세한 내용은 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], 참조 [FOR xml&#40; SQL Server &#41; ](../../relational-databases/xml/for-xml-sql-server.md).  
  
 원시 [ **('***ElementName***')** ]  
 쿼리 결과 일반 식별자를 갖는 XML 요소로 설정 하 여 결과의 각 행을 변환 \<행 / > 요소 태그로 합니다. 필요에 따라 행 요소에 대한 이름을 지정할 수 있습니다. 결과 XML 출력은 지정 된를 사용 하 여 *ElementName* 으로 각 행에 대해 생성 된 행 요소입니다. 자세한 내용은 참조 [FOR XML RAW 모드 사용](../../relational-databases/xml/use-raw-mode-with-for-xml.md) 및 [FOR XML RAW 모드 사용](../../relational-databases/xml/use-raw-mode-with-for-xml.md)합니다.  
  
 AUTO  
 단순하게 중첩된 XML 트리로 쿼리 결과를 반환합니다. 최소한 한 개의 열이 SELECT 절에 나열되는 FROM 절의 각 테이블은 XML 요소로 표시됩니다. SELECT 절에 나열되는 열은 해당 요소의 특성에 매핑됩니다. 자세한 내용은 [FOR XML에서 AUTO 모드 사용](../../relational-databases/xml/use-auto-mode-with-for-xml.md)을 참조하세요.  
  
 EXPLICIT  
 결과 XML 트리 셰이프가 명시적으로 정의되도록 지정합니다. 쿼리는 이 모드를 사용하여 원하는 중첩에 대한 추가 정보가 명시적으로 지정되도록 특정 방식으로 작성되어야 합니다. 자세한 내용은 [FOR XML에서 EXPLICIT 모드 사용](../../relational-databases/xml/use-explicit-mode-with-for-xml.md)을 참조하세요.  
  
 XMLDATA  
 인라인 XDR 스키마를 반환하지만 결과에 루트 요소를 추가하지는 않습니다. XMLDATA를 지정하면 문서에 XDR 스키마가 첨부됩니다.  
  
> [!IMPORTANT]  
>  XMLDATA 지시어의 경우 사용 되지 않습니다. RAW 및 AUTO 모드의 경우 XSD 생성을 사용하세요. EXPLICIT 모드의 XMLDATA 지시어의 경우에는 대체할 옵션이 없습니다. [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 XMLSCHEMA [ **('***TargetNameSpaceURI***')** ]  
 인라인 XSD 스키마를 반환합니다. 이 지시어를 지정할 때 스키마에 지정된 네임스페이스를 반환하는 대상 네임스페이스 URI를 필요에 따라 지정할 수 있습니다. 자세한 내용은 [인라인 XSD 스키마 생성](../../relational-databases/xml/generate-an-inline-xsd-schema.md)을 참조하세요.  
  
 ELEMENTS  
 열을 하위 요소로 반환하도록 지정합니다. 그렇지 않은 경우에는 XML 특성에 매핑됩니다. 이 옵션은 RAW, AUTO 및 PATH 모드에서만 지원됩니다. 자세한 내용은 [FOR XML에서 RAW 모드 사용](../../relational-databases/xml/use-raw-mode-with-for-xml.md)을 참조하세요.  
  
 XSINIL  
 지정 된 요소가 **xsi: nil** 특성이로 설정 **True** NULL 열 값에 대해 만들 수입니다. 이 옵션은 ELEMENTS 지시어에만 지정할 수 있습니다. 자세한 내용은 참조 [XSINIL 매개 변수를 사용 하 여 NULL 값 요소 생성](../../relational-databases/xml/generate-elements-for-null-values-with-the-xsinil-parameter.md)합니다.  
  
 ABSENT  
 Null 열 값에서는 해당 XML 요소가 XML 결과에 추가되지 않음을 나타냅니다. 이 옵션은 ELEMENTS에만 지정하세요.  
  
 PATH [ **('***ElementName***')** ]  
 생성 된 \<행 > 요소 래퍼는 결과 집합의 각 행에 대 한 합니다. 요소 이름에 대 한 선택적으로 지정할 수 있습니다는 \<행 > 요소 래퍼 합니다. FOR XML PATH와 같은 경우 빈 문자열이 제공 됩니다 (**'**)), 래퍼 요소가 생성 되지 않습니다. EXPLICIT 지시어를 사용하여 작성된 쿼리 대신 PATH를 사용하는 것이 더 간단한 방법일 수 있습니다. 자세한 내용은 [FOR XML에서 PATH 모드 사용](../../relational-databases/xml/use-path-mode-with-for-xml.md)을 참조하세요.  
  
 BINARY BASE64  
 쿼리에서 이진 데이터를 이진 base64 인코드 형식으로 반환하도록 지정합니다. RAW 및 EXPLICIT 모드를 사용하여 이진 데이터를 검색하는 경우 이 옵션을 지정해야 합니다. 이 값은 AUTO 모드에서 기본값입니다.  
  
 TYPE  
 쿼리 결과를 반환 하도록 지정 **xml** 유형입니다. 자세한 내용은 [TYPE Directive in FOR XML Queries](../../relational-databases/xml/type-directive-in-for-xml-queries.md)를 참조하세요.  
  
 ROOT [ **('***RootName***')** ]  
 단일 최상위 요소가 결과 XML에 추가되도록 지정합니다. 필요에 따라 생성할 루트 요소 이름을 지정할 수 있습니다. 선택 사항인 루트 이름을 지정 하지 않으면 기본 \<루트 > 요소가 추가 됩니다.  
  
 자세한 내용은 참조 하십시오. [FOR xml&#40; SQL Server &#41; ](../../relational-databases/xml/for-xml-sql-server.md).  
  
 **XML 예제에 대 한**  
  
 다음 예에서는 `FOR XML AUTO`를 `TYPE` 및 `XMLSCHEMA` 옵션을 사용하여 지정합니다. 때문에 `TYPE` 옵션을 결과 집합으로 클라이언트에 반환 되는 **xml** 유형입니다. `XMLSCHEMA` 옵션은 반환되는 XML 데이터에 인라인 XSD 스키마가 포함되도록 지정하며 `ELEMENTS` 옵션은 XML 결과가 요소 중심이 되도록 지정합니다.  
  
```  
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
 쿼리 결과를 반환할 지정에 대 한 JSON JSON 텍스트로 형식이 지정 된 합니다. 또한 다음 JSON 모드 중 하나를 지정 해야: 자동 또는 경로입니다. 에 대 한 자세한 내용은 **FOR JSON** 절 참조 [쿼리 결과 FOR JSON &#40; 있는 JSON으로 서식 지정 SQL Server &#41; ](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md).  
  
 AUTO  
 형식은 JSON 자동으로 출력의 구조에 따라는 **선택** 문  
            지정 하 여 **FOR JSON AUTO**합니다. 자세한 내용과 예제는 [AUTO 모드를 사용하여 JSON 출력 형식 자동 지정&#40;SQL Server&#41;](../../relational-databases/json/format-json-output-automatically-with-auto-mode-sql-server.md)을 참조하세요.  
  
 PATH  
 JSON 출력의 형식에 대 한 모든 권한을 지정 하 여 가져오기   
            **FOR JSON PATH**합니다. **PATH** 모드를 통해 래퍼 개체를 만들고 복잡한 속성을 중첩할 수 있습니다. 자세한 내용과 예제는 [PATH 모드로 중첩 JSON 출력 서식 지정&#40;SQL Server&#41;](../../relational-databases/json/format-nested-json-output-with-path-mode-sql-server.md)을 참조하세요.  
  
 INCLUDE_NULL_VALUES  
 지정 하 여 JSON 출력에 null 값이 포함 된 **INCLUDE_NULL_VALUES** 옵션과 함께 **FOR JSON** 절. 이 옵션을 지정 하지 않는 경우 출력은 null 값에 대 한 JSON 속성 쿼리 결과에 포함 되지 않습니다. 자세한 내용과 예제에 대 한 참조 [INCLUDE_NULL_VALUES 옵션 &#40;를 사용 하 여 JSON 출력에서 Null 값 포함 SQL Server &#41; ](../../relational-databases/json/include-null-values-in-json-include-null-values-option.md).  
  
 ROOT [ **('***RootName***')** ]  
 단일 최상위 요소를 지정 하 여 JSON 출력에 추가 된 **루트** 옵션과 함께 **FOR JSON** 절. **ROOT** 옵션을 지정하지 않은 경우 JSON 출력에는 루트 요소가 없습니다. 자세한 내용과 예제에 대 한 참조 [루트 옵션 &#40;를 사용 하 여 JSON 출력에 루트 노드 추가 SQL Server &#41; ](../../relational-databases/json/add-a-root-node-to-json-output-with-the-root-option-sql-server.md).  
  
 WITHOUT_ARRAY_WRAPPER  
 기본적으로 지정 하 여 JSON 출력을 둘러싸고 있는 대괄호를 제거는 **WITHOUT_ARRAY_WRAPPER** 옵션과 함께 **FOR JSON** 절. 이 옵션을 지정하지 않으면 JSON 출력은 대괄호로 묶입니다. 사용 하 여 **WITHOUT_ARRAY_WRAPPER** 단일 JSON 개체를 출력으로 생성 하는 옵션입니다.  자세한 내용은 [WITHOUT_ARRAY_WRAPPER 옵션을 사용하여 JSON 출력에서 대괄호 제거&#40;SQL Server&#41;](../../relational-databases/json/remove-square-brackets-from-json-without-array-wrapper-option.md).  
  
 자세한 내용은 [FOR JSON을 사용하여 쿼리 결과를 JSON으로 서식 지정&#40;SQL Server&#41;](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [SELECT &#40;TRANSACT-SQL&#41;](../../t-sql/queries/select-transact-sql.md)  
  
  
