---
title: "업데이트됨 - SQL Server용 SSDT 문서 | Microsoft Docs"
description: "Microsoft SQL Server용 SSDT(SQL Server Data Tools) 설명서에서 최근에 변경된 내용에 대해 업데이트된 콘텐츠의 코드 조각을 표시합니다."
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
ms.date: 06/30/2017
ms.author: genemi
ms.workload: ssdt-sql-server-data-tools
ms.translationtype: Human Translation
ms.sourcegitcommit: dcf26be9dc2e502b2d01f5d05bcb005fd7938017
ms.openlocfilehash: 5e43cb76dac922b3c43318b2a9f539ab19ec7bfe
ms.contentlocale: ko-kr
ms.lasthandoff: 07/03/2017

---
<a id="new-and-recently-updated-sql-server-data-tools-ssdt" class="xliff"></a>

# 새로 추가되었거나 최근에 업데이트됨: SSDT(SQL Server Data Tools)



거의 매일 Microsoft 업데이트 기존 아티클 중 일부에 해당 [Docs.Microsoft.com](http://docs.microsoft.com/) 설명서 웹 사이트입니다. 이 문서에는 최근에 업데이트 된 문서에서 발췌 한 내용 표시 됩니다. 새 문서와 연결도 나열 되어 있습니다.

이 문서는 주기적으로 다시 실행 하는 프로그램에서 생성 됩니다. 경우에 따라 발췌 한 구문을 소스 문서에서 불완전 한 서식을 사용 하 여 또는 마크 다운으로 나타날 수 있습니다. 이미지는 여기에 표시 되지 않습니다.

다음 날짜 범위 및 주체에 대 한 최신 업데이트가 보고 됩니다.



- *업데이트 날짜 범위:* &nbsp; **2017-05-17** &nbsp; ~ &nbsp; **2017-06-30**
- *주제 영역:* &nbsp; **SSDT(SQL Server Data Tools)**.




&nbsp;

<a id="new-articles-created-recently" class="xliff"></a>

## 최근에 만든 새로운 문서

다음 링크는 최근에 추가된 새로운 문서로 이동합니다.


*지금은 나열할 새 문서가 없습니다.*



&nbsp;

<a id="updated-articles-with-excerpts" class="xliff"></a>

## 부분 업데이트 되는 문서

이 섹션에는 최근에 발견 된 대규모 업데이트를 문서에서 수집 하는 업데이트의 발췌 한 내용 표시 됩니다.

여기에 표시 된 부분 적절 한 의미 체계 컨텍스트에서 분리 된 나타납니다. 또한 때로는 실제 문서의 주위에 있는 중요 한 마크 다운 구문에서 발췌 한 구문을 분리 됩니다. 따라서 이러한 발췌 한이 내용에 대 한 일반적인 지침만 됩니다. 발췌 한 내용 관심 분야를 클릭 하 고 실제 문서를 참조 하는 데 시간이 걸리는 보증 있는지 여부를 알 수 있습니다에 사용 합니다.

이러한 및 기타 이유로 이러한 부분에서 코드를 복사 하지 않으려면 및 사용 하지 않습니다 정확한 진리도 모든 텍스트 발췌문 합니다. 대신 실제 문서를 참조 합니다.



&nbsp;

&nbsp;

<a name="TitleNum_1"/>

<a id="1-nbsp-changelog-for-sql-server-data-tools-ssdtchangelog-for-sql-server-data-tools-ssdtmd" class="xliff"></a>

### 1. &nbsp; [SSDT(SQL Server Data Tools)에 대한 변경 로그](changelog-for-sql-server-data-tools-ssdt.md)

*업데이트됨: 2017-05-19* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; 

<!-- Source markdown line 21.  ms.author= "sstein".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 cf17883ce0daf75fdf88881171bf4042558b1cf4 536fe0fe41b023a4186f494a509fa14fcbafccf4  (PR=1777  ,  Filename=changelog-for-sql-server-data-tools-ssdt.md  ,  Dirpath=docs\ssdt\  ,  MergeCommitSha40=5bd0e1d3955d898824d285d28979089e2de6f322) -->



새로운 기능과 변경된 기능에 대한 자세한 게시물은 [SSDT 팀 블로그](https://blogs.msdn.microsoft.com/ssdt/)를 참조하세요.

**SSDT 17.1**

빌드 번호: 14.0.61705.170

**새로운 기능**

**AS 프로젝트:**
- 사용자가 UI 1400 모델에서의 열에 대 한 힌트를 인코딩을 설정할 수 있습니다.
- IntelliSense 모델과 관련 된 오프 라인 모드에서 출시 되었습니다.
- 테이블 형식 모델 탐색기에는 이제 모델 (1400 호환성 수준의 테이블 형식 모델)에서 사용할 수 있는 명명 된 M 식을 나타내는 노드가 포함
- Azure Active Directory 사용자 선택 테이블 형식 모델의 역할 멤버를 설정할 때 이제 사용할 수 있는 Microsoft Azure 포털의 IAM 비슷합니다

**데이터베이스 프로젝트:**
- 17.1 DacFx에 대 한 업데이트

**버그 수정**

- 여기서 비즈니스 인텔리전스 디자이너 그룹 이름을 잘못 표시 VS2017에서 Visual Studio 옵션에서 문제 해결
- 보고서 프로젝트를 솔루션에 대 한 코드 맵을 생성 충돌이 발생할 수 위치나 프로젝트으로 문제가 해결 되었습니다.
- Analysis Services 1400 compat 수준 테이블 형식 모델에 대 한 PowerQuery 통합 있는 여러 가지 문제 해결
- 문제가 해결 되었습니다. 새 DAX 편집기에서 대입 연산자 수 없는 별도 줄에는 측정값을 정의할 때 도구 창
- 테이블 형식 측정값 표시 관점에서 측정값 이름을 바꿀 때 업데이트 하지 못하는 문제가 해결 되었습니다.
- SQL Server 2016 Analysis Services 서버에 배포 하는 업데이트 된 Analysis Services 통합된 작업 영역 엔진 및 테이블 형식 개체 모델을 1200에 오류가 발생 하는 번역을 포함 하는 테이블 형식 프로젝트를 발생 시킨 회귀 수정
- 새 1400 테이블 형식 데이터 원본의 매우 느리고 creation\deletion 변경한 성능 문제를 수정
- 다차원 모델에 DSV 다이어그램 다른 Dsv 간에 신속 하 게 뷰를 변경 하는 경우 렌더링을 중지할 수 문제 해결

**DacFx 17.1**

- 문제가 해결 되었습니다. 다른 id 열이 있는 메모리 액세스에 최적화 된 테이블이 포함 된 열을 암호화 하는 경우
- CREATE DATABASE에 대 한 CATALOG_COLLATION 옵션에 대 한 SQLDOM 지원





&nbsp;

<a name="compactupdatedlist"/>

<a id="compact-list-of-articles-updated-recently" class="xliff"></a>

## Compact를 최근에 업데이트 하는 문서 목록

이 압축 목록 이전 섹션에 나열 된 모든 업데이트 된 문서에 대 한 링크를 제공 합니다.

1. [SSDT(SQL Server Data Tools)에 대한 변경 로그](#TitleNum_1)




<a name="sisters2"/>

&nbsp;

<a id="sister-articles" class="xliff"></a>

## 대체 문서

이 섹션에는 동일한 GitHub.com 리포지토리 내의 다른 주제 영역에서 최근에 업데이트된 문서와 유사한 문서가 나와 있습니다. [MicrosoftDocs/**sql-docs-pr**](https://github.com/microsoftdocs/sql-docs-pr/).

<!--  20170630-1150  -->

<a id="subject-areas-which-do-have-new-or-recently-updated-articles" class="xliff"></a>

#### 새로 추가되었거나 최근에 업데이트된 문서가 있는 주제 영역

- [새로 추가되었거나 업데이트됨(12+2): **SQL용 고급 분석** 문서](../advanced-analytics/new-updated-advanced-analytics.md)
- [새로 추가되었거나 업데이트됨(1+0): **SQL용 Analysis Services** 문서](../analysis-services/new-updated-analysis-services.md)
- [새로 추가되었거나 업데이트됨(0+2): **SQL에 연결** 문서](../connect/new-updated-connect.md)
- [새로 추가되었거나 업데이트됨(3+0): **SQL용 데이터베이스 엔진** 문서](../database-engine/new-updated-database-engine.md)
- [새로 추가되었거나 업데이트됨(1+2): **SQL용 Integration Services** 문서](../integration-services/new-updated-integration-services.md)
- [새 + 업데이트 (2 + 8): **SQL용 Linux** docs](../linux/new-updated-linux.md)
- [새로 추가되었거나 업데이트됨(1+0): **SQL용 MDS(Master Data Services)** 문서](../master-data-services/new-updated-master-data-services.md)
- [새로 추가되었거나 업데이트됨(5+5): **SQL용 관계형 데이터베이스** 문서](../relational-databases/new-updated-relational-databases.md)
- [새로 추가되었거나 업데이트됨(2+0): **SQL용 Reporting Services** 문서](../reporting-services/new-updated-reporting-services.md)
- [새로 추가되었거나 업데이트됨(0+4): **Microsoft SQL Server** 문서](../sql-server/new-updated-sql-server.md)
- [새로 추가되었거나 업데이트됨(0+1): **SSDT(SQL Server Data Tools)** 문서](../ssdt/new-updated-ssdt.md)
- [새로 추가되었거나 업데이트됨(0+1): **SSMS(SQL Server Management Studio)** 문서](../ssms/new-updated-ssms.md)
- [새로 추가되었거나 업데이트됨(1+0): **SQL용 도구** 문서](../tools/new-updated-tools.md)


<a id="subject-areas-which-have-no-new-or-recently-updated-articles" class="xliff"></a>

#### 새로 추가되었거나 최근에 업데이트된 문서가 없는 주제 영역

- [새로 추가되었거나 업데이트됨(0+0): **SQL용 ADO(ActiveX Data Objects)** 문서](../ado/new-updated-ado.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 Data Quality Services** 문서](../data-quality-services/new-updated-data-quality-services.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 DMX(Data Mining Extension)** 문서](../dmx/new-updated-dmx.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 MDX(Multidimensional Expression)** 문서](../mdx/new-updated-mdx.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 ODBC(Open Database Connectivity)** 문서](../odbc/new-updated-odbc.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 PowerShell** 문서](../powershell/new-updated-powershell.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 샘플** 문서](../sample/new-updated-sample.md)
- [새로 추가되었거나 업데이트됨(0+0): **SSMA(SQL Server Migration Assistant)** 문서](../ssma/new-updated-ssma.md)
- [새로 추가되었거나 업데이트됨(0+0): **Transact-SQL** 문서](../t-sql/new-updated-t-sql.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 XQuery** 문서](../xquery/new-updated-xquery.md)


&nbsp;


