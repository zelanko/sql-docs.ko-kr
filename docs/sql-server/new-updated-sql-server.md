---
title: 업데이트됨 - SQL Server 문서 | Microsoft Docs
description: SQL Server의 설명서에서 최근에 변경된 업데이트된 콘텐츠의 일부를 표시합니다.
manager: craigg
author: MightyPen
ms.author: genemi
ms.topic: conceptual
ms.custom: UpdArt.exe
ms.suite: sql
ms.technology: release-landing
ms.prod: sql
ms.date: 04/28/2018
ms.openlocfilehash: 3575f65c751d91e2a32cf0acbf76665b42378d6a
ms.sourcegitcommit: c8f7e9f05043ac10af8a742153e81ab81aa6a3c3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/17/2018
ms.locfileid: "39084435"
---
# <a name="new-and-recently-updated-sql-server-docs"></a>새로 추가되었거나 최근에 업데이트됨: SQL Server 문서



Microsoft에서는 거의 매일 [Docs.Microsoft.com](http://docs.microsoft.com/) 설명서 웹 사이트에서 기존 문서 일부를 업데이트합니다. 이 문서에는 최근 업데이트된 문서에서 발췌한 내용이 표시됩니다. 새 문서로 연결되는 링크도 나열될 수 있습니다.

이 문서는 주기적으로 다시 실행되는 프로그램에 의해 생성됩니다. 경우에 따라 발췌한 내용의 형식이 완전하지 않거나 원본 문서의 표식(markdown)으로 표시될 수 있습니다. 이미지는 여기에 표시되지 않습니다.

다음 날짜 범위 및 주제에 대한 최근 업데이트가 보고됩니다.



- 업데이트 날짜 범위: &nbsp; **2018-02-03**&nbsp; - &nbsp;**2018-04-28**
- *주제 영역:* &nbsp; **SQL Server**




&nbsp;

## <a name="new-articles-created-recently"></a>최근에 만든 새로운 문서

다음 링크는 최근에 추가된 새로운 문서로 이동합니다.


1. [SQL Server 설명서에 기여하는 방법](sql-server-docs-contribute.md)
2. [SQL Server 개인 정보 제공](sql-server-privacy.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>업데이트된 문서의 발췌 내용

이 섹션에는 최근에 많이 업데이트된 문서에서 발췌한 업데이트 내용이 표시됩니다.

여기에 표시된 발췌 내용은 적절한 의미 체계 맥락과 분리되어 표시됩니다. 또한 발췌 내용은 때때로 실제 문서에서 이 내용의 주변에 있는 중요한 markdown 구문과도 분리되어 표시됩니다. 따라서 이러한 발췌 내용은 일반적인 지침을 제공하기 위한 것입니다. 이 발췌 내용에서는 관심 내용을 클릭하여 실제 문서를 참조할 가치가 있을지 여부만 파악할 수 있습니다.

따라서 이러한 발췌 내용에서 코드를 복사하거나 발췌 내용을 정확한 사실로 간주하지 마세요. 대신 실제 문서를 참조하세요.





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>최근 업데이트된 문서의 간결한 목록

이 간결한 목록에는 발췌 섹션에 나열된 모든 업데이트된 문서로 연결되는 링크가 있습니다.

1. [SQL Server 2012 서비스 팩 릴리스 정보](#TitleNum_1)
2. [SQL Server 2016 릴리스 정보](#TitleNum_2)
3. [SQL Server 설명서](#TitleNum_3)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-sql-server-2012-service-pack-release-notessql-server-2012-sp4-release-notesmd"></a>1. &nbsp; [SQL Server 2012 서비스 팩 릴리스 정보](sql-server-2012-sp4-release-notes.md)

*업데이트됨: 2018-04-25* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;([다음](#TitleNum_2))

<!-- Source markdown line 57.  ms.author= craigg.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 ce108992ea942b4a11f30d67a1a52d7f26868caa a6269ba2cb2d3b3b54aebf5087dc4d513e476a96  (PR=5676  ,  Filename=sql-server-2012-sp4-release-notes.md  ,  Dirpath=docs\sql-server\  ,  MergeCommitSha40=a85a46312acf8b5a59a8a900310cf088369c4150) -->



- **자동 Soft-NUMA 분할** – SQL 2014 SP2에서 추적 플래그 8079를 서버 수준에서 사용할 때 자동 [Soft-NUMA](https://msdn.microsoft.com/library/ms345357(SQL.120).aspx) 분할이 도입됩니다. 시작하는 동안 추적 플래그 8079를 사용하면 SQL Server 2014 SP2는 하드웨어 레이아웃에 대해 검사하고 시스템 보고에서 NUMA 노드당 8개 이상의 CPU를 가진 소프트 NUMA를 자동으로 구성합니다. 자동 소프트 NUMA 동작은 하이퍼스레드(HT/논리 프로세서)를 인식합니다. 추가 노드를 분할하고 생성하면 수신기 수, 크기 조정 및 네트워크와 암호화 기능을 늘려서 후순위 처리를 조정합니다. 프로덕션 환경에서 설정하기 전에 자동 소프트 NUMA를 사용하여 워크로드의 성능을 첫 번째로 테스트하는 것이 좋습니다.

**서비스 팩 3 릴리스 정보**


**다운로드 페이지**

- [SQL Server 2012 SP3 기능 팩](http://go.microsoft.com/fwlink/?linkid=615935)
- [SQL Server 2012 SP3 Express](http://go.microsoft.com/fwlink/?linkid=692144)

현재 설치된 버전에 따라 다운로드할 파일의 이름과 위치를 확인하기 위한 자세한 내용은 [SQL Server 2012 Service Pack 3 release information](https://support.microsoft.com/help/3072779/sql-server-2012-service-pack-3-release-information)(SQL Server 2012 서비스 팩 3 릴리스 정보)에서 “Select the correct file to download”(다운로드할 올바른 파일 선택) 섹션을 참조하세요.

**서비스 팩 2 릴리스 정보**


**다운로드 페이지**

- [SQL Server 2012 SP2 기능 팩](http://go.microsoft.com/fwlink/?LinkID=401008)
- [SQL Server 2012 SP2 Express](http://go.microsoft.com/fwlink/?LinkID=401007)

아래 표에서 현재 설치된 버전에 따라 다운로드할 파일의 위치와 이름을 확인하세요. 다운로드 페이지에 시스템 요구 사항 및 기본 설치 지침이 나와 있습니다.

|현재 설치된 버전...|및...하려는 경우|다운로드 및 설치...|



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-sql-server-2016-release-notessql-server-2016-release-notesmd"></a>2. &nbsp; [SQL Server 2016 릴리스 정보](sql-server-2016-release-notes.md)

*업데이트됨: 2018-04-27* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;([이전](#TitleNum_1) | [다음](#TitleNum_3))

<!-- Source markdown line 25.  ms.author= craigg.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 a15210866acf524dae49f3a7fd7957c9ffa6a78a 7257cb2017779242cbb8fa2b562f4b102502e942  (PR=5695  ,  Filename=sql-server-2016-release-notes.md  ,  Dirpath=docs\sql-server\  ,  MergeCommitSha40=d1c114b98fea55d2d4829dffdb25daf1b3f73dc2) -->



  이 문서는 서비스 팩을 포함하여 SQL Server 2016 릴리스 관련 제한 사항 및 문제를 설명합니다. 새로운 기능에 대한 자세한 내용은 [SQL Server 2016의 새로운 기능](https://docs.microsoft.com/sql/sql-server/what-s-new-in-sql-server-2016)을 참조하세요.

- **[Evaluation Center](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016)** 에서 SQL Server 2016을 다운로드하세요.
- Azure 가상 머신 소형: Azure 계정이 있나요?  계정이 있는 경우 **[여기](https://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2016sp1standardwindowsserver2016/)** 로 이동하여 SQL Server 2016 SP1이 이미 설치된 가상 머신을 실행해 보세요.
- SSMS 다운로드: SQL Server Management Studio의 최신 버전을 얻으려면 **[SSMS(SQL Server Management Studio) 다운로드]** 를 참조하세요.

**<a name="bkmk_2016sp2"></a>SQL Server 2016 서비스 팩 2(SP2)**


SQL Server 2016 SP2에는 2016 SP1 이후부터 CU8까지 모든 누적 업데이트가 포함되어 있습니다.

- [Microsoft 다운로드 SQL Server 2016 서비스 팩 2(SP2)](https://go.microsoft.com/fwlink/?linkid=869608)
- 업데이트의 전체 목록은 [SQL Server 2016 서비스 팩 2 릴리스 정보](https://support.microsoft.com/help/4052908/sql-server-2016-service-pack-2-release-information)를 참조하세요.



&nbsp;

&nbsp;

---

<a name="TitleNum_3"/>

### <a name="3-nbsp-sql-server-documentationsql-server-technical-documentationmd"></a>3. &nbsp; [SQL Server 설명서](sql-server-technical-documentation.md)

*업데이트됨: 2018-04-27* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;([이전](#TitleNum_2))

<!-- Source markdown line 77.  ms.author= craigg.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 0262010ba39785a6d46b42f8469fb17701f13008 c69a83236391d039381a93c65ebbb2efa53e11b8  (PR=5695  ,  Filename=sql-server-technical-documentation.md  ,  Dirpath=docs\sql-server\  ,  MergeCommitSha40=d1c114b98fea55d2d4829dffdb25daf1b3f73dc2) -->




<!-- : : : m-r -->
**SQL Server를 사용해 보세요.**
- 평가 센터에서 다운로드: [Windows용 SQL Server 다운로드](http://go.microsoft.com/fwlink/?LinkID=829477)
- 평가 센터에서 다운로드: SSMS(SQL Server Management Studio) 다운로드
- 평가 센터에서 다운로드: SSDT(SQL Server Data Tools) 다운로드
- 가상 머신 만들기: [SQL Server가 있는 가상 머신 가져오기](https://azure.microsoft.com/services/virtual-machines/sql-server/?wt.mc_id=sqL16_vm)





## <a name="similar-articles-about-new-or-updated-articles"></a>신규 문서 또는 업데이트된 문서에 대한 유사 문서

이 섹션에는 공용 GitHub.com 리포지토리 내의 다른 주제 영역에서 최근에 업데이트된 문서와 유사한 문서가 나와 있습니다. [MicrosoftDocs/sql-docs](https://github.com/MicrosoftDocs/sql-docs/)



#### <a name="subject-areas-that-do-have-new-or-recently-updated-articles"></a>새로 추가되었거나 최근에 업데이트된 문서가 *있는* 주제 영역

- [새로 추가되었거나 업데이트됨(11+6):&nbsp; &nbsp;**SQL용 고급 분석** 문서](../advanced-analytics/new-updated-advanced-analytics.md)
- [새로 추가되었거나 업데이트됨(18+0): &nbsp; &nbsp;**SQL용 Analysis Services** 문서](../analysis-services/new-updated-analysis-services.md)
- [새로 추가되었거나 업데이트됨(218+14):  **SQL에 연결** 문서](../connect/new-updated-connect.md)
- [새로 추가되었거나 업데이트됨(14+0): &nbsp; &nbsp;**SQL용 데이터베이스 엔진** 문서](../database-engine/new-updated-database-engine.md)
- [새로 추가되었거나 업데이트됨(3+2): &nbsp; &nbsp; **SQL용 Integration Services** 문서](../integration-services/new-updated-integration-services.md)
- [새로 추가되었거나 업데이트됨(3+3): &nbsp; &nbsp; **SQL용 Linux** 문서](../linux/new-updated-linux.md)
- [새로 추가되었거나 업데이트됨(7+10): &nbsp; &nbsp;**SQL용 관계형 데이터베이스** 문서](../relational-databases/new-updated-relational-databases.md)
- [새로 추가되었거나 업데이트됨(0+2): &nbsp; &nbsp; **SQL용 Reporting Services** 문서](../reporting-services/new-updated-reporting-services.md)
- [새로 추가되었거나 업데이트됨(1+3): &nbsp; &nbsp; **SQL Operations Studio** 문서](../sql-operations-studio/new-updated-sql-operations-studio.md)
- [새로 추가되었거나 업데이트됨(2+3): &nbsp; &nbsp; **Microsoft SQL Server** 문서](../sql-server/new-updated-sql-server.md)
- [새로 추가되었거나 업데이트됨(1+1): &nbsp; &nbsp; **SSDT(SQL Server Data Tools)** 문서](../ssdt/new-updated-ssdt.md)
- [새로 추가되었거나 업데이트됨(5+2): &nbsp; &nbsp; **SSMS(SQL Server Management Studio)** 문서](../ssms/new-updated-ssms.md)
- [새로 추가되었거나 업데이트됨(0+2): &nbsp; &nbsp; **Transact-SQL** 문서](../t-sql/new-updated-t-sql.md)
- [새로 추가되었거나 업데이트됨(1+1): &nbsp; &nbsp; **SQL용 도구** 문서](../tools/new-updated-tools.md)



#### <a name="subject-areas-that-do-not-have-any-new-or-recently-updated-articles"></a>새로 추가되었거나 최근에 업데이트된 문서가 *없는* 주제 영역

- [새로 추가되었거나 업데이트됨(0+0): **SQL용 분석 플랫폼 시스템** 문서](../analytics-platform-system/new-updated-analytics-platform-system.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 Data Quality Services** 문서](../data-quality-services/new-updated-data-quality-services.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 DMX(Data Mining Extension)** 문서](../dmx/new-updated-dmx.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 MDS(Master Data Services)** 문서](../master-data-services/new-updated-master-data-services.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 MDX(Multidimensional Expression)** 문서](../mdx/new-updated-mdx.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 ODBC(Open Database Connectivity)** 문서](../odbc/new-updated-odbc.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 PowerShell** 문서](../powershell/new-updated-powershell.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 샘플** 문서](../samples/new-updated-samples.md)
- [새로 추가되었거나 업데이트됨(0+0): **SSMA(SQL Server Migration Assistant)** 문서](../ssma/new-updated-ssma.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 XQuery** 문서](../xquery/new-updated-xquery.md)

