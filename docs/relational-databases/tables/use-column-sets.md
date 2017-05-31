---
title: "열 집합 사용 | Microsoft 문서"
ms.custom: 
ms.date: 07/30/2015
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-tables
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- sparse columns, column sets
- column sets
ms.assetid: a4f9de95-dc8f-4ad8-b957-137e32bfa500
caps.latest.revision: 28
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 7ae01121fcb9c3cfaf67297fee281979a7ee8627
ms.contentlocale: ko-kr
ms.lasthandoff: 04/11/2017

---
# <a name="use-column-sets"></a>열 집합 사용
[!INCLUDE[tsql-appliesto-ss2016-all_md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  스파스 열을 사용하는 테이블에서는 테이블의 모든 스파스 열을 반환하는 열 집합을 지정할 수 있습니다. 열 집합은 구조화된 출력으로 테이블의 모든 스파스 열을 결합하는 형식화되지 않은 XML 표현입니다. 열 집합은 열 집합이 테이블에 물리적으로 저장되지 않는다는 점에서 계산 열과 유사하며, 직접 업데이트할 수 있다는 점에서 계산 열과 다릅니다.  
  
 테이블의 열 수가 많고 이러한 열을 개별적으로 작업하는 것이 복잡한 경우 열 집합을 사용하는 것이 좋습니다. 응용 프로그램에서 열이 많은 테이블의 열 집합을 사용하여 데이터를 선택하고 삽입하는 경우 성능이 약간 향상될 수도 있습니다. 그러나 테이블의 열에 많은 인덱스가 정의되어 있는 경우 열 집합의 성능이 저하될 수 있습니다. 왜냐하면 실행 계획에 필요한 메모리 양이 늘어나기 때문입니다.  
  
 열 집합을 정의하려면 [CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md) 또는 [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) 문에 *<column_set_name>* FOR ALL_SPARSE_COLUMNS 키워드를 사용합니다.  
  
## <a name="guidelines-for-using-column-sets"></a>열 집합 사용 지침  
 열 집합을 사용하는 경우 다음 지침을 고려합니다.  
  
-   스파스 열 및 열 집합을 동일한 문의 일부로 추가할 수 있습니다.  
  
-   테이블에 스파스 열이 이미 포함되어 있는 경우 해당 테이블에 열 집합을 추가할 수 없습니다.  
  
-   열 집합은 변경할 수 없습니다. 열 집합을 변경하려면 스파스 열 및 열 집합을 삭제한 다음 다시 만들어야 합니다.  
  
-   스파스 열을 포함하지 않는 테이블에 열 집합을 추가할 수 있습니다. 스파스 열이 나중에 테이블에 추가되면 열 집합에 표시됩니다.  
  
-   테이블당 열 집합 하나만 허용됩니다.  
  
-   열 집합은 선택 사항이며 스파스 열을 사용하지 않아도 됩니다.  
  
-   열 집합에 제약 조건 또는 기본값을 정의할 수 없습니다.  
  
-   계산 열은 열 집합 열을 포함할 수 없습니다.  
  
-   열 집합을 포함하는 테이블에서는 분산 쿼리가 지원되지 않습니다.  
  
-   복제는 열 집합을 지원하지 않습니다.  
  
-   변경 데이터 캡처에서 열 집합을 지원하지 않습니다.  
  
-   열 집합은 어떠한 인덱스 종류의 일부도 될 수 없습니다. 여기에는 XML 인덱스, 전체 텍스트 인덱스 및 인덱싱된 뷰가 포함됩니다. 열 집합은 인덱스의 포괄 열로 추가될 수 없습니다.  
  
-   열 집합은 필터링된 인덱스 또는 필터링된 통계의 필터 식에 사용할 수 없습니다.  
  
-   뷰에 열 집합이 포함되어 있으면 열 집합이 뷰에서 XML 열로 표시됩니다.  
  
-   열 집합은 인덱싱된 뷰 정의에 포함될 수 없습니다.  
  
-   열 집합을 포함하는 테이블이 있는 분할 뷰가 이름별로 스파스 열을 지정하면 해당 분할 뷰를 업데이트할 수 있습니다. 분할 뷰가 열 집합을 참조하면 해당 분할 뷰를 업데이트할 수 없습니다.  
  
-   열 집합을 참조하는 쿼리 알림은 허용되지 않습니다.  
  
-   XML 데이터의 크기 제한이 2GB입니다. 행에서 Null이 아닌 모든 스파스 열의 결합된 데이터가 이 제한을 초과하면 쿼리 또는 DML 작업에서 오류가 발생합니다.  
  
-   COLUMNS_UPDATED 함수에서 반환되는 데이터에 대한 자세한 내용은 [스파스 열 사용](../../relational-databases/tables/use-sparse-columns.md)을 참조하세요.  
  
## <a name="guidelines-for-selecting-data-from-a-column-set"></a>열 집합 데이터 선택 지침  
 열 집합에서 데이터를 선택하는 경우 다음 지침을 고려합니다.  
  
-   이론적으로 열 집합은 기본 관계형 열 집합을 단일 XML 표현으로 집계하는 업데이트 가능 XML 계산 열 유형입니다. 열 집합은 ALL_SPARSE_COLUMNS 속성만 지원합니다. 이 속성은 특정 행에 대해 모든 스파스 열의 Null이 아닌 값을 모두 집계하는 데 사용됩니다.  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 테이블 편집기에서 열 집합은 편집할 수 있는 XML 필드로 표시됩니다. 열 집합을 다음 형식으로 정의합니다.  
  
    ```  
    <column_name_1>value1</column_name_1><column_name_2>value2</column_name_2>...  
    ```  
  
     열 집합 값의 예는 다음과 같습니다.  
  
    -   `<sparseProp1>10</sparseProp1><sparseProp3>20</sparseProp3>`  
  
    -   `<DocTitle>Bicycle Parts List</DocTitle><Region>West</Region>`  
  
-   Null 값을 포함하는 스파스 열은 열 집합에 대한 XML 표현에서 생략됩니다.  
  
> [!WARNING]  
>  열 집합을 추가하면 SELECT * 쿼리 동작이 변경됩니다. 쿼리는 열 집합을 XML 열로 반환하며 개별 스파스 열을 반환하지 않습니다. 스키마 디자이너 및 소프트웨어 개발자는 기존 응용 프로그램에서 오류가 발생하지 않도록 주의해야 합니다.  
  
## <a name="inserting-or-modifying-data-in-a-column-set"></a>열 집합에서 데이터 삽입 또는 수정  
 개별 열 이름을 사용하거나 열 집합의 XML 형식을 통해 열 집합의 이름을 참조하고 열 집합의 값을 지정하여 스파스 열의 데이터 조작 작업을 수행할 수 있습니다. 스파스 열은 XML 열에서 어떤 순서로도 표시될 수 있습니다.  
  
 XML 열 집합을 사용하여 스파스 열 값을 삽입하거나 업데이트하는 경우 기본 스파스 열에 삽입된 값은 **xml** 데이터 형식에서 암시적으로 변환됩니다. 숫자 열의 경우 XML 숫자 열에 있는 빈 값이 빈 문자열로 변환됩니다. 이로 인해 다음 예에서처럼 0이 숫자 열에 삽입됩니다.  
  
```  
CREATE TABLE t (i int SPARSE, cs xml column_set FOR ALL_SPARSE_COLUMNS);  
GO  
INSERT t(cs) VALUES ('<i/>');  
GO  
SELECT i FROM t;  
GO  
```  
  
 이 예에서는 열 `i`에 값이 지정되지 않았지만 값 `0` 이 삽입되었습니다.  
  
## <a name="using-the-sqlvariant-data-type"></a>sql_variant 데이터 형식 사용  
 **sql_variant** 데이터 형식은 **int**, **char**및 **date**와 같은 여러 다른 데이터 형식을 저장할 수 있습니다. 열 집합은 **sql_variant** 값에 연결된 소수 자릿수, 전체 자릿수 및 로캘 정보와 같은 데이터 형식 정보를 생성된 XML 열에서 특성으로 출력합니다. 사용자 지정하여 생성된 XML 문에 있는 이러한 특성을 열 집합의 삽입 또는 업데이트 작업에 대한 입력으로 제공하려는 경우에는 이 특성 중 일부가 필요하여 이러한 일부 특성에 기본값이 할당됩니다. 다음 표에서는 데이터 형식과 값이 제공되지 않은 경우 서버에서 생성하는 기본값을 나열합니다.  
  
|데이터 형식|localeID*|sqlCompareOptions|sqlCollationVersion|SqlSortId|최대 길이|전체 자릿수|소수 자릿수|  
|---------------|----------------|-----------------------|-------------------------|---------------|--------------------|---------------|-----------|  
|**char**, **varchar**, **binary**|-1|'기본값'|0|0|8000|해당 사항 없음**|해당 사항 없음|  
|**nvarchar**|-1|'기본값'|0|0|4000|해당 사항 없음|해당 사항 없음|  
|**decimal**, **float**, **real**|해당 사항 없음|해당 사항 없음|해당 사항 없음|해당 사항 없음|해당 사항 없음|18|0|  
|**integer**, **bigint**, **tinyint**, **smallint**|해당 사항 없음|해당 사항 없음|해당 사항 없음|해당 사항 없음|해당 사항 없음|해당 사항 없음|해당 사항 없음|  
|**datetime2**|해당 사항 없음|해당 사항 없음|해당 사항 없음|해당 사항 없음|해당 사항 없음|해당 사항 없음|7|  
|**datetime offset**|해당 사항 없음|해당 사항 없음|해당 사항 없음|해당 사항 없음|해당 사항 없음|해당 사항 없음|7|  
|**datetime**, **date**, **smalldatetime**|해당 사항 없음|해당 사항 없음|해당 사항 없음|해당 사항 없음|해당 사항 없음|해당 사항 없음|해당 사항 없음|  
|**money**, **smallmoney**|해당 사항 없음|해당 사항 없음|해당 사항 없음|해당 사항 없음|해당 사항 없음|해당 사항 없음|해당 사항 없음|  
|**time**|해당 사항 없음|해당 사항 없음|해당 사항 없음|해당 사항 없음|해당 사항 없음|해당 사항 없음|7|  
  
 \*  localeID -1은 기본 로캘을 의미합니다. 영어 로캘은 1033입니다.  
  
 **  해당 사항 없음 = 열 집합에서 선택 작업을 수행하는 동안 이 특성에 대해 값이 출력되지 않습니다. 삽입 또는 업데이트 작업에서 열 집합에 대해 제공된 XML 표현의 호출자에 의해 이 특성에 대한 값이 지정된 경우 오류를 생성합니다.  
  
## <a name="security"></a>보안  
 열 집합에 대한 보안 모델은 테이블과 열 사이에 존재하는 보안 모델과 유사하게 작동합니다. 열 집합은 미니 테이블로 시각화할 수 있으며 선택 작업은 이 미니 테이블에 대한 SELECT * 작업과 유사합니다. 그러나 스파스 열에 대한 열 집합 간 관계는 엄격히 말해 컨테이너가 아닌 그룹화 관계입니다. 보안 모델은 열 집합 열의 보안을 검사하고 기본 스파스 열의 DENY 작업을 인식합니다. 보안 모델에는 다음과 같은 추가 특징이 있습니다.  
  
-   보안 권한은 테이블에 있는 다른 모든 열과 유사하게 열 집합 열에서 부여되고 취소될 수 있습니다.  
  
-   열 집합 열에 대한 SELECT, INSERT, UPDATE, DELETE 및 REFERENCES 권한의 GRANT 또는 REVOKE가 해당 집합의 기본 멤버 열로 전파되지 않습니다. 이는 열 집합 열을 사용하는 경우에만 적용됩니다. 열 집합에 대한 DENY 권한은 테이블의 기본 스파스 열로 전파되지 않습니다.  
  
-   열 집합 열에 대해 SELECT, INSERT, UPDATE 및 DELETE 문을 실행하려면 사용자가 열 집합 열에 해당하는 권한은 물론 테이블의 모든 스파스 열에 해당하는 권한을 가지고 있어야 합니다. 열 집합은 테이블의 모든 스파스 열을 나타내므로 사용자가 변경하지 않으려는 스파스 열을 포함한 모든 스파스 열에 대한 권한을 가지고 있어야 합니다.  
  
-   스파스 열 또는 열 집합에 대해 REVOKE 문을 실행하면 보안이 기본값인 해당 부모 개체의 보안으로 되돌려집니다.  
  
## <a name="examples"></a>예  
 다음 예의 Document 테이블에는 `DocID` 및 `Title`열의 공통 집합이 포함되어 있습니다. Production 그룹은 모든 생산 문서에 대한 `ProductionSpecification` 및 `ProductionLocation` 열을 원하며, Marketing 그룹은 마케팅 문서에 대한 `MarketingSurveyGroup` 열을 원합니다.  
  
### <a name="a-creating-a-table-that-has-a-column-set"></a>1. 열 집합을 포함하는 테이블 만들기  
 다음 예에서는 스파스 열을 사용하고 열 집합 `SpecialPurposeColumns`를 포함하는 테이블을 만듭니다. 이 예에서는 테이블에 두 개의 행을 삽입한 다음 테이블에서 데이터를 선택합니다.  
  
> [!NOTE]  
>  이 테이블에는 테이블을 보다 잘 표시하고 읽을 수 있도록 열이 5개만 있습니다.  
  
```  
USE AdventureWorks2012;  
GO  
  
CREATE TABLE DocumentStoreWithColumnSet  
    (DocID int PRIMARY KEY,  
     Title varchar(200) NOT NULL,  
     ProductionSpecification varchar(20) SPARSE NULL,  
     ProductionLocation smallint SPARSE NULL,  
     MarketingSurveyGroup varchar(20) SPARSE NULL,  
     MarketingProgramID int SPARSE NULL,  
     SpecialPurposeColumns XML COLUMN_SET FOR ALL_SPARSE_COLUMNS);  
GO  
```  
  
### <a name="b-inserting-data-to-a-table-by-using-the-names-of-the-sparse-columns"></a>2. 스파스 열 이름을 사용하여 테이블에 데이터 삽입  
 다음 예에서는 예 1에서 만든 테이블에 두 개의 행을 삽입합니다. 이 예에서는 스파스 열 이름을 사용하고 열 집합을 참조하지 않습니다.  
  
```  
INSERT DocumentStoreWithColumnSet (DocID, Title, ProductionSpecification, ProductionLocation)  
VALUES (1, 'Tire Spec 1', 'AXZZ217', 27);  
GO  
  
INSERT DocumentStoreWithColumnSet (DocID, Title, MarketingSurveyGroup)  
VALUES (2, 'Survey 2142', 'Men 25 - 35');  
GO  
```  
  
### <a name="c-inserting-data-to-a-table-by-using-the-name-of-the-column-set"></a>3. 열 집합 이름을 사용하여 테이블에 데이터 삽입  
 다음 예에서는 예 1에서 만든 테이블에 세 번째 행을 삽입합니다. 이 예에서는 스파스 열 이름이 사용되지 않습니다. 대신 열 집합 이름이 사용되고 삽입 작업으로 인해 XML 형식의 스파스 열 4개 중 2개에 대한 값이 제공됩니다.  
  
```  
INSERT DocumentStoreWithColumnSet (DocID, Title, SpecialPurposeColumns)  
VALUES (3, 'Tire Spec 2', '<ProductionSpecification>AXW9R411</ProductionSpecification><ProductionLocation>38</ProductionLocation>');  
GO  
```  
  
### <a name="d-observing-the-results-of-a-column-set-when-select--is-used"></a>4. SELECT *가 사용되는 경우의 열 집합 결과 관찰  
 다음 예에서는 열 집합을 포함하는 테이블의 모든 열을 선택합니다. 이 예에서는 스파스 열의 조합 값과 함께 XML 열을 반환하며 스파스 열을 개별적으로 반환하지 않습니다.  
  
```  
SELECT DocID, Title, SpecialPurposeColumns FROM DocumentStoreWithColumnSet ;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `DocID Title        SpecialPurposeColumns`  
  
 `1      Tire Spec 1  <ProductionSpecification>AXZZ217</ProductionSpecification><ProductionLocation>27</ProductionLocation>`  
  
 `2      Survey 2142  <MarketingSurveyGroup>Men 25 - 35</MarketingSurveyGroup>`  
  
 `3      Tire Spec 2  <ProductionSpecification>AXW9R411</ProductionSpecification><ProductionLocation>38</ProductionLocation>`  
  
### <a name="e-observing-the-results-of-selecting-the-column-set-by-name"></a>5. 이름별로 열 집합을 선택한 결과 관찰  
 Production 부서는 마케팅 데이터에 관심이 없으므로 이 예에서는 `WHERE` 절을 추가하여 출력을 제한합니다. 이 예에서는 열 집합 이름을 사용합니다.  
  
```  
SELECT DocID, Title, SpecialPurposeColumns  
FROM DocumentStoreWithColumnSet  
WHERE ProductionSpecification IS NOT NULL ;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `DocID Title        SpecialPurposeColumns`  
  
 `1     Tire Spec 1  <ProductionSpecification>AXZZ217</ProductionSpecification><ProductionLocation>27</ProductionLocation>`  
  
 `3     Tire Spec 2  <ProductionSpecification>AXW9R411</ProductionSpecification><ProductionLocation>38</ProductionLocation>`  
  
### <a name="f-observing-the-results-of-selecting-sparse-columns-by-name"></a>6. 이름별로 스파스 열을 선택한 결과 관찰  
 테이블에 열 집합이 포함되어 있으면 다음 예에서처럼 개별 열 이름을 사용하여 테이블을 쿼리할 수 있습니다.  
  
```  
SELECT DocID, Title, ProductionSpecification, ProductionLocation   
FROM DocumentStoreWithColumnSet  
WHERE ProductionSpecification IS NOT NULL ;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `DocID Title        ProductionSpecification ProductionLocation`  
  
 `1     Tire Spec 1  AXZZ217                 27`  
  
 `3     Tire Spec 2  AXW9R411                38`  
  
### <a name="g-updating-a-table-by-using-a-column-set"></a>7. 열 집합을 사용하여 테이블 업데이트  
 다음 예에서는 해당 행에서 사용하는 스파스 열 모두에 대해 세 번째 레코드를 새 값으로 업데이트합니다.  
  
```  
UPDATE DocumentStoreWithColumnSet  
SET SpecialPurposeColumns = '<ProductionSpecification>ZZ285W</ProductionSpecification><ProductionLocation>38</ProductionLocation>'  
WHERE DocID = 3 ;  
GO  
```  
  
> [!IMPORTANT]  
>  열 집합을 사용하는 UPDATE 문은 테이블의 모든 스파스 열을 업데이트합니다. 참조되지 않는 스파스 열은 NULL로 업데이트됩니다.  
  
 다음 예에서는 세 번째 레코드를 업데이트하지만 채워진 두 열 중 하나의 값만 지정합니다. 세 번째 열 `ProductionLocation` 은 `UPDATE` 문에 포함되지 않으며 NULL로 업데이트됩니다.  
  
```  
UPDATE DocumentStoreWithColumnSet  
SET SpecialPurposeColumns = '<ProductionSpecification>ZZ285W</ProductionSpecification>'  
WHERE DocID = 3 ;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [스파스 열 사용](../../relational-databases/tables/use-sparse-columns.md)  
  
  

