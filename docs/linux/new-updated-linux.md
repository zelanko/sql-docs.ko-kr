---
title: 업데이트-Linux 문서에서 SQL Server | Microsoft Docs
description: 가져온 조각을 Linux에서 Microsoft SQL server에서 최근에 변경된 된 설명서에 대 한 업데이트 된 콘텐츠를 표시 합니다.
manager: craigg
author: MightyPen
ms.author: genemi
ms.topic: article
ms.custom: UpdArt.exe
ms.suite: sql
ms.technology: release-landing
ms.prod: sql
ms.prod_service: sql-non-specified
ms.component: linux
ms.date: 04/28/2018
ms.openlocfilehash: adc9b9d4dec86f1b0e8807869aa0f20532837cea
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="new-and-recently-updated-sql-server-on-linux-docs"></a>신규 / 최근에 업데이트: Linux 문서에서 SQL Server



거의 매일 Microsoft 업데이트 기존 아티클 중 일부에 해당 [Docs.Microsoft.com](http://docs.microsoft.com/) 설명서 웹 사이트입니다. 이 문서에는 최근에 업데이트 된 문서에서 발췌 한 내용 표시 됩니다. 새 문서와 연결도 나열 되어 있습니다.

이 문서는 주기적으로 다시 실행 하는 프로그램에서 생성 됩니다. 경우에 따라 발췌 한 구문을 소스 문서에서 불완전 한 서식을 사용 하 여 또는 마크 다운으로 나타날 수 있습니다. 이미지는 여기에 표시 되지 않습니다.

다음 날짜 범위 및 주체에 대 한 최신 업데이트가 보고 됩니다.



- *날짜 범위 업데이트:* &nbsp; **2018-02-03** &nbsp; 을 아래와 같이 &nbsp; **2018-04-28**
- *주제 영역:* &nbsp; **Linux에서 Microsoft SQL Server**합니다.




&nbsp;

## <a name="new-articles-created-recently"></a>최근에 만든 새로운 기사

다음 링크는 최근에 추가된 새로운 문서로 이동합니다.


1. [Linux에서 SQL Server 용 active Directory 인증](sql-server-linux-active-directory-auth-overview.md)
2. [구성 SQL Server Always On 가용성 그룹에 Windows 및 Linux (플랫폼 간)](sql-server-linux-availability-group-cross-platform.md)
3. [Linux에서 가용성 그룹에 대해 항상 작동](sql-server-linux-availability-group-operate-ha.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>부분 업데이트 되는 문서

이 섹션에는 최근에 많이 업데이트된 문서에서 발췌한 업데이트 내용이 표시됩니다.

여기에 표시 된 부분 적절 한 의미 체계 컨텍스트에서 분리 된 나타납니다. 또한 때로는 실제 문서의 주위에 있는 중요 한 마크 다운 구문에서 발췌 한 구문을 분리 됩니다. 따라서 이러한 발췌 한이 내용에 대 한 일반적인 지침만 됩니다. 발췌 한 내용 관심 분야를 클릭 하 고 실제 문서를 참조 하는 데 시간이 걸리는 보증 있는지 여부를 알 수 있습니다에 사용 합니다.

이러한 및 기타 이유로 이러한 부분에서 코드를 복사 하지 않으려면 및 사용 하지 않습니다 정확한 진리도 모든 텍스트 발췌문 합니다. 대신 실제 문서를 참조 합니다.





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>Compact를 최근에 업데이트 하는 문서 목록

이 간결한 목록에는 발췌 섹션에 나열된 모든 업데이트된 문서로 연결되는 링크가 있습니다.

1. [설치 및 Linux에서 SQL Server 업그레이드에 대 한 저장소를 구성 합니다.](#TitleNum_1)
2. [Mssql conf 도구와 함께 Linux에서 SQL Server 구성](#TitleNum_2)
3. [SQL Server 2017 linux에 대 한 릴리스 정보](#TitleNum_3)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-configure-repositories-for-installing-and-upgrading-sql-server-on-linuxsql-server-linux-change-repomd"></a>1. &nbsp; [설치 및 Linux에서 SQL Server 업그레이드에 대 한 저장소를 구성 합니다.](sql-server-linux-change-repo.md)

*업데이트 됨된: 2018-04-25* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([다음](#TitleNum_2))

<!-- Source markdown line 72.  ms.author= jroth.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 b5ccaa0fcb8895f25c162e4e0494ad4872773de3 29a959be6ee7d58fe0c53e8f91bdd282fb2e6d29  (PR=5676  ,  Filename=sql-server-linux-change-repo.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=a85a46312acf8b5a59a8a900310cf088369c4150) -->



- 파일의 내용을 출력 합니다.

```
   sudo cat /etc/yum.repos.d/mssql-server.repo
```

- **이름** 속성은 구성된 저장소입니다. 이 문서의 [저장소] 섹션의 표를 식별할 수 있습니다.

**이전 리포지토리 (RHEL)를 제거 합니다.**

필요한 경우 다음 명령 사용 하 여 이전 저장소를 제거 합니다.

```
sudo rm -rf /etc/yum.repos.d/mssql-server.repo
```

이 명령에서는 이전 섹션에서 식별 된 파일 이름이 **mssql server.repo**합니다.

**새 저장소 (RHEL) 구성**

SQL Server 설치 및 업그레이드에 사용할 새 저장소를 구성 합니다. 사용자가 선택한 저장소를 구성 하려면 다음 명령 중 하나를 사용 합니다.

| 리포지토리 | Command |
|---|---|
| **CU** | `sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2017.repo` |
| **GDR** | `sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2017-gdr.repo` |

**<a id="sles"></a> SLES 저장소 구성**

SLES에서 저장소를 구성 하려면 다음 단계를 사용 합니다.

**이전에 구성 된 저장소 (SLES)에 대 한 확인**

먼저 SQL Server 저장소 이미 등록 하는지 여부를 확인 합니다.

- 사용 하 여 **zypper 정보** 는 이전에 구성 된 저장소에 대 한 정보를 얻을 수 있습니다.

```
   sudo zypper info mssql-server
```

- **리포지토리** 속성은 구성된 저장소입니다. 이 문서의 [저장소] 섹션의 표를 식별할 수 있습니다.

**이전 리포지토리 (SLES)를 제거 합니다.**

필요한 경우 이전 저장소를 제거 합니다. 이전에 구성 된 저장소 형식에 따라 다음 명령 중 하나를 사용 합니다.

| 리포지토리 | 제거 하려면 명령 |
|---|---|
| **미리 보기** | `sudo zypper removerepo 'packages-microsoft-com-mssql-server'` |



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-configure-sql-server-on-linux-with-the-mssql-conf-toolsql-server-linux-configure-mssql-confmd"></a>2. &nbsp; [Mssql conf 도구와 함께 Linux에서 SQL Server 구성](sql-server-linux-configure-mssql-conf.md)

*업데이트 됨된: 2018-04-25* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([이전](#TitleNum_1) | [다음](#TitleNum_3))

<!-- Source markdown line 151.  ms.author= jroth.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 3664c4d64ea4840dcbc718461ed04403cc486f30 89f708af45ce262057e967e9047f1328e19248ba  (PR=5676  ,  Filename=sql-server-linux-configure-mssql-conf.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=a85a46312acf8b5a59a8a900310cf088369c4150) -->




**<a id="masterdatabasedir"></a> 기본 master 데이터베이스 파일 디렉터리 위치를 변경 합니다.**


**filelocation.masterdatafile** 및 **filelocation.masterlogfile** 변경 master 데이터베이스 파일에 대 한 SQL Server 엔진을 찾는 위치 위치를 설정 합니다. 기본적으로이 위치는 /var/opt/mssql/data는입니다.

이러한 설정을 변경 하려면 다음 단계를 사용 합니다.

- 새 오류 로그 파일에 대 한 대상 디렉터리를 만듭니다. 다음 예제에서는 새 **/tmp/masterdatabasedir** 디렉터리:

```
   sudo mkdir /tmp/masterdatabasedir
```

- 소유자 및 그룹 디렉터리의 변경 된 **mssql** 사용자:

```
   sudo chown mssql /tmp/masterdatabasedir
   sudo chgrp mssql /tmp/masterdatabasedir
```

- Mssql conf를 사용 하 여 사용 하 여 마스터 데이터 및 로그 파일에 대 한 기본 master 데이터베이스 디렉터리를 변경 하는 **설정** 명령:

```
   sudo /opt/mssql/bin/mssql-conf set filelocation.masterdatafile /tmp/masterdatabasedir/master.mdf
   sudo /opt/mssql/bin/mssql-conf set filelocation.masterlogfile /tmp/masterdatabasedir/mastlog.ldf
```

- SQL Server 서비스를 중지 합니다.

```
   sudo systemctl stop mssql-server
```

- Master.mdf 및 masterlog.ldf 이동 합니다.

```
   sudo mv /var/opt/mssql/data/master.mdf /tmp/masterdatabasedir/master.mdf
   sudo mv /var/opt/mssql/data/mastlog.ldf /tmp/masterdatabasedir/mastlog.ldf
```

- SQL Server 서비스를 시작 합니다.

```
   sudo systemctl start mssql-server
```

> [!NOTE]
> SQL Server는 지정된 된 디렉터리에서 master.mdf 및 mastlog.ldf 파일을 찾을 수 없으면, 시스템 데이터베이스의 템플릿 기반 복사본 자동으로 지정된 된 디렉터리에서 만들어지고 SQL Server 성공적으로 시작 됩니다. 그러나 새 master 데이터베이스에서 사용자 데이터베이스, 서버 로그인, 서버 인증서, 암호화 키, SQL 에이전트 작업 또는 이전 SA 로그인 암호와 같은 메타 데이터 업데이트 되지 않습니다. SQL Server를 중지 하 고 이전 master.mdf 및 mastlog.ldf 지정 된 새 위치로 이동할 기존 메타 데이터를 사용 하 여 계속 하려면 SQL Server를 시작 해야 합니다.



&nbsp;

&nbsp;

---

<a name="TitleNum_3"/>

### <a name="3-nbsp-release-notes-for-sql-server-2017-on-linuxsql-server-linux-release-notesmd"></a>3. &nbsp; [SQL Server 2017 linux에 대 한 릴리스 정보](sql-server-linux-release-notes.md)

*업데이트 됨된: 2018-04-25* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([이전](#TitleNum_2))

<!-- Source markdown line 64.  ms.author= jroth.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 367d112a9427bbdd18e0e52cc82264dd169c91ae 63a67be08fa39ece778cf9ca0b9746dd28694574  (PR=5676  ,  Filename=sql-server-linux-release-notes.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=a85a46312acf8b5a59a8a900310cf088369c4150) -->



- [SQL Server 에이전트 사용]

**<a id="CU6"></a> Cu6 적용 (2018 년 4 월)**


이 SQL Server 2017의 누적 업데이트 6 (cu6)가 적용 릴리스입니다. 이 릴리스에 대 한 SQL Server 엔진 버전 14.0.3025.34입니다. 수정 사항 및이 릴리스에서 향상 된 기능에 대 한 정보를 참조 하십시오. [ https://support.microsoft.com/help/4101464 ](https://support.microsoft.com/help/4101464)합니다.

**패키지 세부 정보**


수동 또는 오프 라인 패키지 설치의 경우 다음 표의 정보를 사용 하 여 RPM 및 Debian 패키지를 다운로드할 수 있습니다.

| 패키지 | 패키지 버전 | 다운로드 |
|-----|-----|-----|
| Red Hat RPM 패키지 | 14.0.3025.34-3 | [엔진 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3025.34-3.x86_64.rpm)</br>[높은 가용성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3025.34-3.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3025.34-3.x86_64.rpm)</br>[SSIS 패키지](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) |
| SLES RPM 패키지 | 14.0.3025.34-3 | [mssql 서버 엔진 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3025.34-3.x86_64.rpm)</br>[높은 가용성 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3025.34-3.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3025.34-3.x86_64.rpm) |
| Ubuntu 16.04 Debian 패키지 | 14.0.3025.34-3 | [엔진 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3025.34-3_amd64.deb)</br>[높은 가용성 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3025.34-3_amd64.deb)</br>[전체 텍스트 검색 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3025.34-3_amd64.deb)<br/>[SSIS 패키지](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |







## <a name="similar-articles-about-new-or-updated-articles"></a>신규 문서 또는 업데이트된 문서에 대한 유사 문서

이 섹션에는 공용 GitHub.com 리포지토리 내의 다른 주제 영역에서 최근에 업데이트된 문서와 유사한 문서가 나와 있습니다. [MicrosoftDocs/sql-docs](https://github.com/MicrosoftDocs/sql-docs/)



#### <a name="subject-areas-that-do-have-new-or-recently-updated-articles"></a>새로 추가되었거나 최근에 업데이트된 문서가 *있는* 주제 영역

- [새 + 업데이트 (11 + 6): &nbsp; &nbsp; **SQL에 대 한 고급 분석** docs](../advanced-analytics/new-updated-advanced-analytics.md)
- [새 + 업데이트 (18 + 0): &nbsp; &nbsp; **SQL에 대 한 Analysis Services** docs](../analysis-services/new-updated-analysis-services.md)
- [새 + 업데이트 (218 + 14): **SQL에 연결** docs](../connect/new-updated-connect.md)
- [새 + 업데이트 (14 + 0): &nbsp; &nbsp; **SQL에 대 한 데이터베이스 엔진** docs](../database-engine/new-updated-database-engine.md)
- [새 + 업데이트 (3 + 2): &nbsp; &nbsp; **sql Integration Services** docs](../integration-services/new-updated-integration-services.md)
- [새 + 업데이트 (3 + 3): &nbsp; &nbsp; **SQL에 대 한 Linux** docs](../linux/new-updated-linux.md)
- [새 + 업데이트 (7 + 10): &nbsp; &nbsp; **SQL에 대 한 관계형 데이터베이스** docs](../relational-databases/new-updated-relational-databases.md)
- [새 + 업데이트 (0 + 2): &nbsp; &nbsp; **sql Reporting Services** docs](../reporting-services/new-updated-reporting-services.md)
- [새 + 업데이트 (1 + 3): &nbsp; &nbsp; **SQL 작업 Studio** docs](../sql-operations-studio/new-updated-sql-operations-studio.md)
- [새 + 업데이트 (2 + 3): &nbsp; &nbsp; **Microsoft SQL Server** docs](../sql-server/new-updated-sql-server.md)
- [새 + 업데이트 (1 + 1): &nbsp; &nbsp; **SQL Server Data Tools (SSDT)** docs](../ssdt/new-updated-ssdt.md)
- [새 + 업데이트 (5 + 2): &nbsp; &nbsp; **SQL Server Management Studio (SSMS)** docs](../ssms/new-updated-ssms.md)
- [새 + 업데이트 (0 + 2): &nbsp; &nbsp; **TRANSACT-SQL** docs](../t-sql/new-updated-t-sql.md)
- [새 + 업데이트 (1 + 1): &nbsp; &nbsp; **SQL에 대 한 도구** docs](../tools/new-updated-tools.md)



#### <a name="subject-areas-that-do-not-have-any-new-or-recently-updated-articles"></a>새로 추가되었거나 최근에 업데이트된 문서가 *없는* 주제 영역

- [새 + 업데이트 (0 + 0): **SQL에 대 한 분석 플랫폼 시스템** docs](../analytics-platform-system/new-updated-analytics-platform-system.md)
- [새 + 업데이트 (0 + 0): **SQL에 대 한 데이터 품질 서비스** docs](../data-quality-services/new-updated-data-quality-services.md)
- [새 + 업데이트 (0 + 0): **확장 DMX (Data Mining) sql** docs](../dmx/new-updated-dmx.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 MDS(Master Data Services)** 문서](../master-data-services/new-updated-master-data-services.md)
- [새 + 업데이트 (0 + 0): **MDX (Multidimensional Expressions)에 대 한 SQL** docs](../mdx/new-updated-mdx.md)
- [새 + 업데이트 (0 + 0): **SQL에 대 한 ODBC (Open Database Connectivity)** docs](../odbc/new-updated-odbc.md)
- [새 + 업데이트 (0 + 0): **SQL에 대 한 PowerShell** docs](../powershell/new-updated-powershell.md)
- [새 + 업데이트 (0 + 0): **SQL에 대 한 샘플** docs](../samples/new-updated-samples.md)
- [새 + 업데이트 (0 + 0): **SQL Server Migration Assistant (SSMA)** docs](../ssma/new-updated-ssma.md)
- [새 + 업데이트 (0 + 0): **SQL에 대 한 XQuery** docs](../xquery/new-updated-xquery.md)

