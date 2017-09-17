---
title: "업데이트 됨-Reporting Services SQL Server 문서에 대 한 | Microsoft Docs"
description: "코드 조각에 최근에 변경 된 설명서, Microsoft SQL server Reporting Services에 대 한 업데이트 된 콘텐츠를 표시 합니다."
services: na
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: 
ms.service: na
ms.topic: updart-autogen
ms.technology: database-engine
ms.custom: UpdArt.exe
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 09/11/2017
ms.author: genemi
ms.workload: reporting-services
ms.translationtype: MT
ms.sourcegitcommit: 15080827744c19120a8474f3142004c4af7a4064
ms.openlocfilehash: 690b622224a31f4327b6dc199b1687f1726937c2
ms.contentlocale: ko-kr
ms.lasthandoff: 09/13/2017

---
# <a name="new-and-recently-updated-reporting-services-for-sql-server"></a>새로 추가 되거나 최근에 업데이트 된: SQL Server 용 Reporting Services



Microsoft에서는 거의 매일 [Docs.Microsoft.com](http://docs.microsoft.com/) 설명서 웹 사이트에서 기존 문서 일부를 업데이트합니다. 이 문서에는 최근 업데이트된 문서에서 발췌한 내용이 표시됩니다. 새 문서로 연결되는 링크도 나열될 수 있습니다.

이 문서는 주기적으로 다시 실행되는 프로그램에 의해 생성됩니다. 경우에 따라 발췌한 내용의 형식이 완전하지 않거나 원본 문서의 표식(markdown)으로 표시될 수 있습니다. 이미지는 여기에 표시되지 않습니다.

다음 날짜 범위 및 주제에 대한 최근 업데이트가 보고됩니다.



- *날짜 범위 업데이트:* &nbsp; **2017-07-18** &nbsp; 을 아래와 같이 &nbsp; **2017-09-11**
- *주제 영역:* &nbsp; **for SQL Server Reporting Services**합니다.




&nbsp;

## <a name="new-articles-created-recently"></a>최근에 만든 새로운 문서

다음 링크는 최근에 추가 된 새 문서를 이동 합니다.


***지금은 나열할 새 문서가 없습니다.***



&nbsp;

## <a name="updated-articles-with-excerpts"></a>업데이트된 문서의 발췌 내용

이 섹션에는 최근에 대규모 업데이트 발견 된 문서에서 수집 하는 업데이트의 발췌 한 내용 표시 됩니다.

여기에 표시된 발췌 내용은 적절한 의미 체계 맥락과 분리되어 표시됩니다. 또한 발췌 내용은 때때로 실제 문서에서 이 내용의 주변에 있는 중요한 markdown 구문과도 분리되어 표시됩니다. 따라서 이러한 발췌 내용은 일반적인 지침을 제공하기 위한 것입니다. 이 발췌 내용에서는 관심 내용을 클릭하여 실제 문서를 참조할 가치가 있을지 여부만 파악할 수 있습니다.

따라서 이러한 발췌 내용에서 코드를 복사하거나 발췌 내용을 정확한 사실로 간주하지 마세요. 대신 실제 문서를 참조하세요.





&nbsp;

<a name="compactupdatedlist"/>

## <a name="compact-list-of-articles-updated-recently"></a>최근 업데이트된 문서의 간결한 목록

이 compact 목록 발췌 한 내용 섹션에 나열 된 모든 업데이트 된 문서에 대 한 링크를 제공 합니다.

1. [서버 속성 (고급 페이지)-Reporting Services](#TitleNum_1)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-server-properties-advanced-page---reporting-servicestoolsserver-properties-advanced-page-reporting-servicesmd"></a>1. &nbsp;[서버 속성 (고급 페이지)-Reporting Services](tools/server-properties-advanced-page-reporting-services.md)

*업데이트 됨된: 2017-08-25* &nbsp; &nbsp; &nbsp; &nbsp;&nbsp; 

<!-- Source markdown line 122.  ms.author= "asaxton".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 92858a7e7239197af4ac2745ffc857d8c04f55cd e86bd4767f668b4ce80dc70056181d001f8e1b89  (PR=2953  ,  Filename=server-properties-advanced-page-reporting-services.md  ,  Dirpath=docs\reporting-services\tools\  ,  MergeCommitSha40=c003d58dd887ce1eddc142fa62f8050b73c0c935) -->



**AccessControlAllowCredentials** '자격 증명' 플래그가 설정 되 면 클라이언트 요청에 대 한 응답 노출 될 수 있는지 여부를 나타냅니다. true로 합니다. 기본값은 **false**입니다.

**AccessControlAllowHeaders** 클라이언트 요청을 하면 서버에서 허용 하는 헤더의 쉼표로 구분 된 목록입니다. 이 속성에는 빈 문자열일 수 지정 * 모든 헤더를 허용 합니다.

**AccessControlAllowMethods** 클라이언트 요청을 하면 서버에서 허용 하는 HTTP 메서드의 쉼표로 구분 된 목록입니다. 기본값은 (GET, PUT, POST, PATCH, DELETE)을 지정 하 * 모든 메서드를 허용 합니다.

**AccessControlAllowOrigin** 는 원본 서버에서 클라이언트 요청을 하면 허용 하는 쉼표로 구분 된 목록입니다. 기본값은 빈 지정 하는 모든 요청을 방지 하는 * 때 자격 증명이 설정 되지 않으면 모든 원본을 허용 됩니다 origin의 자세한 목록을 지정 해야 자격 증명을 지정 합니다.

**AccessControlExposeHeaders** 서버는 클라이언트에 노출 하는 헤더의 쉼표로 구분 된 목록입니다. 기본값은 공백입니다.

**AccessControlMaxAge** 실행 전 요청의 결과 캐시할 수 있습니다 (초)을 지정 합니다. 기본값은 600 (10 분).








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



