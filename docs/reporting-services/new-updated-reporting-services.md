---
title: "업데이트됨 - SQL Server용 Reporting Services 문서 | Microsoft Docs"
description: "Microsoft SQL Server용 Reporting Services 설명서에서 최근에 변경된 내용에 대해 업데이트된 콘텐츠의 코드 조각을 표시합니다."
services: na
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: 
ms.service: 
ms.component: reporting-services
ms.suite: pro-bi
ms.topic: updart-autogen
ms.technology: database-engine
ms.custom: 
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 12/02/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.author: genemi
ms.workload: reporting-services
ms.openlocfilehash: fc35b1dc39ded10eaf20f503fb561562ce55da98
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/05/2017
---
# <a name="new-and-recently-updated-reporting-services-for-sql-server"></a>새로 추가되거나 최근에 업데이트됨: SQL Server용 Reporting Services



Microsoft에서는 거의 매일 [Docs.Microsoft.com](http://docs.microsoft.com/) 설명서 웹 사이트에서 기존 문서 일부를 업데이트합니다. 이 문서에는 최근 업데이트된 문서에서 발췌한 내용이 표시됩니다. 새 문서로 연결되는 링크도 나열될 수 있습니다.

이 문서는 주기적으로 다시 실행되는 프로그램에 의해 생성됩니다. 경우에 따라 발췌한 내용의 형식이 완전하지 않거나 원본 문서의 표식(markdown)으로 표시될 수 있습니다. 이미지는 여기에 표시되지 않습니다.

다음 날짜 범위 및 주제에 대한 최근 업데이트가 보고됩니다.



- *업데이트 날짜 범위:*  &nbsp; **2017-09-28** &nbsp;부터 &nbsp; **2017-12-02**
- *주제 영역:* &nbsp; **SQL Server용 Reporting Services**.




&nbsp;

## <a name="new-articles-created-recently"></a>최근에 만든 새로운 문서

다음 링크는 최근에 추가된 새로운 문서로 이동합니다.


1. [SQL Server Reporting Services의 변경 로그](change-log-sql-server-reporting-services.md)
2. [Reporting Services에 대한 REST API를 사용하여 개발](developer/rest-api.md)
3. [SharePoint 사이트의 보고서 뷰어 웹 파트](report-server-sharepoint/report-viewer-web-part-sharepoint-site.md)
4. [보고서 뷰어 웹 파트의 SharePoint 사이트 설정](report-server-sharepoint/report-viewer-web-part-sharepoint-site-settings.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>업데이트된 문서의 발췌 내용

이 섹션에는 최근에 많이 업데이트된 문서에서 발췌한 업데이트 내용이 표시됩니다.

여기에 표시된 발췌 내용은 적절한 의미 체계 맥락과 분리되어 표시됩니다. 또한 발췌 내용은 때때로 실제 문서에서 이 내용의 주변에 있는 중요한 markdown 구문과도 분리되어 표시됩니다. 따라서 이러한 발췌 내용은 일반적인 지침을 제공하기 위한 것입니다. 이 발췌 내용에서는 관심 내용을 클릭하여 실제 문서를 참조할 가치가 있을지 여부만 파악할 수 있습니다.

따라서 이러한 발췌 내용에서 코드를 복사하거나 발췌 내용을 정확한 사실로 간주하지 마세요. 대신 실제 문서를 참조하세요.





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>최근 업데이트된 문서의 간결한 목록

이 간결한 목록에는 발췌 섹션에 나열된 모든 업데이트된 문서로 연결되는 링크가 있습니다.

1. [SQL Server Reporting Services 설치](#TitleNum_1)
2. [SharePoint 사이트에 SQL Server Reporting Services 보고서 뷰어 웹 파트 배포](#TitleNum_2)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-install-sql-server-reporting-servicesinstall-windowsinstall-reporting-servicesmd"></a>1. &nbsp; [SQL Server Reporting Services 설치](install-windows/install-reporting-services.md)

*업데이트됨: 2017-11-30* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;([다음](#TitleNum_2))

<!-- Source markdown line 66.  ms.author= "asaxton".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 c959622d4d10a71ed598256e8e284130eb49af5b 77dc1b4f6696e911ed036fc27724ff8a96b79f57  (PR=4150  ,  Filename=install-reporting-services.md  ,  Dirpath=docs\reporting-services\install-windows\  ,  MergeCommitSha40=578bd1c2760866ddeb3523f830cfc3cb6b4ab9af) -->



    > The default path is C:\Program Files\Microsoft SQL Server Reporting Services.

7. 성공적으로 설치 후 **보고서 서버 구성**을 선택하여 Reporting Services 구성 관리자를 시작합니다.

    ![Configure the report server--media/install-reporting-services/report-server-install-configure.png)

**보고서 서버 구성**


설치에서 **보고서 서버 구성**을 설치한 후 **보고서 서버 구성 관리자**가 나타납니다. 자세한 내용은 [Report Server Configuration Manager--reporting-services-configuration-manager-native-mode.md)을 참조하세요.

Reporting Services의 초기 구성을 완료하기 위해 [create a report server database--ssrs-report-server-create-a-report-server-database.md)해야 합니다. 이 단계를 완료하는 데 SQL Server 데이터베이스 서버가 필요합니다.

**다른 서버에 데이터베이스 만들기**


다른 컴퓨터의 데이터베이스 서버에서 보고서 서버 데이터베이스를 만드는 경우 보고서 서버에 대한 서비스 계정을 데이터베이스 서버에서 인식하는 자격 증명으로 변경해야 합니다.

기본적으로 보고서 서버는 가상 서비스 계정을 사용합니다. 다른 서버에서 데이터베이스를 만들려고 하는 경우 연결 적용 권한 단계에서 다음 오류가 나타날 수 있습니다.

`System.Data.SqlClient.SqlException (0x80131904): Windows NT user or group '(null)' not found. Check the name again.`

오류를 해결하기 위해 서비스 계정을 네트워크 서비스 또는 도메인 계정으로 변경할 수 있습니다. 서비스 계정을 네트워크 서비스로 변경하는 것은 보고서 서버에 대한 컴퓨터 계정의 컨텍스트에서 권한을 적용합니다.

자세한 내용은 [Configure the report server service account--configure-the-report-server-service-account-ssrs-configuration-manager.md)를 참조하세요.

**Windows 서비스**


Windows 서비스는 설치의 일부로 만들어집니다. **SQL Server Reporting Services**로 표시됩니다. 서비스 이름은 **SQLServerReportingServices**입니다.



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-deploy-the-sql-server-reporting-services-report-viewer-web-part-on-a-sharepoint-sitereport-server-sharepointdeploy-report-viewer-web-partmd"></a>2. &nbsp; [SharePoint 사이트에 SQL Server Reporting Services 보고서 뷰어 웹 파트 배포](report-server-sharepoint/deploy-report-viewer-web-part.md)

*업데이트됨: 2017-11-30* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;([이전](#TitleNum_1))

<!-- Source markdown line 129.  ms.author= "asaxton".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 99275aa597f491bb09688060b3f713406e2f0624 a282486da6df55154212c98fa06c7e62e66c8350  (PR=4150  ,  Filename=deploy-report-viewer-web-part.md  ,  Dirpath=docs\reporting-services\report-server-sharepoint\  ,  MergeCommitSha40=578bd1c2760866ddeb3523f830cfc3cb6b4ab9af) -->



웹 파트 삭제는 PowerShell을 사용하여 시도될 수 있지만 직접 명령이 없습니다. 스크립트 예제는 [웹 파트 갤러리에서 웹 파트를 삭제하는 방법](https://gallery.technet.microsoft.com/office/How-to-delete-Web-Parts-1132701f)을 참조하세요.

**지원되는 언어**


웹 파트에 지원되는 언어는 다음과 같습니다.

* 영어(en)
* 독일어(de)
* 스페인어(sp)
* 프랑스어(fr)
* 이탈리아어(it)
* 일본어(ja)
* 한국어(ko)
* 포르투갈어(pt)
* 러시아어(ru)
* 중국어(간체 - zh-HANS 및 zh-CHS)







## <a name="similar-articles"></a>유사한 문서

<!--  HOW TO:
    Refresh this file's line items with the latest 'Count-in-Similars*' content.
    Then run Run-533-*.BAT
    2017-12-02  23:00pm
-->

이 섹션에는 공용 GitHub.com 리포지토리 내의 다른 주제 영역에서 최근에 업데이트된 문서와 유사한 문서가 나와 있습니다. [MicrosoftDocs/sql-docs](https://github.com/MicrosoftDocs/sql-docs/)

#### <a name="subject-areas-which-do-have-new-or-recently-updated-articles"></a>새로 추가되었거나 최근에 업데이트된 문서가 있는 주제 영역

- [새로 추가되었거나 업데이트됨(3+14): **SQL용 고급 분석** 문서](../advanced-analytics/new-updated-advanced-analytics.md)
- [새로 추가되었거나 업데이트됨(1+0): **SQL용 Analysis Services** 문서](../analysis-services/new-updated-analysis-services.md)
- [새로 추가되었거나 업데이트됨(87 + 0): **SQL용 분석 플랫폼 시스템** 문서](../analytics-platform-system/new-updated-analytics-platform-system.md)
- [새로 추가되었거나 업데이트됨(5+4): **SQL에 연결** 문서](../connect/new-updated-connect.md)
- [새로 추가되었거나 업데이트됨(0+1): **SQL용 데이터베이스 엔진** 문서](../database-engine/new-updated-database-engine.md)
- [새로 추가되었거나 업데이트됨(2+2): **SQL용 Integration Services** 문서](../integration-services/new-updated-integration-services.md)
- [새로 추가되었거나 업데이트됨(10+9): **SQL용 Linux** 문서](../linux/new-updated-linux.md)
- [새로 추가되었거나 업데이트됨(2+4): **SQL용 관계형 데이터베이스** 문서](../relational-databases/new-updated-relational-databases.md)
- [새로 추가되었거나 업데이트됨(4+2): **SQL용 Reporting Services** 문서](../reporting-services/new-updated-reporting-services.md)
- [새로 추가되었거나 업데이트됨(0+1): **SQL용 샘플** 문서](../sample/new-updated-sample.md)
- [새로 추가되었거나 업데이트됨(21+0): **SQL 작업 Studio** 문서](../sql-operations-studio/new-updated-sql-operations-studio.md)
- [새로 추가되었거나 업데이트됨(5+1): **Microsoft SQL Server** 문서](../sql-server/new-updated-sql-server.md)
- [새로 추가되었거나 업데이트됨(0+1): **SSDT(SQL Server Data Tools)** 문서](../ssdt/new-updated-ssdt.md)
- [새로 추가되었거나 업데이트됨(1+0): **SSMA(SQL Server Migration Assistant)** 문서](../ssma/new-updated-ssma.md)
- [새로 추가되었거나 업데이트됨(0+1): **SSMS(SQL Server Management Studio)** 문서](../ssms/new-updated-ssms.md)
- [새로 추가되었거나 업데이트됨(0+2): **Transact-SQL** 문서](../t-sql/new-updated-t-sql.md)

#### <a name="subject-areas-which-have-no-new-or-recently-updated-articles"></a>새로 추가되었거나 최근에 업데이트된 문서가 없는 주제 영역

- [새로 추가되었거나 업데이트됨(0+0): **SQL용 DMA(Data Migration Assistant)** 문서](../dma/new-updated-dma.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 ADO(ActiveX Data Objects)** 문서](../ado/new-updated-ado.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 Data Quality Services** 문서](../data-quality-services/new-updated-data-quality-services.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 DMX(Data Mining Extension)** 문서](../dmx/new-updated-dmx.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 MDS(Master Data Services)** 문서](../master-data-services/new-updated-master-data-services.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 MDX(Multidimensional Expression)** 문서](../mdx/new-updated-mdx.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 ODBC(Open Database Connectivity)** 문서](../odbc/new-updated-odbc.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 PowerShell** 문서](../powershell/new-updated-powershell.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 도구** 문서](../tools/new-updated-tools.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 XQuery** 문서](../xquery/new-updated-xquery.md)


