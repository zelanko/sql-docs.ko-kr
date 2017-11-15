---
title: "업데이트됨 - 데이터베이스 엔진 설명서 | Microsoft Docs"
description: "데이터베이스 엔진 설명서에서 최근에 변경되어 업데이트된 내용 중에서 발췌한 부분을 표시합니다."
services: na
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: barbkess
ms.service: na
ms.topic: updart-autogen
ms.technology: database-engine
ms.custom: UpdArt.exe
ms.workload: database-engine
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 09/27/2017
ms.author: genemi
ms.openlocfilehash: dc4a5516662b200b4224facbb4c9cf4588c1b42e
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="new-and-recently-updated-database-engine-docs"></a>신규 및 최근 업데이트: 데이터베이스 엔진 설명서



Microsoft에서는 거의 매일 [Docs.Microsoft.com](http://docs.microsoft.com/) 설명서 웹 사이트에서 기존 문서 일부를 업데이트합니다. 이 문서에는 최근 업데이트된 문서에서 발췌한 내용이 표시됩니다. 새 문서로 연결되는 링크도 나열될 수 있습니다.

이 문서는 주기적으로 다시 실행되는 프로그램에 의해 생성됩니다. 경우에 따라 발췌한 내용의 형식이 완전하지 않거나 원본 문서의 표식(markdown)으로 표시될 수 있습니다. 이미지는 여기에 표시되지 않습니다.

다음 날짜 범위 및 주제에 대한 최근 업데이트가 보고됩니다.



- *업데이트 날짜 범위:*  &nbsp; **2017-09-11** &nbsp; 부터 &nbsp; **2017-09-27**
- *주제 영역:* &nbsp; **데이터베이스 엔진**




&nbsp;

## <a name="new-articles-created-recently"></a>최근에 만든 새로운 문서

다음 링크는 최근에 추가된 새로운 문서로 이동합니다.


1. [SQL Server 인스턴스에 기능 추가(설치 프로그램)](install-windows/add-features-to-an-instance-of-sql-server-setup.md)
2. [명령 프롬프트에서 SQL Server 설치](install-windows/install-sql-server-from-the-command-prompt.md)
3. [구성 파일을 사용하여 SQL Server 설치](install-windows/install-sql-server-using-a-configuration-file.md)
4. [비즈니스 연속성 및 데이터베이스 복구 - SQL Server](sql-server-business-continuity-dr.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>업데이트된 문서의 발췌 내용

이 섹션에는 최근에 많이 업데이트된 문서에서 발췌한 업데이트 내용이 표시됩니다.

여기에 표시된 발췌 내용은 적절한 의미 체계 맥락과 분리되어 표시됩니다. 또한 발췌 내용은 때때로 실제 문서에서 이 내용의 주변에 있는 중요한 markdown 구문과도 분리되어 표시됩니다. 따라서 이러한 발췌 내용은 일반적인 지침을 제공하기 위한 것입니다. 이 발췌 내용에서는 관심 내용을 클릭하여 실제 문서를 참조할 가치가 있을지 여부만 파악할 수 있습니다.

따라서 이러한 발췌 내용에서 코드를 복사하거나 발췌 내용을 정확한 사실로 간주하지 마세요. 대신 실제 문서를 참조하세요.





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>최근 업데이트된 문서의 간결한 목록

이 간결한 목록에는 발췌 섹션에 나열된 모든 업데이트된 문서로 연결되는 링크가 있습니다.

1. [명령 프롬프트에서 업데이트 설치](#TitleNum_1)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-installing-updates-from-the-command-promptinstall-windowsinstalling-updates-from-the-command-promptmd"></a>1. &nbsp; [명령 프롬프트에서 업데이트 설치](install-windows/installing-updates-from-the-command-prompt.md)

*업데이트됨: 2017-09-12* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; 

<!-- Source markdown line 48.  ms.author= "mikeray".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 04abb23d0682c23654a55e7926d2140f0b6ae408 a4bb1e27ae99460a66da72848ace1417b148f85c  (PR=3122  ,  Filename=installing-updates-from-the-command-prompt.md  ,  Dirpath=docs\database-engine\install-windows\  ,  MergeCommitSha40=1df54edd5857ac2816fa4b164d268835d9713638) -->



- 컴퓨터에서 ..!NCLUDE-NotShown--ssNoVersion--../../includes/ssnoversion-md.md)]의 모든 인스턴스와 ..!NCLUDE-NotShown--ssISnoversion--../../includes/ssisnoversion-md.md)]와 같은 모든 공유 구성 요소 및 관리 도구 업데이트:

```
    <package_name>.exe /qs /IAcceptSQLServerLicenseTerms /Action=Patch /AllInstances.
```

- ..!NCLUDE-NotShown--ssNoVersion--../../includes/ssnoversion-md.md)]의 단일 인스턴스와 ..!NCLUDE-NotShown--ssISnoversion--../../includes/ssisnoversion-md.md)]와 같은 모든 공유 구성 요소 및 관리 도구에서 업데이트 제거:

```
    <package_name>.exe /qs /Action=RemovePatch /InstanceName=MyInstance.
```

- ..!NCLUDE-NotShown--ssNoVersion--../../includes/ssnoversion-md.md)]와 ..!NCLUDE-NotShown--ssISnoversion--../../includes/ssisnoversion-md.md)]와 같은 공유 구성 요소 및 관리 도구에서 업데이트 제거:

```
    <package_name>.exe /qs /Action=RemovePatch
```







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


