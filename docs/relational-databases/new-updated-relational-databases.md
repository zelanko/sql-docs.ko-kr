---
title: "업데이트됨 - 관계형 데이터베이스 문서 | Microsoft Docs"
description: "관계형 데이터베이스 설명서에서 최근에 변경된 업데이트된 콘텐츠의 일부를 표시합니다."
services: na
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: BYHAM
ms.service: na
ms.topic: updart-autogen
ms.technology: database-engine
ms.custom: UpdArt.exe
ms.workload: relational-databases
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 09/27/2017
ms.author: genemi
ms.openlocfilehash: 70cb071dc7b6f4ff15c5c7dee3f24bb352d6eb61
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="new-and-recently-updated-relational-databases-docs"></a>새로 추가되었거나 최근에 업데이트됨: 관계형 데이터베이스 문서



Microsoft에서는 거의 매일 [Docs.Microsoft.com](http://docs.microsoft.com/) 설명서 웹 사이트에서 기존 문서 일부를 업데이트합니다. 이 문서에는 최근 업데이트된 문서에서 발췌한 내용이 표시됩니다. 새 문서로 연결되는 링크도 나열될 수 있습니다.

이 문서는 주기적으로 다시 실행되는 프로그램에 의해 생성됩니다. 경우에 따라 발췌한 내용의 형식이 완전하지 않거나 원본 문서의 표식(markdown)으로 표시될 수 있습니다. 이미지는 여기에 표시되지 않습니다.

다음 날짜 범위 및 주제에 대한 최근 업데이트가 보고됩니다.



- *업데이트 날짜 범위:*  &nbsp; **2017-09-11** &nbsp; 부터 &nbsp; **2017-09-27**
- *주제 영역:* &nbsp; **관계형 데이터베이스**




&nbsp;

## <a name="new-articles-created-recently"></a>최근에 만든 새로운 문서

다음 링크는 최근에 추가된 새로운 문서로 이동합니다.


1. [SQL Server 및 Azure SQL Database에서 데이터 가져오기 및 내보내기](import-export/overview-import-export.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>업데이트된 문서의 발췌 내용

이 섹션에는 최근에 많이 업데이트된 문서에서 발췌한 업데이트 내용이 표시됩니다.

여기에 표시된 발췌 내용은 적절한 의미 체계 맥락과 분리되어 표시됩니다. 또한 발췌 내용은 때때로 실제 문서에서 이 내용의 주변에 있는 중요한 markdown 구문과도 분리되어 표시됩니다. 따라서 이러한 발췌 내용은 일반적인 지침을 제공하기 위한 것입니다. 이 발췌 내용에서는 관심 내용을 클릭하여 실제 문서를 참조할 가치가 있을지 여부만 파악할 수 있습니다.

따라서 이러한 발췌 내용에서 코드를 복사하거나 발췌 내용을 정확한 사실로 간주하지 마세요. 대신 실제 문서를 참조하세요.





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>최근 업데이트된 문서의 간결한 목록

이 간결한 목록에는 발췌 섹션에 나열된 모든 업데이트된 문서로 연결되는 링크가 있습니다.

1. [공간 데이터 형식 개요](#TitleNum_1)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-spatial-data-types-overviewspatialspatial-data-types-overviewmd"></a>1. &nbsp; [공간 데이터 형식 개요](spatial/spatial-data-types-overview.md)

*업데이트됨: 2017-09-26* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; 

<!-- Source markdown line 27.  ms.author= "rickbyh".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 96dd44cf49e96d1d543a629d49de297dba9c1753 2e9629f852ea42a213c7c24831bcfa53e40358f2  (PR=0  ,  Filename=spatial-data-types-overview.md  ,  Dirpath=docs\relational-databases\spatial\  ,  MergeCommitSha40=b33976cf92f23fbb13cee0c353fd40608d002d94) -->



 -  공간 데이터 형식은 두 가지가 있습니다. **geometry** 데이터 형식은 평면, 즉 유클리드(평평한 표면) 데이터를 지원합니다. **geometry** 데이터 형식은 OGC(Open Geospatial Consortium)의 Simple Features for SQL Specification 버전 1.1.0을 따르며 SQL MM(ISO 표준) 규격을 준수합니다.
 -
 - 또한 ..!NCLUDE-NotShown--ssNoVersion--../../includes/ssnoversion-md.md)]에서는 GPS 위도 및 경도 좌표 등의 타원(둥근 표면) 데이터를 저장하는 **geography** 데이터 형식을 지원합니다.
 -
 -> [!IMPORTANT]
 -> 향상된 공간 데이터 형식을 비롯한 ..!NCLUDE-NotShown--ssSQL11--../../includes/sssql11-md.md)]에서 소개된 공간 기능에 대한 자세한 설명 및 예제를 보려면 [SQL Server 코드 이름 "Denali"의 새로운 공간 기능](http://go.microsoft.com/fwlink/?LinkId=226407) 백서를 다운로드하세요.
 -
 -##  <a name="objects"></a> 공간 데이터 개체
 - **geometry** 및 **geography** 데이터 형식은 16개의 공간 데이터 개체 또는 인스턴스 유형을 지원합니다. 그러나 이러한 인스턴스 유형 중 11개만 *인스턴스화할 수 있고*데이터베이스에서 이러한 인스턴스를 만들고 작업(인스턴스화)할 수 있습니다. 이러한 인스턴스는 **Points**에서 이들을 **LineStrings, CircularStrings**, **CompoundCurves**, **Polygons**, **CurvePolygons** , **geometry** 로 구분하거나 여러 **geography** 또는 **GeometryCollection**인스턴스로 구분하는 부모 데이터 형식에서 특정 속성을 파생시킵니다. **Geography** 형식에는 **FullGlobe**라는 추가 인스턴스 유형이 있습니다.
 -
 - 아래 그림에서는 **geometry** 및 **geometry** 데이터 형식의 기반인 **geography** 계층을 보여 줍니다. **geometry** 및 **geography** 의 인스턴스화할 수 있는 형식은 파란색으로 표시되어 있습니다.
 -
 - ![geom_hierarchy--../../relational-databases/spatial/media/geom-hierarchy.gif)
 -
 - 그림에 표시된 대로 **geometry** 및 **geography** 데이터 형식 중 인스턴스화할 수 있는 10개의 형식은 **Point**, **MultiPoint**, **LineString**, **CircularString**, **MultiLineString**, **CompoundCurve**, **Polygon**, **CurvePolygon**, **MultiPolygon**및 **GeometryCollection**입니다. geography 데이터 형식의 경우 인스턴스화할 수 있는 추가 형식이 하나( **FullGlobe**) 있습니다. **geometry** 및 **geography** 형식은 인스턴스가 명시적으로 정의되어 있지 않더라도 형식이 올바르다면 특정 인스턴스를 인식할 수 있습니다. 예를 들어 STPointFromText() 메서드를 사용하여 **Point** 인스턴스를 명시적으로 정의할 경우, 올바른 형식의 메서드 입력에 한해 **geometry** 및 **geography** 는 해당 인스턴스를 **Point**로 인식합니다. `STGeomFromText()` 메서드를 사용하여 동일한 인스턴스를 정의할 경우 **geometry** 및 **geography** 데이터 형식은 해당 인스턴스를 **Point**로 인식합니다.







## <a name="similar-articles"></a>유사한 문서

<!--  HOW TO:
    Refresh this file's line items with the latest 'Count-in-Similars*' content.
    Then run Run-533-*.BAT
-->

이 섹션에는 공용 GitHub.com 리포지토리 내의 다른 주제 영역에서 최근에 업데이트된 문서와 유사한 문서가 나와 있습니다. [MicrosoftDocs/sql-docs](https://github.com/MicrosoftDocs/sql-docs/)

#### <a name="subject-areas-which-do-have-new-or-recently-updated-articles"></a>새로 추가되었거나 최근에 업데이트된 문서가 있는 주제 영역

- [새로 추가되었거나 업데이트됨(0+1): **SQL용 고급 분석** 문서](../advanced-analytics/new-updated-advanced-analytics.md)
- [새로 추가되었거나 업데이트됨(0+1): **SQL용 Analysis Services** 문서](../analysis-services/new-updated-analysis-services.md)
- [새로 추가되었거나 업데이트됨(4+1): **SQL용 데이터베이스 엔진** 문서](../database-engine/new-updated-database-engine.md)
- [새로 추가되었거나 업데이트됨(17+0): **SQL용 Integration Services** 문서](../integration-services/new-updated-integration-services.md)
- [새로 추가되었거나 업데이트됨(3+0): **SQL용 Linux** 문서](../linux/new-updated-linux.md)
- [새로 추가되었거나 업데이트됨(1+1): **SQL용 관계형 데이터베이스** 문서](../relational-databases/new-updated-relational-databases.md)
- [새로 추가되었거나 업데이트됨(2+0): **SQL용 Reporting Services** 문서](../reporting-services/new-updated-reporting-services.md)
- [새로 추가되었거나 업데이트됨(0+1): **SSMS(SQL Server Management Studio)** 문서](../ssms/new-updated-ssms.md)
- [새로 추가되었거나 업데이트됨(0+1): **Transact-SQL** 문서](../t-sql/new-updated-t-sql.md)

#### <a name="subject-areas-which-have-no-new-or-recently-updated-articles"></a>새로 추가되었거나 최근에 업데이트된 문서가 없는 주제 영역

- [새로 추가되었거나 업데이트됨(0+0): **SQL용 ADO(ActiveX Data Objects)** 문서](../ado/new-updated-ado.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL에 연결** 문서](../connect/new-updated-connect.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 Data Quality Services** 문서](../data-quality-services/new-updated-data-quality-services.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 DMX(Data Mining Extension)** 문서](../dmx/new-updated-dmx.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 MDS(Master Data Services)** 문서](../master-data-services/new-updated-master-data-services.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 MDX(Multidimensional Expression)** 문서](../mdx/new-updated-mdx.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 ODBC(Open Database Connectivity)** 문서](../odbc/new-updated-odbc.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 PowerShell** 문서](../powershell/new-updated-powershell.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 샘플** 문서](../sample/new-updated-sample.md)
- [새로 추가되었거나 업데이트됨(0+0): **Microsoft SQL Server** 문서](../sql-server/new-updated-sql-server.md)
- [새로 추가되었거나 업데이트됨(0+0): **SSDT(SQL Server Data Tools)** 문서](../ssdt/new-updated-ssdt.md)
- [새로 추가되었거나 업데이트됨(0+0): **SSMA(SQL Server Migration Assistant)** 문서](../ssma/new-updated-ssma.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 도구** 문서](../tools/new-updated-tools.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 XQuery** 문서](../xquery/new-updated-xquery.md)


