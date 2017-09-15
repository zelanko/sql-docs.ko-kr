---
title: "업데이트 됨-T-SQL docs | Microsoft Docs"
description: "가져온 조각을 TRANSACT-SQL에 대 한 최근에 변경 된 설명서에 대 한 업데이트 된 콘텐츠를 표시 합니다."
services: na
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: BYHAM
ms.service: na
ms.topic: updart-autogen
ms.technology: database-engine
ms.custom: UpdArt.exe
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 09/11/2017
ms.author: genemi
ms.workload: t-sql
ms.translationtype: MT
ms.sourcegitcommit: 15080827744c19120a8474f3142004c4af7a4064
ms.openlocfilehash: fa2ad3f4bc6071c54b9996a893ee584ba215100f
ms.contentlocale: ko-kr
ms.lasthandoff: 09/13/2017

---
# <a name="new-and-recently-updated-transact-sql-docs"></a>신규 / 최근에 업데이트: Transact SQL docs



Microsoft에서는 거의 매일 [Docs.Microsoft.com](http://docs.microsoft.com/) 설명서 웹 사이트에서 기존 문서 일부를 업데이트합니다. 이 문서에는 최근 업데이트된 문서에서 발췌한 내용이 표시됩니다. 새 문서로 연결되는 링크도 나열될 수 있습니다.

이 문서는 주기적으로 다시 실행되는 프로그램에 의해 생성됩니다. 경우에 따라 발췌한 내용의 형식이 완전하지 않거나 원본 문서의 표식(markdown)으로 표시될 수 있습니다. 이미지는 여기에 표시되지 않습니다.

다음 날짜 범위 및 주제에 대한 최근 업데이트가 보고됩니다.



- *날짜 범위 업데이트:* &nbsp; **2017-07-18** &nbsp; 을 아래와 같이 &nbsp; **2017-09-11**
- *주제 영역:* &nbsp; **T-SQL**합니다.




&nbsp;

## <a name="new-articles-created-recently"></a>최근에 만든 새로운 문서

다음 링크는 최근에 추가 된 새 문서를 이동 합니다.


1. [예측 (Transact SQL)](queries/predict-transact-sql.md)
2. [ALTER 외부 라이브러리 (Transact SQL)](statements/alter-external-library-transact-sql.md)
3. [외부 라이브러리 (Transact SQL) 만들기](statements/create-external-library-transact-sql.md)
4. [DROP 외부 라이브러리 (Transact SQL)](statements/drop-external-library-transact-sql.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>업데이트된 문서의 발췌 내용

이 섹션에는 최근에 대규모 업데이트 발견 된 문서에서 수집 하는 업데이트의 발췌 한 내용 표시 됩니다.

여기에 표시된 발췌 내용은 적절한 의미 체계 맥락과 분리되어 표시됩니다. 또한 발췌 내용은 때때로 실제 문서에서 이 내용의 주변에 있는 중요한 markdown 구문과도 분리되어 표시됩니다. 따라서 이러한 발췌 내용은 일반적인 지침을 제공하기 위한 것입니다. 이 발췌 내용에서는 관심 내용을 클릭하여 실제 문서를 참조할 가치가 있을지 여부만 파악할 수 있습니다.

따라서 이러한 발췌 내용에서 코드를 복사하거나 발췌 내용을 정확한 사실로 간주하지 마세요. 대신 실제 문서를 참조하세요.





&nbsp;

<a name="compactupdatedlist"/>

## <a name="compact-list-of-articles-updated-recently"></a>최근 업데이트된 문서의 간결한 목록

이 compact 목록 발췌 한 내용 섹션에 나열 된 모든 업데이트 된 문서에 대 한 링크를 제공 합니다.

1. [CAST 및 CONVERT (Transact SQL)](#TitleNum_1)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-cast-and-convert-transact-sqlfunctionscast-and-convert-transact-sqlmd"></a>1. &nbsp;[CAST 및 CONVERT (Transact SQL)](functions/cast-and-convert-transact-sql.md)

*업데이트 됨된: 2017-09-08* &nbsp; &nbsp; &nbsp; &nbsp;&nbsp; 

<!-- Source markdown line 647.  ms.author= "rickbyh".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 b805ecddecda72ffc026c3866b5284a79b69fb3f f2906eaf87c7cdf1409922d4efba8cd1c5635674  (PR=0  ,  Filename=cast-and-convert-transact-sql.md  ,  Dirpath=docs\t-sql\functions\  ,  MergeCommitSha40=b97cc9723d563b19c85661f5ad7049a96fc904ff) -->



**11. 산술 연산자와 CAST 사용**

다음 예제에서는 제품 단가 분할 하 여 단일 열 계산을 계산 (`UnitPrice`)는 할인 백분율 (`UnitPriceDiscountPct`). 이 결과는 가장 근사한 정수로 반올림된 후 `int` 데이터 형식으로 변환됩니다. AdventureWorksDW를 사용합니다.

```
SELECT ProductKey, UnitPrice,UnitPriceDiscountPct,
       CAST(ROUND (UnitPrice*UnitPriceDiscountPct,0) AS int) AS DiscountPrice
FROM dbo.FactResellerSales
WHERE SalesOrderNumber = 'SO47355'
      AND UnitPriceDiscountPct > .02;
```

..! 포함 NotShown-ssResult... /.. /includes/ssresult-md.md)]

```
ProductKey  UnitPrice  UnitPriceDiscountPct  DiscountPrice
----------  ---------  --------------------  -------------
323         430.6445   0.05                  22
213         18.5043    0.05                  1
456         37.4950    0.10                  4
456         37.4950    0.10                  4
216         18.5043    0.05                  1
```

**범위로 정의 됩니다. CAST를 사용 하 여 연결 하려면**

다음 예에서는 캐스팅을 사용 하 여 문자가 아닌 식을 연결 합니다. AdventureWorksDW를 사용합니다.

```
SELECT 'The list price is ' + CAST(ListPrice AS varchar(12)) AS ListPrice
FROM dbo.DimProduct
WHERE ListPrice BETWEEN 350.00 AND 400.00;
```

..! 포함 NotShown-ssResult... /.. /includes/ssresult-md.md)]

