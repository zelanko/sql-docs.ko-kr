---
title: 업데이트된 기능 - SQL Server Integration Services 문서 | Microsoft Docs
description: Microsoft SQL Server Integration Services 설명서에서 최근에 변경되어 업데이트된 내용의 코드 조각을 표시합니다.
manager: craigg
author: MightyPen
ms.author: genemi
ms.topic: conceptual
ms.custom: UpdArt.exe
ms.suite: sql
ms.technology: release-landing
ms.prod: sql
ms.prod_service: sql-non-specified
ms.date: 04/28/2018
ms.openlocfilehash: 2a853be10aba997c4cb08f68951aa64233c8a578
ms.sourcegitcommit: c8f7e9f05043ac10af8a742153e81ab81aa6a3c3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/17/2018
ms.locfileid: "39083505"
---
# <a name="new-and-recently-updated-integration-services-for-sql-server"></a>새로운 기능 및 최근에 업데이트된 기능: SQL Server Integration Services



Microsoft에서는 거의 매일 [Docs.Microsoft.com](http://docs.microsoft.com/) 설명서 웹 사이트에서 기존 문서 일부를 업데이트합니다. 이 문서에는 최근 업데이트된 문서에서 발췌한 내용이 표시됩니다. 새 문서로 연결되는 링크도 나열될 수 있습니다.

이 문서는 주기적으로 다시 실행되는 프로그램에 의해 생성됩니다. 경우에 따라 발췌한 내용의 형식이 완전하지 않거나 원본 문서의 표식(markdown)으로 표시될 수 있습니다. 이미지는 여기에 표시되지 않습니다.

다음 날짜 범위 및 주제에 대한 최근 업데이트가 보고됩니다.



- 업데이트 날짜 범위: &nbsp; **2018-02-03**&nbsp; - &nbsp;**2018-04-28**
- *주제 영역:* &nbsp; **SQL Server Integration Services**.




&nbsp;

## <a name="new-articles-created-recently"></a>최근에 만든 새로운 문서

다음 링크는 최근에 추가된 새로운 문서로 이동합니다.


1. [SSIS(SQL Server Integration Services)를 통해 Excel에서 데이터 로드](load-data-to-from-excel-with-ssis.md)
2. [SSIS(SQL Server Integration Services)를 사용하여 SQL Server에서 Azure SQL Data Warehouse로 데이터 로드](load-data-to-sql-data-warehouse.md)
3. [SQL Server 장애 조치(failover) 클러스터 인스턴스를 통한 고가용성을 위한 Scale Out 지원](scale-out/scale-out-failover-cluster-instance.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>업데이트된 문서의 발췌 내용

이 섹션에는 최근에 많이 업데이트된 문서에서 발췌한 업데이트 내용이 표시됩니다.

여기에 표시된 발췌 내용은 적절한 의미 체계 맥락과 분리되어 표시됩니다. 또한 발췌 내용은 때때로 실제 문서에서 이 내용의 주변에 있는 중요한 markdown 구문과도 분리되어 표시됩니다. 따라서 이러한 발췌 내용은 일반적인 지침을 제공하기 위한 것입니다. 이 발췌 내용에서는 관심 내용을 클릭하여 실제 문서를 참조할 가치가 있을지 여부만 파악할 수 있습니다.

따라서 이러한 발췌 내용에서 코드를 복사하거나 발췌 내용을 정확한 사실로 간주하지 마세요. 대신 실제 문서를 참조하세요.





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>최근 업데이트된 문서의 간결한 목록

이 간결한 목록에는 발췌 섹션에 나열된 모든 업데이트된 문서로 연결되는 링크가 있습니다.

1. [Integration Services 설치](#TitleNum_1)
2. [Azure에서 SSIS 패키지 배포, 실행 및 모니터링](#TitleNum_2)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-install-integration-servicesinstall-windowsinstall-integration-servicesmd"></a>1. &nbsp; [Integration Services 설치](install-windows/install-integration-services.md)

*업데이트됨: 2018-04-25* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;([다음](#TitleNum_2))

<!-- Source markdown line 75.  ms.author= "douglasl".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 49551f3b1138f805e6d5e0f6099a100e2f3b3e7a 97caaafc1587b2326f4c357dd5eb21f2de7d358f  (PR=5676  ,  Filename=install-integration-services.md  ,  Dirpath=docs\integration-services\install-windows\  ,  MergeCommitSha40=a85a46312acf8b5a59a8a900310cf088369c4150) -->



**Integration Services 설치 완료**


*{Included-Content-Goes-Here}* 의 설치를 완료하려면 다음 목록에서 필요한 구성 요소를 선택합니다.

-   **Integration Services(SSIS)**. SQL Server 설치 마법사를 사용하여 SSIS를 설치합니다. SSIS를 선택하면 다음 항목이 설치됩니다.
    -   SQL Server 데이터베이스 엔진에서 SSIS 카탈로그 지원.
    -   필요에 따라, 마스터와 작업자로 구성되는 SSIS 규모 확장 기능.
    -   32비트 및 64비트 SSIS 구성 요소.
    -   SSIS를 설치해도 SSIS 패키지를 설계 및 개발하는 데 필요한 도구는 설치되지 **않습니다**.
-   **SQL Server 데이터베이스 엔진**. SQL Server 설치 마법사를 사용하여 데이터베이스 엔진을 설치합니다. 데이터베이스 엔진을 선택하면 SSIS 패키지를 저장, 관리, 실행 및 모니터링하는 SSIS 카탈로그 데이터베이스 `SSISDB`를 만들고 호스팅할 수 있습니다.
-   **SQL Server Data Tools(SSDT)**. SSDT를 다운로드하여 설치하려면 [SSDT(SQL Server Data Tools) 다운로드]를 참조하세요. SSDT를 설치하면 SSIS 패키지를 설계 및 배포할 수 있습니다. SSDT는 다음 항목을 설치합니다.
    -   SSIS 디자이너를 포함한 SSIS 패키지 디자인 및 개발 도구.
    -   32비트 SSIS 구성 요소만.
    -   제한된 버전의 Visual Studio(Visual Studio 버전이 아직 설치되지 않은 경우).
    -   SSIS 스크립트 태스크 및 스크립트 구성 요소에서 사용하는 스크립트 편집기인 VSTA(Visual Studio Tools for Applications).
    -   배포 마법사 및 패키지 업그레이드 마법사를 포함한 SSIS 마법사.
    -   SQL Server 가져오기 및 내보내기 마법사.
-   **Azure용 integration Services 기능 팩**. 기능 팩을 다운로드하여 설치하려면 [Azure용 Microsoft SQL Server 2017 Integration Services 기능 팩](https://www.microsoft.com/download/details.aspx?id=54798)을 참조하세요. 기능 팩을 설치하면 패키지에서 다음 서비스를 포함한 Azure 클라우드의 저장소 및 분석 서비스에 연결할 수 있습니다.



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-deploy-run-and-monitor-an-ssis-package-on-azurelift-shiftssis-azure-deploy-run-monitor-tutorialmd"></a>2. &nbsp; [Azure에서 SSIS 패키지 배포, 실행 및 모니터링](lift-shift/ssis-azure-deploy-run-monitor-tutorial.md)

*업데이트됨: 2018-04-25* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;([이전](#TitleNum_1))

<!-- Source markdown line 99.  ms.author= "douglasl".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 07f2b752818f2e786c4380fb822099190c59f302 54de9497353bac2d6a8a87e546fc6ab9e444a734  (PR=5676  ,  Filename=ssis-azure-deploy-run-monitor-tutorial.md  ,  Dirpath=docs\integration-services\lift-shift\  ,  MergeCommitSha40=a85a46312acf8b5a59a8a900310cf088369c4150) -->



**PowerShell을 사용하여 프로젝트 배포**


PowerShell을 사용하여 Azure SQL Database의 SSISDB에 프로젝트를 배포하려면 다음 스크립트를 요구 사항에 맞게 조정합니다. 이 스크립트는 `$ProjectFilePath` 아래의 자식 폴더와 각 자식 폴더의 프로젝트를 열거한 후 SSISDB에 동일한 폴더를 만들고 이러한 폴더에 프로젝트를 배포합니다.

이 스크립트를 실행하려면 스크립트를 실행하는 컴퓨터에 SQL Server Data Tools 버전 17.x 또는 SQL Server Management Studio가 설치되어 있어야 합니다.

```
**Variables**

$ProjectFilePath = "C:\<folder>"
$SSISDBServerEndpoint = "<servername>.database.windows.net"
$SSISDBServerAdminUserName = "<username>"
$SSISDBServerAdminPassword = "<password>"

**Load the IntegrationServices Assembly**

[System.Reflection.Assembly]::LoadWithPartialName("Microsoft.SqlServer.Management.IntegrationServices") | Out-Null;

**Store the IntegrationServices Assembly namespace to avoid typing it every time**

$ISNamespace = "Microsoft.SqlServer.Management.IntegrationServices"

Write-Host "Connecting to server ..."

**Create a connection to the server**

$sqlConnectionString = "Data Source=" + $SSISDBServerEndpoint + ";User ID="+ $SSISDBServerAdminUserName +";Password="+ $SSISDBServerAdminPassword + ";Initial Catalog=SSISDB"
$sqlConnection = New-Object System.Data.SqlClient.SqlConnection $sqlConnectionString

**Create the Integration Services object**

$integrationServices = New-Object $ISNamespace".IntegrationServices" $sqlConnection

**Get the catalog**

$catalog = $integrationServices.Catalogs['SSISDB']

write-host "Enumerating all folders..."

$folders = ls -Path $ProjectFilePath -Directory

if ($folders.Count -gt 0)
{
    foreach ($filefolder in $folders)
    {
        Write-Host "Creating Folder " $filefolder.Name " ..."

        # Create a new folder
        $folder = New-Object $ISNamespace".CatalogFolder" ($catalog, $filefolder.Name, "Folder description")
```







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

