---
title: "업데이트됨 - SQL Server용 SSDT 문서 | Microsoft Docs"
description: "Microsoft SQL Server용 SSDT(SQL Server Data Tools) 설명서에서 최근에 변경된 내용에 대해 업데이트된 콘텐츠의 코드 조각을 표시합니다."
manager: craigg
author: MightyPen
ms.author: genemi
ms.topic: article
ms.custom: UpdArt.exe
ms.suite: sql
ms.prod_service: sql-non-specified
ms.component: ssdt
ms.date: 02/03/2018
ms.openlocfilehash: c591ddddd60af31fe2d338fdee25ea2c17ab0ea5
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/09/2018
---
# <a name="new-and-recently-updated-sql-server-data-tools-ssdt"></a>새로 추가되었거나 최근에 업데이트됨: SSDT(SQL Server Data Tools)



Microsoft에서는 거의 매일 [Docs.Microsoft.com](http://docs.microsoft.com/) 설명서 웹 사이트에서 기존 문서 일부를 업데이트합니다. 이 문서에는 최근 업데이트된 문서에서 발췌한 내용이 표시됩니다. 새 문서로 연결되는 링크도 나열될 수 있습니다.

이 문서는 주기적으로 다시 실행되는 프로그램에 의해 생성됩니다. 경우에 따라 발췌한 내용의 형식이 완전하지 않거나 원본 문서의 표식(markdown)으로 표시될 수 있습니다. 이미지는 여기에 표시되지 않습니다.

다음 날짜 범위 및 주제에 대한 최근 업데이트가 보고됩니다.



- *업데이트 날짜 범위:*  &nbsp; **2017-12-03** &nbsp;부터 &nbsp; **2018-02-03**까지
- *주제 영역:* &nbsp; **SSDT(SQL Server Data Tools)**.




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

1. [SSDT(SQL Server Data Tools)에 대한 변경 로그](#TitleNum_1)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-changelog-for-sql-server-data-tools-ssdtchangelog-for-sql-server-data-tools-ssdtmd"></a>1. &nbsp; [SSDT(SQL Server Data Tools)에 대한 변경 로그](changelog-for-sql-server-data-tools-ssdt.md)

*업데이트됨: 2018-01-18* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; 

<!-- Source markdown line 28.  ms.author= "sstein".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 6416949beaee91da2f77dfebb9eb5ed363db4cb7 de18314845cffa197b3fd2ed868f2c330760bedb  (PR=4652  ,  Filename=changelog-for-sql-server-data-tools-ssdt.md  ,  Dirpath=docs\ssdt\  ,  MergeCommitSha40=6b4aae3706247ce9b311682774b13ac067f60a79) -->



**Visual Studio 2017용 SSDT(15.5.1)**

빌드 번호: 14.0.16148.0

**새로운 기능**


Visual Studio 2017(15.5.1)은 설치 관리자에 대한 다음과 같은 버그 수정을 제외하고 15.5.0 버전과 동일한 릴리스입니다.

1.  SQL Server Integration Services 사후 설치 시 설치 관리자가 응답하지 않는 문제를 수정했습니다.
2.  "요청된 메타 파일 작업이 지원되지 않습니다(0x800707D3)" 오류 메시지와 함께 설치가 실패하는 문제를 수정했습니다.

이러한 두 가지 버그 수정 외에도 15.5.0에 대한 다음과 같은 세부 사항이 15.5.1에 적용됩니다.

**Visual Studio 2017용 SSDT(15.5.0)**

빌드 번호: 14.0.16146.0

**새로운 기능**


Visual Studio 2017용 SSDT(15.5.0)가 미리 보기에서 GA(일반 공급)로 전환됩니다.

**설치 관리자**
1. 설치 UI가 지역화됩니다.
1. 아이콘이 더 높은 품질 버전으로 바뀝니다.

**IS(Integration Services)**
1. ADF에서 Azure SSIS IR에 배포할 때 사용하는 배포 마법사에서, Azure SSIS IR에서 실행되는 SSIS 패키지의 잠재적 호환성 문제를 검색하는 패키지 유효성 검사 단계가 추가되었습니다. 자세한 내용은 [Azure에 배포된 SSIS 패키지 유효성 검사](..\integration-services\lift-shift\ssis-azure-validate-packages.md)를 참조하세요.
1. SSIS 확장이 지역화됩니다.

**버그 수정**


**IS(Integration Services)**
1. OLEDB 및 ADO.NET 연결 관리자의 레이아웃이 손상되는 문제를 수정했습니다.
2. 차원 처리 작업을 편집하려고 할 때 어셈블리를 찾을 수 없는 오류가 발생하는 문제를 수정했습니다.

**알려진 문제**


**IS(Integration Services)** SSIS 패키지 실행 태스크는 ExecuteOutOfProcess가 True로 설정되었을 때 디버깅을 지원하지 않습니다. 이 문제는 디버깅에만 적용됩니다. DTExec.exe 또는 SSIS 카탈로그를 통한 저장, 배포 및 실행은 영향을 받지 않습니다.



**Visual Studio 2015용 SSDT 17.4**

빌드 번호: 14.0.61712.050

**새로운 기능**


**AS(Analysis Services) 프로젝트**
- 테이블 형식 프로젝트에 세 개의 새로운 옵션이 추가되었습니다.(옵션 > Analysis Services 테이블 형식 > 데이터 가져오기).







## <a name="similar-articles-about-new-or-updated-articles"></a>신규 문서 또는 업데이트된 문서에 대한 유사 문서

이 섹션에는 공용 GitHub.com 리포지토리 내의 다른 주제 영역에서 최근에 업데이트된 문서와 유사한 문서가 나와 있습니다. [MicrosoftDocs/sql-docs](https://github.com/MicrosoftDocs/sql-docs/)


#### <a name="subject-areas-that-do-have-new-or-recently-updated-articles"></a>새로 추가되었거나 최근에 업데이트된 문서가 *있는* 주제 영역


- [새로 추가되었거나 업데이트됨(1+3):&nbsp; **SQL용 고급 분석** 문서](../advanced-analytics/new-updated-advanced-analytics.md)
- [새로 추가되었거나 업데이트됨(0+1):&nbsp; **SQL용 분석 플랫폼 시스템** 문서](../analytics-platform-system/new-updated-analytics-platform-system.md)
- [새로 추가되었거나 업데이트됨(0+1):&nbsp; **SQL에 연결** 문서](../connect/new-updated-connect.md)
- [새로 추가되었거나 업데이트됨(0+1):&nbsp; **SQL용 데이터베이스 엔진** 문서](../database-engine/new-updated-database-engine.md)
- [새로 추가되었거나 업데이트됨(12+1): **SQL용 Integration Services** 문서](../integration-services/new-updated-integration-services.md)
- [새로 추가되었거나 업데이트됨(6+2):&nbsp; **SQL용 Linux** 문서](../linux/new-updated-linux.md)
- [새로 추가되었거나 업데이트됨(15+0): **SQL용 PowerShell** 문서](../powershell/new-updated-powershell.md)
- [새로 추가되었거나 업데이트됨(2+9):&nbsp; **SQL용 관계형 데이터베이스** 문서](../relational-databases/new-updated-relational-databases.md)
- [새로 추가되었거나 업데이트됨(1+0):&nbsp; **SQL용 Reporting Services** 문서](../reporting-services/new-updated-reporting-services.md)
- [새로 추가되었거나 업데이트됨(1+1):&nbsp; **SQL 작업 Studio** 문서](../sql-operations-studio/new-updated-sql-operations-studio.md)
- [새로 추가되었거나 업데이트됨(1+1):&nbsp; **Microsoft SQL Server** 문서](../sql-server/new-updated-sql-server.md)
- [새로 추가되었거나 업데이트됨(0+1):&nbsp; **SSDT(SQL Server Data Tools)** 문서](../ssdt/new-updated-ssdt.md)
- [새로 추가되었거나 업데이트됨(1+2):&nbsp; **SSMS(SQL Server Management Studio)** 문서](../ssms/new-updated-ssms.md)
- [새로 추가되었거나 업데이트됨(0+2):&nbsp; **Transact-SQL** 문서](../t-sql/new-updated-t-sql.md)



#### <a name="subject-areas-that-do-not-have-any-new-or-recently-updated-articles"></a>새로 추가되었거나 최근에 업데이트된 문서가 *없는* 주제 영역


- [새로 추가되었거나 업데이트됨(0+0): **SQL용 DMA(Data Migration Assistant)** 문서](../dma/new-updated-dma.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 ADO(ActiveX Data Objects)** 문서](../ado/new-updated-ado.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 Analysis Services** 문서](../analysis-services/new-updated-analysis-services.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 Data Quality Services** 문서](../data-quality-services/new-updated-data-quality-services.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 DMX(Data Mining Extension)** 문서](../dmx/new-updated-dmx.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 MDS(Master Data Services)** 문서](../master-data-services/new-updated-master-data-services.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 MDX(Multidimensional Expression)** 문서](../mdx/new-updated-mdx.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 ODBC(Open Database Connectivity)** 문서](../odbc/new-updated-odbc.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 샘플** 문서](../sample/new-updated-sample.md)
- [새로 추가되었거나 업데이트됨(0+0): **SSMA(SQL Server Migration Assistant)** 문서](../ssma/new-updated-ssma.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 도구** 문서](../tools/new-updated-tools.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 XQuery** 문서](../xquery/new-updated-xquery.md)