```
ListPrice
------------------------
The list price is 357.06
The list price is 364.09
The list price is 364.09
The list price is 364.09
The list price is 364.09
```

**M입니다. CAST를 사용 하 여 읽기 쉬운 텍스트 만들기**

다음 예제에서는 SELECT 목록에서 변환 하려면 CAST가 사용 된 `Name` 열을 한 **char (10)** 열. AdventureWorksDW를 사용합니다.

```
SELECT DISTINCT CAST(EnglishProductName AS char(10)) AS Name, ListPrice
FROM dbo.DimProduct
WHERE EnglishProductName LIKE 'Long-Sleeve Logo Jersey, M';
```

..! 포함 NotShown-ssResult... /.. /includes/ssresult-md.md)]







## <a name="similar-articles"></a>유사한 문서

<!--  HOW TO:
    Refresh this file's line items with the latest 'Count-in-Similars*' content.
    Then run Run-533-*.BAT
-->

이 섹션에서는 공용 GitHub.com 리포지토리 내에서 다른 주제 영역에서 최근에 업데이트 된 아티클에 대 한 매우 유사한 문서: [MicrosoftDocs/sql-docs](https://github.com/MicrosoftDocs/sql-docs/)합니다.

#### <a name="subject-areas-which-do-have-new-or-recently-updated-articles"></a>새로 추가되었거나 최근에 업데이트된 문서가 있는 주제 영역

- [새 + 업데이트 (3 + 12): **SQL에 대 한 고급 분석** docs](../advanced-analytics/new-updated-advanced-analytics.md)
- [새 + 업데이트 (5 + 0): **SQL에 연결** docs](../connect/new-updated-connect.md)
- [새 + 업데이트 (5 + 1): **SQL에 대 한 데이터베이스 엔진** docs](../database-engine/new-updated-database-engine.md)
- [새 + 업데이트 (19 + 82): **sql Integration Services** docs](../integration-services/new-updated-integration-services.md)
- [새 + 업데이트 (1 + 8): **SQL에 대 한 Linux** docs](../linux/new-updated-linux.md)
- [새 + 업데이트 (12 + 1): **SQL에 대 한 관계형 데이터베이스** docs](../relational-databases/new-updated-relational-databases.md)
- [새 + 업데이트 (0 + 1): **sql Reporting Services** docs](../reporting-services/new-updated-reporting-services.md)
- [새 + 업데이트 (7 + 1): **Microsoft SQL Server** docs](../sql-server/new-updated-sql-server.md)
- [새 + 업데이트 (1 + 1): **SQL Server Data Tools (SSDT)** docs](../ssdt/new-updated-ssdt.md)
- [새 + 업데이트 (0 + 2): **SQL Server Migration Assistant (SSMA)** docs](../ssma/new-updated-ssma.md)
- [새 + 업데이트 (1 + 4): **SQL Server Management Studio (SSMS)** docs](../ssms/new-updated-ssms.md)
- [새 + 업데이트 (4 + 1): **TRANSACT-SQL** docs](../t-sql/new-updated-t-sql.md)
- [새 + 업데이트 (0 + 1): **SQL에 대 한 도구** docs](../tools/new-updated-tools.md)

#### <a name="subject-areas-which-have-no-new-or-recently-updated-articles"></a>새로 추가되었거나 최근에 업데이트된 문서가 없는 주제 영역

- [새로 추가되었거나 업데이트됨(0+0): **SQL용 ADO(ActiveX Data Objects)** 문서](../ado/new-updated-ado.md)
- [새 + 업데이트 (0 + 0): **SQL에 대 한 Analysis Services** docs](../analysis-services/new-updated-analysis-services.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 Data Quality Services** 문서](../data-quality-services/new-updated-data-quality-services.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 DMX(Data Mining Extension)** 문서](../dmx/new-updated-dmx.md)
- [새 + 업데이트 (0 + 0): **서비스 MDS (Master Data) sql** docs](../master-data-services/new-updated-master-data-services.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 MDX(Multidimensional Expression)** 문서](../mdx/new-updated-mdx.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 ODBC(Open Database Connectivity)** 문서](../odbc/new-updated-odbc.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 PowerShell** 문서](../powershell/new-updated-powershell.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 샘플** 문서](../sample/new-updated-sample.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 XQuery** 문서](../xquery/new-updated-xquery.md)



