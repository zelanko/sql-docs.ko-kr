---
title: "SQL Server 문서에 대 한 Analysis Services-업데이트 | Microsoft Docs"
description: "코드 조각에 최근에 변경 된 설명서, Microsoft SQL server Analysis Services에 대 한 업데이트 된 콘텐츠를 표시 합니다."
services: na
documentationcenter: 
author: MightyPen
manager: kfile
editor: 
ms.service: na
ms.topic: updart-autogen
ms.technology: database-engine
ms.custom: UpdArt.exe
ms.workload: analysis-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 09/27/2017
ms.author: genemi
ms.translationtype: MT
ms.sourcegitcommit: 834bba08c90262fd72881ab2890abaaf7b8f7678
ms.openlocfilehash: a21f82dd5a0bd4ef59abc639d9441be25191a21b
ms.contentlocale: ko-kr
ms.lasthandoff: 10/02/2017

---
# <a name="new-and-recently-updated-analysis-services-for-sql-server"></a>새로 추가 되거나 최근에 업데이트 된: SQL server Analysis Services



Microsoft에서는 거의 매일 [Docs.Microsoft.com](http://docs.microsoft.com/) 설명서 웹 사이트에서 기존 문서 일부를 업데이트합니다. 이 문서에는 최근 업데이트된 문서에서 발췌한 내용이 표시됩니다. 새 문서로 연결되는 링크도 나열될 수 있습니다.

이 문서는 주기적으로 다시 실행되는 프로그램에 의해 생성됩니다. 경우에 따라 발췌한 내용의 형식이 완전하지 않거나 원본 문서의 표식(markdown)으로 표시될 수 있습니다. 이미지는 여기에 표시되지 않습니다.

다음 날짜 범위 및 주제에 대한 최근 업데이트가 보고됩니다.



- *날짜 범위 업데이트:* &nbsp; **2017-09-11** &nbsp; 을 아래와 같이 &nbsp; **2017-09-27**
- *주제 영역:* &nbsp; **for SQL Server Analysis Services**합니다.




&nbsp;

## <a name="new-articles-created-recently"></a>최근에 만든 새로운 문서

다음 링크는 최근에 추가된 새로운 문서로 이동합니다.


***지금은 나열할 새 문서가 없습니다.***



&nbsp;

## <a name="updated-articles-with-excerpts"></a>업데이트된 문서의 발췌 내용

이 섹션에는 최근에 많이 업데이트된 문서에서 발췌한 업데이트 내용이 표시됩니다.

여기에 표시된 발췌 내용은 적절한 의미 체계 맥락과 분리되어 표시됩니다. 또한 발췌 내용은 때때로 실제 문서에서 이 내용의 주변에 있는 중요한 markdown 구문과도 분리되어 표시됩니다. 따라서 이러한 발췌 내용은 일반적인 지침을 제공하기 위한 것입니다. 이 발췌 내용에서는 관심 내용을 클릭하여 실제 문서를 참조할 가치가 있을지 여부만 파악할 수 있습니다.

따라서 이러한 발췌 내용에서 코드를 복사하거나 발췌 내용을 정확한 사실로 간주하지 마세요. 대신 실제 문서를 참조하세요.





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>최근 업데이트된 문서의 간결한 목록

이 간결한 목록에는 발췌 섹션에 나열된 모든 업데이트된 문서로 연결되는 링크가 있습니다.

1. [기능 &#39; s SQL Server 2017 Analysis Services의 새로운 기능](#TitleNum_1)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-what39s-new-in-sql-server-2017-analysis-serviceswhat-s-new-in-sql-server-analysis-services-2017md"></a>1. &nbsp;[기능 &#39; s SQL Server 2017 Analysis Services의 새로운 기능](what-s-new-in-sql-server-analysis-services-2017.md)

*업데이트 됨된: 2017-09-22* &nbsp; &nbsp; &nbsp; &nbsp;&nbsp; 

<!-- Source markdown line 143.  ms.author= "owend".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 c8d75883f07e6e32859728d09139920eb9bf65c5 d206e83413d15a6e6116120e4a98dda9c8ce81d8  (PR=3278  ,  Filename=what-s-new-in-sql-server-analysis-services-2017.md  ,  Dirpath=docs\analysis-services\  ,  MergeCommitSha40=656e62f36446db4ef5b232129130a0253d2aebdf) -->



**개체 수준 보안**

이 릴리스에서 소개 [개체 수준 보안을... / analysis-services/tabular-models/object-level-security.md) 테이블 및 열에 대 한 합니다. 테이블 및 열 데이터를 액세스를 제한 하는 것 외에도 중요 한 테이블 및 열 이름은 강화할 수 있습니다. 이렇게 하면 악의적인 사용자가 해당 테이블이 있는지 검색할 수 없습니다.

JSON 기반 메타 데이터, TMSL Tabular Model Scripting Language (), 또는 테이블 형식 개체 모델 (TOM)를 사용 하 여 개체 수준 보안을 설정 해야 합니다.

예를 들어 다음 코드는 **TablePermission** 클래스의 **MetadataPermission** 속성을 **None**으로 설정하여 샘플 Adventure Works 테이블 형식 모델의 Product 테이블을 보호하는 데 도움이 됩니다.

```
//Find the Users role in Adventure Works and secure the Product table
ModelRole role = db.Model.Roles.Find("Users");
Table productTable = db.Model.Tables.Find("Product");
if (role != null && productTable != null)
{
    TablePermission tablePermission;
    if (role.TablePermissions.Contains(productTable.Name))
    {
        tablePermission = role.TablePermissions[productTable.Name];
    }
    else
    {
        tablePermission = new TablePermission();
        role.TablePermissions.Add(tablePermission);
        tablePermission.Table = productTable;
    }
    tablePermission.MetadataPermission = MetadataPermission.None;
}
db.Update(UpdateOptions.ExpandFull);
```

**동적 관리 뷰 (Dmv)**

[Dmv... / analysis-services/instances/use-dynamic-management-views-dmvs-to-monitor-analysis-services.md) 로컬 서버 작업 및 서버 상태에 대 한 정보를 반환 하는 SQL Server Profiler에서 쿼리 됩니다.
이 릴리스에 향상 된 기능이 [동적 관리 뷰](https://docs.microsoft.com/sql/analysis-services/instances/use-dynamic-management-views-dmvs-to-monitor-analysis-services) (DMV) 1400 하 고 1200 호환성 수준의 테이블 형식 모델에 대 한 합니다.







## <a name="similar-articles"></a>유사한 문서

<!--  HOW TO:
    Refresh this file's line items with the latest 'Count-in-Similars*' content.
    Then run Run-533-*.BAT
-->

이 섹션에는 공용 GitHub.com 리포지토리 내의 다른 주제 영역에서 최근에 업데이트된 문서와 유사한 문서가 나와 있습니다. [MicrosoftDocs/sql-docs](https://github.com/MicrosoftDocs/sql-docs/)

#### <a name="subject-areas-which-do-have-new-or-recently-updated-articles"></a>새로 추가되었거나 최근에 업데이트된 문서가 있는 주제 영역

- [새 + 업데이트 (0 + 1): **SQL에 대 한 고급 분석** docs](../advanced-analytics/new-updated-advanced-analytics.md)
- [새 + 업데이트 (0 + 1): **SQL에 대 한 Analysis Services** docs](../analysis-services/new-updated-analysis-services.md)
- [새 + 업데이트 (4 + 1): **SQL에 대 한 데이터베이스 엔진** docs](../database-engine/new-updated-database-engine.md)
- [새 + 업데이트 (17 + 0): **sql Integration Services** docs](../integration-services/new-updated-integration-services.md)
- [새 + 업데이트 (3 + 0): **SQL에 대 한 Linux** docs](../linux/new-updated-linux.md)
- [새 + 업데이트 (1 + 1): **SQL에 대 한 관계형 데이터베이스** docs](../relational-databases/new-updated-relational-databases.md)
- [새 + 업데이트 (2 + 0): **sql Reporting Services** docs](../reporting-services/new-updated-reporting-services.md)
- [새 + 업데이트 (0 + 1): **SQL Server Management Studio (SSMS)** docs](../ssms/new-updated-ssms.md)
- [새 + 업데이트 (0 + 1): **TRANSACT-SQL** docs](../t-sql/new-updated-t-sql.md)

#### <a name="subject-areas-which-have-no-new-or-recently-updated-articles"></a>새로 추가되었거나 최근에 업데이트된 문서가 없는 주제 영역

- [새로 추가되었거나 업데이트됨(0+0): **SQL용 ADO(ActiveX Data Objects)** 문서](../ado/new-updated-ado.md)
- [새 + 업데이트 (0 + 0): **SQL에 연결** docs](../connect/new-updated-connect.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 Data Quality Services** 문서](../data-quality-services/new-updated-data-quality-services.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 DMX(Data Mining Extension)** 문서](../dmx/new-updated-dmx.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 MDS(Master Data Services)** 문서](../master-data-services/new-updated-master-data-services.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 MDX(Multidimensional Expression)** 문서](../mdx/new-updated-mdx.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 ODBC(Open Database Connectivity)** 문서](../odbc/new-updated-odbc.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 PowerShell** 문서](../powershell/new-updated-powershell.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 샘플** 문서](../sample/new-updated-sample.md)
- [새 + 업데이트 (0 + 0): **Microsoft SQL Server** docs](../sql-server/new-updated-sql-server.md)
- [새로 추가되었거나 업데이트됨(0+0): **SSDT(SQL Server Data Tools)** 문서](../ssdt/new-updated-ssdt.md)
- [새로 추가되었거나 업데이트됨(0+0): **SSMA(SQL Server Migration Assistant)** 문서](../ssma/new-updated-ssma.md)
- [새 + 업데이트 (0 + 0): **SQL에 대 한 도구** docs](../tools/new-updated-tools.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 XQuery** 문서](../xquery/new-updated-xquery.md)



