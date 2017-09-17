---
title: "업데이트-Linux 문서에서 SQL Server | Microsoft Docs"
description: "가져온 조각을 Linux에서 Microsoft SQL server에서 최근에 변경된 된 설명서에 대 한 업데이트 된 콘텐츠를 표시 합니다."
services: na
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: rothja
ms.service: na
ms.topic: updart-autogen
ms.technology: database-engine
ms.custom: UpdArt.exe
ms.workload: linux-sql
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 09/11/2017
ms.author: genemi
ms.translationtype: MT
ms.sourcegitcommit: 15080827744c19120a8474f3142004c4af7a4064
ms.openlocfilehash: 9e6b139e45ccb5184255eabedfb0f809ff64fd2b
ms.contentlocale: ko-kr
ms.lasthandoff: 09/13/2017

---
# <a name="new-and-recently-updated-sql-server-on-linux-docs"></a>신규 / 최근에 업데이트: Linux 문서에서 SQL Server



Microsoft에서는 거의 매일 [Docs.Microsoft.com](http://docs.microsoft.com/) 설명서 웹 사이트에서 기존 문서 일부를 업데이트합니다. 이 문서에는 최근 업데이트된 문서에서 발췌한 내용이 표시됩니다. 새 문서로 연결되는 링크도 나열될 수 있습니다.

이 문서는 주기적으로 다시 실행되는 프로그램에 의해 생성됩니다. 경우에 따라 발췌한 내용의 형식이 완전하지 않거나 원본 문서의 표식(markdown)으로 표시될 수 있습니다. 이미지는 여기에 표시되지 않습니다.

다음 날짜 범위 및 주제에 대한 최근 업데이트가 보고됩니다.



- *날짜 범위 업데이트:* &nbsp; **2017-07-18** &nbsp; 을 아래와 같이 &nbsp; **2017-09-11**
- *주제 영역:* &nbsp; **Linux에서 Microsoft SQL Server**합니다.




&nbsp;

## <a name="new-articles-created-recently"></a>최근에 만든 새로운 문서

다음 링크는 최근에 추가 된 새 문서를 이동 합니다.


1. [DB 메일 및 Linux에서 SQL 에이전트와 전자 메일 알림](sql-server-linux-db-mail-sql-agent.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>업데이트된 문서의 발췌 내용

이 섹션에는 최근에 대규모 업데이트 발견 된 문서에서 수집 하는 업데이트의 발췌 한 내용 표시 됩니다.

여기에 표시된 발췌 내용은 적절한 의미 체계 맥락과 분리되어 표시됩니다. 또한 발췌 내용은 때때로 실제 문서에서 이 내용의 주변에 있는 중요한 markdown 구문과도 분리되어 표시됩니다. 따라서 이러한 발췌 내용은 일반적인 지침을 제공하기 위한 것입니다. 이 발췌 내용에서는 관심 내용을 클릭하여 실제 문서를 참조할 가치가 있을지 여부만 파악할 수 있습니다.

따라서 이러한 발췌 내용에서 코드를 복사하거나 발췌 내용을 정확한 사실로 간주하지 마세요. 대신 실제 문서를 참조하세요.





&nbsp;

<a name="compactupdatedlist"/>

## <a name="compact-list-of-articles-updated-recently"></a>최근 업데이트된 문서의 간결한 목록

이 compact 목록 발췌 한 내용 섹션에 나열 된 모든 업데이트 된 문서에 대 한 링크를 제공 합니다.

1. [Linux에서 SQL Server에 대 한 HA 가용성 그룹 동작](#TitleNum_1)
2. [Docker에서 SQL Server 2017 컨테이너 이미지를 구성 합니다.](#TitleNum_2)
3. [Mssql conf 도구와 함께 Linux에서 SQL Server 구성](#TitleNum_3)
4. [Linux에서 SQL Server에 대 한 고객 의견](#TitleNum_4)
5. [Linux 백업 및 복원을 사용 하 여 Windows에서 SQL Server 데이터베이스 마이그레이션](#TitleNum_5)
6. [SQL Server 2017 linux에 대 한 릴리스 정보](#TitleNum_6)
7. [Linux에서 SQL Server에 대 한 설치 지침](#TitleNum_7)
8. [Linux에서 SQL Server Integration Services (SSIS)를 설치 합니다.](#TitleNum_8)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-operate-ha-availability-group-for-sql-server-on-linuxsql-server-linux-availability-group-failover-hamd"></a>1. &nbsp;[작동 HA 가용성 그룹 Linux에서 SQL Server에 대 한](sql-server-linux-availability-group-failover-ha.md)

*업데이트 됨된: 2017-08-24* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([다음](#TitleNum_2))

<!-- Source markdown line 167.  ms.author= mikeray.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 1bef3ece125721b041aa2b9d836329736377df8d 669d2b9a614d680b98280d5b522ba82cf466536c  (PR=2948  ,  Filename=sql-server-linux-availability-group-failover-ha.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=7b8c23474aee48e6d34ba268bc8942bc1c0263d3) -->



**가용성 그룹을 업그레이드**


가용성 그룹을 업그레이드 하기 전에 검토 [업그레이드 가용성 그룹 복제본 인스턴스-..에서 모범 사례 / database-engine/availability-groups/windows/upgrading-always-on-availability-group-replica-instances.md).

다음 섹션에서는 Linux에서 가용성 그룹이 포함 된 SQL Server 인스턴스에서 롤링 업그레이드를 수행 하는 방법을 설명 합니다.

**Linux에서 업그레이드 단계**


Linux에서 SQL Server의 인스턴스에서 가용성 그룹 복제본을 가용성 그룹의 클러스터 유형 중 하나는 `EXTERNAL` 또는 `NONE`합니다. 이외에 Windows Server 장애 조치 클러스터 (WSFC)는 클러스터 관리자에서 관리 되는 가용성 그룹 `EXTERNAL`합니다. Corosync와 pacemaker는 외부 클러스터 관리자의 예시입니다. 클러스터 관리자가 없습니다 포함 된 가용성 그룹에 클러스터 형식이 `NONE` 여기에 설명 된 업그레이드 단계는 클러스터 유형의 가용성 그룹에 대 한 특정 `EXTERNAL` 또는 `NONE`합니다.

1. 시작 하기 전에 각 데이터베이스를 백업 합니다.
2. 보조 복제본을 호스팅하는 SQL Server의 인스턴스를 업그레이드 합니다.

    a. 비동기 보조 복제본을 먼저 업그레이드 합니다.

    b. 동기 보조 복제본을 업그레이드 합니다.

   >[!NOTE]
   >가용성 그룹에 있는 비동기 데이터 손실을 방지 하기 위해 복제본-하나의 복제본을 동기 변경한 동기화 될 때까지 기다립니다. 이 복제를 업그레이드 합니다.

   b.1 합니다. 업그레이드에 대 한 대상 보조 복제본을 호스팅하는 노드의에 리소스를 중지 합니다.

   업그레이드 명령을 실행 하기 전에 클러스터 모니터링은 되 불필요 하 게 실패 하지 하도록 리소스를 중지 합니다. 다음 예제에서는 중지 될 리소스에 취소할 수 있는 노드의 위치 제약 조건을 추가 합니다. 업데이트 `ag_cluster-master` 리소스 이름으로 및 `nodeName1` 노드를 복제본을 호스팅하는 업그레이드에 대 한 대상으로 합니다.

```
   pcs constraint location ag_cluster-master avoids nodeName1
```



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-configure-sql-server-2017-container-images-on-dockersql-server-linux-configure-dockermd"></a>2. &nbsp;[Docker에 SQL Server 2017 구성 컨테이너 이미지](sql-server-linux-configure-docker.md)

*업데이트 됨된: 2017-09-05* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([이전](#TitleNum_1) | [다음](#TitleNum_3))

<!-- Source markdown line 257.  ms.author= jroth.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 0239ed55a23721eedcc0407a0886d08da47c975b 108fe230151cff7dc91fcdc22218f232394746ec  (PR=3050  ,  Filename=sql-server-linux-configure-docker.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=60272ce672c0a32738b0084ea86f8907ec7fc0a5) -->



1. Docker 식별 **태그** 사용 하려는 릴리스에 대 한 합니다. 사용 가능한 태그를 보려면 참조 [mssql-서버-linux Docker 허브 페이지](https://hub.docker.com/r/microsoft/mssql-server-linux/tags/)합니다.

1. 태그와 SQL Server 컨테이너 이미지를 끌어옵니다. 예를 들어 대체 RC1 이미지를 끌어오려면 `<image_tag>` 다음 명령에 `rc1`합니다.

```
   docker pull microsoft/mssql-server-linux:<image_tag>
```

1. 새 컨테이너 이미지를 실행 하려면에 태그 이름을 지정는 `docker run` 명령입니다. 다음 명령에서 `<image_tag>` 실행 하려는 버전입니다.

```
   docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1401:1433 -d microsoft/mssql-server-linux:<image_tag>
```

```
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1401:1433 -d microsoft/mssql-server-linux:<image_tag>
```

이러한 단계는 기존 컨테이너를 다운 그레이드 하 데도 사용할 수 있습니다. 예를 들어 rollback을 하거나 문제를 해결 하거나 테스트에 대 한 실행 중인 컨테이너를 다운 그레이드할 수 있습니다. 실행 중인 컨테이너를 다운 그레이드 하려면 사용 해야 하는 지 속성 기술 데이터 폴더에 대 한 합니다. 에 설명 된 동일한 단계에서 [섹션-#upgrade)를 업그레이드 하지만 새 컨테이너를 실행 하면 이전 버전의 태그 이름을 지정 합니다.

> [!IMPORTANT]



&nbsp;

&nbsp;

---

<a name="TitleNum_3"/>

### <a name="3-nbsp-configure-sql-server-on-linux-with-the-mssql-conf-toolsql-server-linux-configure-mssql-confmd"></a>3. &nbsp;[Mssql conf 도구와 함께 Linux에서 SQL Server 구성](sql-server-linux-configure-mssql-conf.md)

*업데이트 됨된: 2017-09-05* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([이전](#TitleNum_2) | [다음](#TitleNum_4))

<!-- Source markdown line 233.  ms.author= lbosq.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 6117f03e9617b70077488d86f94b32537c4cb9e8 4247a749c056037dd71a27121525be04be6a4f21  (PR=3042  ,  Filename=sql-server-linux-configure-mssql-conf.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=46b16dcf147dbd863eec0330e87511b4ced6c4ce) -->



**<a id="localaudit"></a>로컬 감사 디렉터리 설정**


**telemetry.userrequestedlocalauditdirectory** 설정은 로컬 감사를 활성화 하 고 로컬 감사를 기록 하는 디렉터리 설정할 있습니다 만들어집니다.

1. 새 로컬 감사 로그에 대 한 대상 디렉터리를 만듭니다. 다음 예제에서는 새 **/tmp/감사** 디렉터리:

```
   sudo mkdir /tmp/audit
```

1. 소유자 및 그룹 디렉터리의 변경 된 **mssql** 사용자:

```
   sudo chown mssql /tmp/audit
   sudo chgrp mssql /tmp/audit
```

1. 루트 및 mssql conf 스크립트를 실행 하는 중는 **설정** 명령을 **telemetry.userrequestedlocalauditdirectory**:

```
   sudo /opt/mssql/bin/mssql-conf set telemetry.userrequestedlocalauditdirectory /tmp/audit
```

1. SQL Server 서비스를 다시 시작 합니다.

```
   sudo systemctl restart mssql-server
```

자세한 내용은 [Linux--sql-server-linux-customer-feedback.md에서 SQL Server에 대 한 고객 의견)을 참조 하십시오.

**<a id="lcid"></a>SQL Server 로캘을 변경합니다**


**language.lcid** 설정 변경 내용을 SQL Server 로캘을 지원 되는 언어 식별자 (LCID)입니다.

1. 다음 예에서는 프랑스어로 로캘을 변경 (1036):

```
   sudo /opt/mssql/bin/mssql-conf set language.lcid 1036
```

1. 변경 내용을 적용 하려면 SQL Server 서비스를 다시 시작 합니다.

```
   sudo systemctl restart mssql-server
```

**<a id="memorylimit"></a>메모리 제한을 설정합니다**


**memory.memorylimitmb** 컨트롤 실제 메모리 양을 mb 단위로 사용할 수 있는 SQL Server에 설정 합니다. 기본값은 실제 메모리의 80%입니다.

1. 루트 및 mssql conf 스크립트를 실행 하는 중는 **설정** 명령을 **memory.memorylimitmb**합니다. 다음 예제에서는 SQL server 3.25 GB (3328 MB)에 사용할 수 있는 메모리를 변경합니다.

```
   sudo /opt/mssql/bin/mssql-conf set memory.memorylimitmb 3328
```

1. 변경 내용을 적용 하려면 SQL Server 서비스를 다시 시작 합니다.



&nbsp;

&nbsp;

---

<a name="TitleNum_4"/>

### <a name="4-nbsp-customer-feedback-for-sql-server-on-linuxsql-server-linux-customer-feedbackmd"></a>4. &nbsp;[Linux에서 SQL Server에 대 한 고객 의견](sql-server-linux-customer-feedback.md)

*업데이트 됨된: 2017-08-24* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([이전](#TitleNum_3) | [다음](#TitleNum_5))

<!-- Source markdown line 104.  ms.author= anshrest.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 9d8122e864804004d91f6b7c5c3d24c4a4114d34 7316ef831c390a854c324f23a02c3fb6005e2fea  (PR=2948  ,  Filename=sql-server-linux-customer-feedback.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=7b8c23474aee48e6d34ba268bc8942bc1c0263d3) -->




**Docker에서**

Docker에서 로컬 감사를 사용 하도록 설정 하려면 Docker 있어야 [프로그램 data--sql-server-linux-configure-docker.md 유지).

1. 새 로컬 감사 로그에 대 한 대상 디렉터리는 컨테이너에 있게 됩니다. 컴퓨터에 호스트 디렉터리에서 새 로컬 감사 로그에 대 한 대상 디렉터리를 만듭니다. 다음 예제에서는 새 **감사/** 디렉터리:

```
   sudo mkdir <host directory>/audit
```


1. 추가 `mssql.conf` 줄이 포함 된 파일 `[telemetry]` 및 `userrequestedlocalauditdirectory = <host directory>/audit` 호스트 디렉터리에 있습니다.

```
   echo '[telemetry]' >> <host directory>/mssql.conf
```

```
   echo 'userrequestedlocalauditdirectory = <host directory>/audit' >> <host directory>/mssql.conf
```
2. 컨테이너 이미지를 실행 합니다.
```
   docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' --cap-add SYS_PTRACE -p 1433:1433 -v <host directory>:/var/opt/mssql -d microsoft/mssql-server-linux
```

```
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" --cap-add SYS_PTRACE -p 1433:1433 -v <host directory>:/var/opt/mssql -d microsoft/mssql-server-linux
```

**다음 단계**





&nbsp;

&nbsp;

---

<a name="TitleNum_5"/>

### <a name="5-nbsp-migrate-a-sql-server-database-from-windows-to-linux-using-backup-and-restoresql-server-linux-migrate-restore-databasemd"></a>5. &nbsp;[Linux 백업과 복원을 사용 하 여 Windows에서 SQL Server 데이터베이스 마이그레이션](sql-server-linux-migrate-restore-database.md)

*업데이트 됨된: 2017-08-24* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([이전](#TitleNum_4) | [다음](#TitleNum_6))

<!-- Source markdown line 30.  ms.author= mikeray.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 e78f5516a46eab834f644979d3e1c0ca415fabcd 6b03a01385078290b9f451ac013b628f53e0e8b4  (PR=2948  ,  Filename=sql-server-linux-migrate-restore-database.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=7b8c23474aee48e6d34ba268bc8942bc1c0263d3) -->



* 다음으로 Windows 컴퓨터:
  * [SQL Server](https://www.microsoft.com/sql-server/sql-server-2016-editions) 설치 합니다.
  * [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) 설치 합니다.
  * 마이그레이션할 대상 데이터베이스입니다.

* 다음을 설치 된 Linux 컴퓨터:
  * SQL Server 2017 RC2 합니다. 에 대 한 설치 퀵 스타트를 참조 하십시오. [RHEL--quickstart-install-connect-red-hat.md), [SLES-빠른 시작-설치-연결-suse.md), 또는 [Ubuntu-빠른 시작-설치-연결-ubuntu.md).
  * SQL Server 2017 RC2 [명령줄 tools--sql-server-linux-setup-tools.md).

**Windows에서 백업을 만들기**


여러 가지 방법으로 Windows에서 데이터베이스의 백업 파일을 만듭니다. 다음 단계에서는 SQL Server Management Studio (SSMS)를 사용 합니다.

1. 시작 **SQL Server Management Studio** Windows 컴퓨터에 있습니다.

1. 연결 대화 상자에 입력 **localhost**합니다.

1. 개체 탐색기에서 확장 **데이터베이스**합니다.



&nbsp;

&nbsp;

---

<a name="TitleNum_6"/>

### <a name="6-nbsp-release-notes-for-sql-server-2017-on-linuxsql-server-linux-release-notesmd"></a>6. &nbsp;[SQL Server 2017 linux에 대 한 릴리스 정보](sql-server-linux-release-notes.md)

*업데이트 됨된: 2017-08-23* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([이전](#TitleNum_5) | [다음](#TitleNum_7))

<!-- Source markdown line 31.  ms.author= jroth.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 4c8b9876f4792782314ba2f9b246405fb8036f84 acb97cf0a2e0bdd039575eaab9c41003316cbb02  (PR=2939  ,  Filename=sql-server-linux-release-notes.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=91098c850b0f6affb8e4831325d0f18fd163d71a) -->



**<a id="RC2"></a>RC2 (2017 년 8 월)**


이 릴리스에 대 한 SQL Server 엔진 버전 14.0.900.75입니다.

**지원 되는 플랫폼**


| 플랫폼 | 파일 시스템 | 설치 가이드 |
|-----|-----|-----|
| Red Hat Enterprise Linux 7.3 워크스테이션, 서버 및 데스크톱 | XFS 또는 EXT4 | [설치 guide--quickstart-install-connect-red-hat.md) |
| SUSE Enterprise Linux Server v12 SP2 | EXT4 | [설치 가이드-빠른 시작-설치-연결-suse.md) |
| Ubuntu 16.04LTS | EXT4 | [설치 가이드-빠른 시작-설치-연결-ubuntu.md) |
| Docker 엔진 1.8 + Windows, Mac 또는 Linux에 | 해당 사항 없음 | [설치 가이드-빠른 시작-설치-연결-docker.md) |

> [!NOTE]
> 최소 3.25 g B 메모리 Linux에서 SQL Server를 실행 해야 합니다.
> SQL Server 엔진 되었습니다.이 이번에 1.5 t B의 메모리를 테스트 합니다.

**패키지 세부 정보**


패키지 세부 정보 및 RPM 및 Debian 패키지에 대 한 다운로드 위치는 다음 표에 나열 됩니다. 참고는 다음과 같은 설치 가이드의 단계를 사용 하는 경우 이러한 패키지를 직접 다운로드할 필요가 없습니다.

- [SQL Server 패키지-sql server-linux setup.md 설치)
- [전체 텍스트 검색 package--sql-server-linux-setup-full-text-search.md 설치)
- [SQL Server 에이전트 package--sql-server-linux-setup-sql-agent.md 설치)

| 패키지 | 패키지 버전 | 다운로드 |
|-----|-----|-----|
| Red Hat RPM 패키지 | 14.0.900.75-1 | [엔진 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-14.0.900.75-1.x86_64.rpm)</br>[높은 가용성 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-ha-14.0.900.75-1.x86_64.rpm)</br>[전체 텍스트 검색 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-fts-14.0.900.75-1.x86_64.rpm)</br>[SQL Server 에이전트 RPM 패키지](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-agent-14.0.900.75-1.x86_64.rpm) |



&nbsp;

&nbsp;

---

<a name="TitleNum_7"/>

### <a name="7-nbsp-installation-guidance-for-sql-server-on-linuxsql-server-linux-setupmd"></a>7. &nbsp;[Linux에서 SQL Server에 대 한 설치 지침](sql-server-linux-setup.md)

*업데이트 됨된: 2017-08-28* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([이전](#TitleNum_6) | [다음](#TitleNum_8))

<!-- Source markdown line 70.  ms.author= jroth.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 00394e1733568a55243788d828968ff9b58a3c99 8ba2bf6f9cf4b5f54a6ee0f4d16d4437d5724880  (PR=2971  ,  Filename=sql-server-linux-setup.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=303d3b74da3fe370d19b7602c0e11e67b63191e7) -->



**<a id="rollback"></a>SQL Server 롤백**


롤백 또는 SQL Server 이전 버전으로 다운 그레이드 하려면 다음 단계를 사용 합니다.

1. 으로 다운 그레이드 하려면 SQL Server 패키지에 대 한 버전 번호를 식별 합니다. 목록이 패키지 번호에 대 한 참조 [릴리스 notes--sql-server-linux-release-notes.md).

1. SQL Server의 이전 버전으로 다운 그레이드 합니다. 다음 명령에서 대체 `<version_number>` 을 1 단계에서 식별 된 SQL Server 버전 번호입니다.

   | 플랫폼 | 패키지 업데이트 명령 |
   |-----|-----|
   | RHEL | `sudo yum downgrade mssql-server-<version_number>.x86_64` |
   | SLES | `sudo zypper install --oldpackage mssql-server=<version_number>` |
   | Ubuntu | `sudo apt-get install mssql-server=<version_number>`<br/>`sudo systemctl start mssql-server` |

> [!NOTE]
> SQL Server 2017 같은 같은 주 버전 내에서 릴리스를 다운 그레이드 하 에서만 지원 됩니다.

> [!IMPORTANT]
> 다운 그레이드이 이번에 간의 RC2 및 r c 1만 지원 됩니다.




&nbsp;

&nbsp;

---

<a name="TitleNum_8"/>

### <a name="8-nbsp-install-sql-server-integration-services-ssis-on-linuxsql-server-linux-setup-ssismd"></a>8. &nbsp;[Linux에 SQL Server Integration Services (SSIS)를 설치 합니다.](sql-server-linux-setup-ssis.md)

*업데이트 됨된: 2017-08-24* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([이전](#TitleNum_7))

<!-- Source markdown line 66.  ms.author= lle.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 a3fecd2553d1b25406445b8a26b22c9015dd98fe f836d560513fef1217e7dbce0ab85f78eec6f937  (PR=2948  ,  Filename=sql-server-linux-setup-ssis.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=7b8c23474aee48e6d34ba268bc8942bc1c0263d3) -->



이미 있는 경우 `mssql-server-is` 있습니다 다음 명령 사용 하 여 최신 버전으로 업데이트할 수 설치 합니다.

```
sudo apt-get install mssql-server-is
```


제거 하려면 `mssql-server-is`, 다음 명령을 실행할 수 있습니다.
```
sudo apt-get remove msssql-server-is
```



**<a name="RHEL"></a>RHEL에 SSIS를 설치 합니다.**

설치 하는 `mssql-server-is` RHEL에 패키지에서 다음이 단계를 수행 합니다.


1.  Superuser 모드를 입력 합니다.

```
    sudo su
```


2.  Microsoft SQL Server Red Hat 저장소 구성 파일을 다운로드 합니다.

```
    curl https://packages.microsoft.com/config/rhel/7/mssql-server.repo > /etc/yum.repos.d/mssql-server.repo
```


3.  Superuser 모드를 종료 합니다.

```
    exit
```


4.  SQL Server Integration Services를 설치 하려면 다음 명령을 실행 합니다.

```
    sudo yum install -y mssql-server-is
```


5.  설치 후 실행 하십시오 `ssis-conf`합니다.







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



