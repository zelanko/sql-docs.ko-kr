---
title: "업데이트됨 - SQL Server용 SSMS 문서 | Microsoft Docs"
description: "Microsoft SQL Server용 SSMS(SQL Server Management Studio) 설명서에서 최근에 변경된 내용에 대해 업데이트된 콘텐츠의 코드 조각을 표시합니다."
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
ms.workload: ssms-sql-server-management-studio
ms.translationtype: HT
ms.sourcegitcommit: 15080827744c19120a8474f3142004c4af7a4064
ms.openlocfilehash: 917198902baf85f2bae57c9ade9f8d3e29dea357
ms.contentlocale: ko-kr
ms.lasthandoff: 09/13/2017

---
# <a name="new-and-recently-updated-sql-server-management-studio-ssms-for-sql-server"></a>새로 추가되었거나 최근에 업데이트됨: SQL Server용 SSMS(SQL Server Management Studio)



Microsoft에서는 거의 매일 [Docs.Microsoft.com](http://docs.microsoft.com/) 설명서 웹 사이트에서 기존 문서 일부를 업데이트합니다. 이 문서에는 최근 업데이트된 문서에서 발췌한 내용이 표시됩니다. 새 문서로 연결되는 링크도 나열될 수 있습니다.

이 문서는 주기적으로 다시 실행되는 프로그램에 의해 생성됩니다. 경우에 따라 발췌한 내용의 형식이 완전하지 않거나 원본 문서의 표식(markdown)으로 표시될 수 있습니다. 이미지는 여기에 표시되지 않습니다.

다음 날짜 범위 및 주제에 대한 최근 업데이트가 보고됩니다.



- *업데이트 날짜 범위:* &nbsp; **2017-07-18** &nbsp; -to- &nbsp; **2017-09-11**
- *주제 영역:* &nbsp; **SSMS(SQL Server Management Studio)**.




&nbsp;

## <a name="new-articles-created-recently"></a>최근에 만든 새로운 문서

다음 링크는 최근에 추가된 새로운 문서로 이동합니다.


1. [SQL Server Management Studio의 출력 창](output-window.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>업데이트된 문서의 발췌 내용

이 섹션에는 최근에 많이 업데이트된 문서에서 발췌한 업데이트 내용이 표시됩니다.

여기에 표시된 발췌 내용은 적절한 의미 체계 맥락과 분리되어 표시됩니다. 또한 발췌 내용은 때때로 실제 문서에서 이 내용의 주변에 있는 중요한 markdown 구문과도 분리되어 표시됩니다. 따라서 이러한 발췌 내용은 일반적인 지침을 제공하기 위한 것입니다. 이 발췌 내용에서는 관심 내용을 클릭하여 실제 문서를 참조할 가치가 있을지 여부만 파악할 수 있습니다.

따라서 이러한 발췌 내용에서 코드를 복사하거나 발췌 내용을 정확한 사실로 간주하지 마세요. 대신 실제 문서를 참조하세요.





&nbsp;

<a name="compactupdatedlist"/>

## <a name="compact-list-of-articles-updated-recently"></a>최근 업데이트된 문서의 간결한 목록

이 간결한 목록에는 발췌 섹션에 나열된 모든 업데이트된 문서로 연결되는 링크가 있습니다.

1. [SSMS(SQL Server Management Studio) 다운로드](#TitleNum_1)
2. [SQL Server 또는 Azure SQL Database에 연결](#TitleNum_2)
3. [SQL Server Management Studio - 변경 로그(SSMS)](#TitleNum_3)를 참조하세요.
4. [데이터베이스 테이블 생성 및 업데이트](#TitleNum_4)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-download-sql-server-management-studio-ssmsdownload-sql-server-management-studio-ssmsmd"></a>1. &nbsp; [SSMS(SQL Server Management Studio) 다운로드](download-sql-server-management-studio-ssms.md)

*업데이트됨: 2017-08-07* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;([다음](#TitleNum_2))

<!-- Source markdown line 63.  ms.author= "sstein".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 23260f301f86651061b47065bee43d42c92a7be4 0c2178d96b621b96bfcd2fbb782f24792debb407  (PR=2775  ,  Filename=download-sql-server-management-studio-ssms.md  ,  Dirpath=docs\ssms\  ,  MergeCommitSha40=3f12671ace99d5fefc199c7b1c2db31e5b3cfade) -->



SSMS 17.2는 최신 버전의 SQL Server Management Studio입니다. 17.X 세대의 SSMS는 SQL Server 2017을 통해 SQL Server 2008의 거의 모든 기능 영역을 지원합니다. 버전 17.x는 SQL Analysis Service PaaS도 지원합니다.

17.2 버전에는 다음이 포함됩니다.

- MFA(Multi-Factor Authentication)
  - MFA(Multi-Factor Authentication)를 지원하는 UA(유니버설 인증)에 대한 다중 사용자 Azure AD 인증
  - 다중 사용자 인증을 지원하기 위해서 새 사용자 자격 증명 입력 필드가 MFA를 지원하는 유니버설 인증에 대해 추가되었습니다.
- 이제 연결 대화 상자는 다음 5개 인증 방법을 지원합니다.
  - Windows 인증
  - SQL Server 인증(SQL Server Authentication)
  - Active Directory - MFA 지원을 포함한 유니버설 인증
  - Active Directory - 암호
  - Active Directory - 통합

- 이제 DACFx 마법사에 대한 데이터베이스 가져오기/내보내기는 MFA를 지원하는 유니버설 인증을 사용할 수 있습니다.
- API 지원에 대해서는 [IUniversalAuthProvider 인터페이스](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.iuniversalauthprovider.aspx)를 참조하세요.
- MFA를 지원하는 Azure AD 유니버설 인증에 사용되는 ADAL 관리 라이브러리가 버전 3.13.9로 업그레이드되었습니다.
- SQL Database 및 SQL Data Warehouse에 대한 Azure AD 관리자 설정을 지원하는 새 CLI 인터페이스.

 Active Directory 인증 방법에 대한 자세한 내용은 [SQL Database 및 SQL Data Warehouse에 대한 유니버설 인증(MFA에 대한 SSMS 지원)](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication) 및 [SQL Server Management Studio에 대한 Azure SQL Database 다단계 인증 구성](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication-configure)을 참조하세요.

- 출력 창에는 개체 탐색기 노드를 확장하는 동안 실행되는 쿼리에 대한 항목이 있습니다.
- Azure SQL Database에 대해 뷰 디자이너 사용 설정
- SSMS의 개체 탐색기에서 개체를 스크립팅하기 위한 기본 스크립팅 옵션이 변경되었습니다.



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-connect-to-a-sql-server-or-azure-sql-databaseobjectconnect-to-an-instance-from-object-explorermd"></a>2. &nbsp; [SQL Server 또는 Azure SQL Database에 연결](object/connect-to-an-instance-from-object-explorer.md)

*업데이트됨: 2017-08-25* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;([이전](#TitleNum_1) | [다음](#TitleNum_3))

<!-- Source markdown line 40.  ms.author= "sstein".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 cfd72893c35c87df96dc8605807e542be28936e2 840981d3a115a15774a8e47ee2f6a0e5c4177b01  (PR=2961  ,  Filename=connect-to-an-instance-from-object-explorer.md  ,  Dirpath=docs\ssms\object\  ,  MergeCommitSha40=21f0cfd102a6fcc44dfc9151750f1b3c936aa053) -->



   ![firewall--../media/connect-to-server/new-firewall-rule.png)

1. 방화벽 규칙을 만들고 서버에 연결하려면 **확인**을 클릭합니다.

1. 성공적으로 연결되면 서버가 **개체 탐색기**에 표시됩니다.

   ![connected--../media/connect-to-server/connected.png)

**다음 단계**


[Design, Create, and Update Tables--../visual-db-tools/design-tables-visual-database-tools.md)

**관련 항목**


[SQL Server Management Studio (SSMS)--../sql-server-management-studio-ssms.md) [Download SQL Server Management Studio (SSMS)--../download-sql-server-management-studio-ssms.md)

[Analysis Services](https://docs.microsoft.com/sql/analysis-services/instances/connect-to-analysis-services)
[Integration Services](https://docs.microsoft.com/sql/integration-services/sql-server-integration-services)
[Reporting Services](https://docs.microsoft.com/sql/reporting-services/tools/connect-to-a-report-server-in-management-studio)



&nbsp;

&nbsp;

---

<a name="TitleNum_3"/>

### <a name="3-nbsp-sql-server-management-studio---changelog-ssmssql-server-management-studio-changelog-ssmsmd"></a>3. &nbsp; [SQL Server Management Studio - 변경 로그(SSMS)](sql-server-management-studio-changelog-ssms.md)

*업데이트됨: 2017-08-07* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;([이전](#TitleNum_2) | [다음](#TitleNum_4))

<!-- Source markdown line 20.  ms.author= "sstein".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 1733ce3c556db1e51cb27bf830429f2c42e8f97e 2abb24fd6547e438181039d095cbad027473a57e  (PR=2775  ,  Filename=sql-server-management-studio-changelog-ssms.md  ,  Dirpath=docs\ssms\  ,  MergeCommitSha40=3f12671ace99d5fefc199c7b1c2db31e5b3cfade) -->



이 문서에서는 SSMS의 현재 버전과 이전 버전에 대한 업데이트, 향상 및 버그 수정에 대한 세부 정보를 제공합니다. [previous SSMS versions below--#previous-ssms-releases)를 다운로드합니다.

**[SSMS 17.2--download-sql-server-management-studio-ssms.md)**


일반 공급 | 빌드 번호: 14.0.17177.0

**개선 사항**


- MFA(Multi-Factor Authentication)
  - MFA(Multi-Factor Authentication)를 지원하는 UA(유니버설 인증)에 대한 다중 사용자 Azure AD 인증
  - 다중 사용자 인증을 지원하기 위해서 새 사용자 자격 증명 입력 필드가 MFA를 지원하는 유니버설 인증에 대해 추가되었습니다.
- 이제 연결 대화 상자는 다음 5개 인증 방법을 지원합니다.
  - Windows 인증
  - SQL Server 인증(SQL Server Authentication)
  - Active Directory - MFA 지원을 포함한 유니버설 인증
  - Active Directory - 암호
  - Active Directory - 통합

- MFA를 지원하는 유니버설 인증을 사용하여 DACFx 마법사에 대한 데이터베이스 내보내기/가져오기를 사용할 수 있습니다.
- API 지원에 대해서는 [IUniversalAuthProvider 인터페이스](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.iuniversalauthprovider.aspx)를 참조하세요.
- MFA를 지원하는 Azure AD 유니버설 인증에 사용되는 ADAL 관리 라이브러리가 버전 3.13.9로 업그레이드되었습니다.
- 또한 SQL Database 및 SQL Data Warehouse에 대한 Azure AD 관리자 설정을 지원하는 새 CLI 인터페이스가 제공되었습니다.

 Active Directory 인증 방법에 대한 자세한 내용은 [SQL Database 및 SQL Data Warehouse에 대한 유니버설 인증(MFA에 대한 SSMS 지원)](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication) 및 [SQL Server Management Studio에 대한 Azure SQL Database 다단계 인증 구성](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication-configure)을 참조하세요.

- 출력 창에는 개체 탐색기 노드를 확장하는 동안 실행되는 쿼리에 대한 항목이 있습니다.



&nbsp;

&nbsp;

---

<a name="TitleNum_4"/>

### <a name="4-nbsp-create-and-update-database-tablesvisual-db-toolsdesign-tables-visual-database-toolsmd"></a>4. &nbsp; [데이터베이스 테이블 생성 및 업데이트](visual-db-tools/design-tables-visual-database-tools.md)

*업데이트됨: 2017-08-25* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([이전](#TitleNum_3))

<!-- Source markdown line 30.  ms.author= "sstein".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 f63884ac2d04889e70c505cb5262c8dd81d73ee7 4b4c7aa5e8a0548405f02d11a66b722219fa78f0  (PR=2961  ,  Filename=design-tables-visual-database-tools.md  ,  Dirpath=docs\ssms\visual-db-tools\  ,  MergeCommitSha40=21f0cfd102a6fcc44dfc9151750f1b3c936aa053) -->



**테이블 만들기**


1. 데이터베이스에서 **테이블** 노드를 마우스 오른쪽 단추로 클릭하고 **새** > **테이블**을 선택합니다.

    ![New table--../media/design-tables/new-table.png)

1. 테이블에 [columns--column-properties-visual-database-tools.md)를 추가합니다.

    ![design table--../media/design-tables/new-table2.png)

1. 디자이너를 닫고 변경 내용을 저장합니다.

**테이블 업데이트**


1. 데이터베이스의 **테이블** 노드 아래 테이블을 마우스 오른쪽 단추로 클릭하고 **디자인**을 선택합니다.

   ![Update table--../media/design-tables/update-table.png)

1. 원하는 테이블 설정을 업데이트합니다.

   ![--../media/design-tables/update-table2.png)

1. 디자이너를 닫고 변경 내용을 저장합니다.

**관련 항목**


[테이블](http://msdn.microsoft.com/82d7819c-b801-4309-a849-baa63083e83f) [Table Properties &#40;Visual Database Tools&#41;--../../ssms/visual-db-tools/table-properties-visual-database-tools.md) [Column Properties--column-properties-visual-database-tools.md) [Add Columns to a Table--../../relational-databases/tables/add-columns-to-a-table-database-engine.md) [Primary and Foreign Keys--../../relational-databases/tables/primary-and-foreign-key-constraints.md) [Indexes--../../relational-databases/indexes/indexes.md) [Data types (Transact-SQL)--../../t-sql/data-types/data-types-transact-sql.md) [Download SQL Server Management Studio (SSMS)--../download-sql-server-management-studio-ssms.md)







## <a name="similar-articles"></a>유사한 문서

<!--  HOW TO:
    Refresh this file's line items with the latest 'Count-in-Similars*' content.
    Then run Run-533-*.BAT
-->

이 섹션에는 공용 GitHub.com 리포지토리 내의 다른 주제 영역에서 최근에 업데이트된 문서와 유사한 문서가 나와 있습니다. [MicrosoftDocs/sql-docs](https://github.com/MicrosoftDocs/sql-docs/)

#### <a name="subject-areas-which-do-have-new-or-recently-updated-articles"></a>새로 추가되었거나 최근에 업데이트된 문서가 있는 주제 영역

- [새로 추가되었거나 업데이트됨(3+12): **SQL용 고급 분석** 문서](../advanced-analytics/new-updated-advanced-analytics.md)
- [새로 추가되었거나 업데이트됨(5+0): **SQL에 연결** 문서](../connect/new-updated-connect.md)
- [새로 추가되었거나 업데이트됨(5+1): **SQL용 데이터베이스 엔진** 문서](../database-engine/new-updated-database-engine.md)
- [새로 추가되었거나 업데이트됨(19+82): **SQL용 Integration Services** 문서](../integration-services/new-updated-integration-services.md)
- [새로 추가되었거나 업데이트됨(1+8): **SQL용 Linux** 문서](../linux/new-updated-linux.md)
- [새로 추가되었거나 업데이트됨(12+1): **SQL용 관계형 데이터베이스** 문서](../relational-databases/new-updated-relational-databases.md)
- [새로 추가되었거나 업데이트됨(0+1): **SQL용 Reporting Services** 문서](../reporting-services/new-updated-reporting-services.md)
- [새로 추가되었거나 업데이트됨(7+1): **Microsoft SQL Server** 문서](../sql-server/new-updated-sql-server.md)
- [새로 추가되었거나 업데이트됨(1+1): **SSDT(SQL Server Data Tools)** 문서](../ssdt/new-updated-ssdt.md)
- [새로 추가되었거나 업데이트됨(0+2): **SSMA(SQL Server Migration Assistant)** 문서](../ssma/new-updated-ssma.md)
- [새로 추가되었거나 업데이트됨(1+4): **SSMS(SQL Server Management Studio)** 문서](../ssms/new-updated-ssms.md)
- [새로 추가되었거나 업데이트됨(4+1): **Transact-SQL** 문서](../t-sql/new-updated-t-sql.md)
- [새로 추가되었거나 업데이트됨(0+1): **SQL용 도구** 문서](../tools/new-updated-tools.md)

#### <a name="subject-areas-which-have-no-new-or-recently-updated-articles"></a>새로 추가되었거나 최근에 업데이트된 문서가 없는 주제 영역

- [새로 추가되었거나 업데이트됨(0+0): **SQL용 ADO(ActiveX Data Objects)** 문서](../ado/new-updated-ado.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 Analysis Services** 문서](../analysis-services/new-updated-analysis-services.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 Data Quality Services** 문서](../data-quality-services/new-updated-data-quality-services.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 DMX(Data Mining Extension)** 문서](../dmx/new-updated-dmx.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 MDS(Master Data Services)** 문서](../master-data-services/new-updated-master-data-services.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 MDX(Multidimensional Expression)** 문서](../mdx/new-updated-mdx.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 ODBC(Open Database Connectivity)** 문서](../odbc/new-updated-odbc.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 PowerShell** 문서](../powershell/new-updated-powershell.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 샘플** 문서](../sample/new-updated-sample.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 XQuery** 문서](../xquery/new-updated-xquery.md)



