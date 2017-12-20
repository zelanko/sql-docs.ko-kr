---
title: "업데이트된 기능 - SQL Server Integration Services 문서 | Microsoft Docs"
description: "Microsoft SQL Server Integration Services 설명서에서 최근에 변경되어 업데이트된 내용의 코드 조각을 표시합니다."
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
ms.date: 12/02/2017
ms.author: genemi
ms.workload: integration-services
ms.openlocfilehash: 9660fa7239c14c3adc963cc75ceb98de8316734c
ms.sourcegitcommit: 29265ad41fbe3326c21c6908ec4275a3a38f1c09
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/04/2017
---
# <a name="new-and-recently-updated-integration-services-for-sql-server"></a>새로운 기능 및 최근에 업데이트된 기능: SQL Server Integration Services



Microsoft에서는 거의 매일 [Docs.Microsoft.com](http://docs.microsoft.com/) 설명서 웹 사이트에서 기존 문서 일부를 업데이트합니다. 이 문서에는 최근 업데이트된 문서에서 발췌한 내용이 표시됩니다. 새 문서로 연결되는 링크도 나열될 수 있습니다.

이 문서는 주기적으로 다시 실행되는 프로그램에 의해 생성됩니다. 경우에 따라 발췌한 내용의 형식이 완전하지 않거나 원본 문서의 표식(markdown)으로 표시될 수 있습니다. 이미지는 여기에 표시되지 않습니다.

다음 날짜 범위 및 주제에 대한 최근 업데이트가 보고됩니다.



- *업데이트 날짜 범위:*  &nbsp; **2017-09-28** &nbsp;부터 &nbsp; **2017-12-02**
- *주제 영역:* &nbsp; **SQL Server Integration Services**.




&nbsp;

## <a name="new-articles-created-recently"></a>최근에 만든 새로운 문서

다음 링크는 최근에 추가된 새로운 문서로 이동합니다.


1. [SSIS로 온-프레미스 및 Azure에서 파일 공유의 파일 저장 및 검색](lift-shift/ssis-azure-files-file-shares.md)
2. [Azure에 배포된 SSIS 패키지 유효성 검사](lift-shift/ssis-azure-validate-packages.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>업데이트된 문서의 발췌 내용

이 섹션에는 최근에 많이 업데이트된 문서에서 발췌한 업데이트 내용이 표시됩니다.

여기에 표시된 발췌 내용은 적절한 의미 체계 맥락과 분리되어 표시됩니다. 또한 발췌 내용은 때때로 실제 문서에서 이 내용의 주변에 있는 중요한 markdown 구문과도 분리되어 표시됩니다. 따라서 이러한 발췌 내용은 일반적인 지침을 제공하기 위한 것입니다. 이 발췌 내용에서는 관심 내용을 클릭하여 실제 문서를 참조할 가치가 있을지 여부만 파악할 수 있습니다.

따라서 이러한 발췌 내용에서 코드를 복사하거나 발췌 내용을 정확한 사실로 간주하지 마세요. 대신 실제 문서를 참조하세요.





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>최근 업데이트된 문서의 간결한 목록

이 간결한 목록에는 발췌 섹션에 나열된 모든 업데이트된 문서로 연결되는 링크가 있습니다.

1. [Hadoop 연결 관리자](#TitleNum_1)
2. [Windows 인증으로 온-프레미스 데이터 원본 및 Azure 파일 공유에 연결](#TitleNum_2)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-hadoop-connection-managerconnection-managerhadoop-connection-managermd"></a>1. &nbsp; [Hadoop 연결 관리자](connection-manager/hadoop-connection-manager.md)

*업데이트됨: 2017-11-28* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;([다음](#TitleNum_2))

<!-- Source markdown line 65.  ms.author= "douglasl".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 2d68f4e884304f1a28045b42b680c15cc6a41ec5 fb2429466ea4d545682975d8dbea47451ce98ec7  (PR=4113  ,  Filename=hadoop-connection-manager.md  ,  Dirpath=docs\integration-services\connection-manager\  ,  MergeCommitSha40=28cccac53767db70763e5e705b8cc59a83c77317) -->



**Kerberos 인증을 사용하여 연결**

Hadoop 연결 관리자에 Kerberos 인증을 사용할 수 있도록 온-프레미스 환경을 설정하는 옵션은 두 가지이며, 상황에 더 적합한 옵션을 선택하면 됩니다.
-   옵션 1: [Kerberos 영역에 SSIS 컴퓨터 조인--#kerberos-join-realm)
-   옵션 2: [Windows 도메인과 Kerberos 영역 간의 상호 신뢰 사용--#kerberos-mutual-trust)

**<a name="kerberos-join-realm"></a>옵션 1: Kerberos 영역에 SSIS 컴퓨터 조인**


**요구 사항:**


-   게이트웨이 컴퓨터가 Kerberos 영역을 조인해야 하며 Windows 도메인은 조인할 수 없습니다.

**구성 방법:**


**SSIS 컴퓨터에서 다음을 수행합니다.**

1.  **Ksetup** 유틸리티를 실행하여 Kerberos 키 서버 및 영역을 구성합니다.

    Kerberos 영역은 Windows 도메인과 다르므로 컴퓨터가 작업 그룹의 구성원으로 구성되어 있어야 합니다. 다음 예제와 같이 Kerberos 영역을 설정하고 KDC 서버를 추가합니다. 필요에 따라 *REALM.COM*을 해당하는 고유한 영역으로 바꿉니다.

```
    C:> Ksetup /setdomain REALM.COM`
    C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>
```

    Restart the computer after executing these two commands.

2.  **Ksetup** 명령으로 구성을 확인합니다. 출력이 다음 샘플과 같아야 합니다.

```
    C:> Ksetup
    default realm = REALM.COM (external)
    REALM.com:
        kdc = <your_kdc_server_address>
```

**<a name="kerberos-mutual-trust"></a>옵션 2: Windows 도메인과 Kerberos 영역 간의 상호 신뢰 사용**


**요구 사항:**

-   게이트웨이 컴퓨터가 Windows 도메인을 조인해야 합니다.
-   도메인 컨트롤러의 설정을 업데이트할 수 있는 권한이 필요합니다.

**구성 방법:**


> [!NOTE]
> 필요에 따라 다음 자습서의 REALM.COM 및 AD.COM을 해당하는 고유한 영역 및 도메인 컨트롤러로 바꿉니다.



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-connect-to-on-premises-data-sources-and-azure-file-shares-with-windows-authenticationlift-shiftssis-azure-connect-with-windows-authmd"></a>2. &nbsp; [Windows 인증으로 온-프레미스 데이터 원본 및 Azure 파일 공유에 연결](lift-shift/ssis-azure-connect-with-windows-auth.md)

*업데이트됨: 2017-11-27* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;([이전](#TitleNum_1))

<!-- Source markdown line 66.  ms.author= "douglasl".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 673386fca53cb60b983e0cb3cd4b9e2ee1dee0de 65458b4dceb92d01184c5e9c6f68ec0e8f16ba08  (PR=4104  ,  Filename=ssis-azure-connect-with-windows-auth.md  ,  Dirpath=docs\integration-services\lift-shift\  ,  MergeCommitSha40=19e1c4067142d33e8485cb903a7a9beb7d894015) -->



**온-프레미스 SQL Server에 연결**

온-프레미스 SQL Server에 연결할 수 있는지 확인하려면 다음을 수행합니다.

1.  이 테스트를 실행하려면 도메인에 가입되지 않은 컴퓨터를 찾습니다.

2.  도메인에 가입하지 않은 컴퓨터에서 다음 명령을 실행하여, 사용할 도메인 자격 증명으로 SSMS(SQL Server Management Studio)를 시작합니다.

```
    runas.exe /netonly /user:<domain>\<username> SSMS.exe
```

3.  SSMS에서 사용할 온-프레미스 SQL Server에 연결할 수 있는지 확인합니다.

**온-프레미스 파일 공유에 연결**

온-프레미스 파일 공유에 연결할 수 있는지 확인하려면 다음을 수행합니다.

1.  이 테스트를 실행하려면 도메인에 가입되지 않은 컴퓨터를 찾습니다.

2.  도메인에 가입하지 않은 컴퓨터에서 다음 명령을 실행합니다. 이 명령은 사용할 도메인 자격 증명이 있는 명령 프롬프트 창을 연 다음 디렉터리 목록을 가져 와서 파일 공유에 대한 연결을 테스트합니다.

```
    runas.exe /netonly /user:<domain>\<username> cmd.exe
    dir \\fileshare
```

3.  사용할 온-프레미스 파일 공유에 대한 디렉터리 목록이 반환되는지 확인합니다.

**Azure VM의 파일 공유에 연결**

Azure 가상 머신의 파일 공유에 연결하려면 다음을 수행합니다.

1.  SSMS(SQL Server Management Studio) 또는 다른 도구를 사용하여 SSISDB(SSIS Catalog database)를 호스트하는 SQL Database에 연결합니다.

2.  SSISDB를 현재 데이터베이스로 사용하여 쿼리 창을 엽니다.

3.  다음 옵션의 설명에 따라 `catalog.set_execution_credential` 저장 프로시저를 실행합니다.

```
    catalog.set_execution_credential @domain = N'.', @user = N'username of local account on Azure virtual machine', @password = N'password'
```

**Azure 파일의 파일 공유에 연결**

Azure Files에 대한 자세한 내용은 [Azure Files](https://azure.microsoft.com/services/storage/files/)를 참조하세요.







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


