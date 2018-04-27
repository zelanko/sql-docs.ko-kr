---
title: 업데이트-Linux 문서에서 SQL Server | Microsoft Docs
description: 가져온 조각을 Linux에서 Microsoft SQL server에서 최근에 변경된 된 설명서에 대 한 업데이트 된 콘텐츠를 표시 합니다.
manager: craigg
author: MightyPen
ms.author: genemi
ms.topic: article
ms.custom: sql-linux,UpdArt.exe
ms.suite: sql
ms.prod_service: sql
ms.component: ''
ms.date: 02/03/2018
ms.openlocfilehash: c277f51ddb50dfb9a5ef2bd23af7f6e80d00c25c
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
---
# <a name="new-and-recently-updated-sql-server-on-linux-docs"></a>신규 / 최근에 업데이트: Linux 문서에서 SQL Server



거의 매일 Microsoft 업데이트 기존 아티클 중 일부에 해당 [Docs.Microsoft.com](http://docs.microsoft.com/) 설명서 웹 사이트입니다. 이 문서에는 최근에 업데이트 된 문서에서 발췌 한 내용 표시 됩니다. 새 문서와 연결도 나열 되어 있습니다.

이 문서는 주기적으로 다시 실행 하는 프로그램에서 생성 됩니다. 경우에 따라 발췌 한 구문을 소스 문서에서 불완전 한 서식을 사용 하 여 또는 마크 다운으로 나타날 수 있습니다. 이미지는 여기에 표시 되지 않습니다.

다음 날짜 범위 및 주체에 대 한 최신 업데이트가 보고 됩니다.



- *업데이트 날짜 범위:*  &nbsp; **2017-12-03** &nbsp;부터 &nbsp; **2018-02-03**까지
- *주제 영역:* &nbsp; **Linux에서 Microsoft SQL Server**합니다.




&nbsp;

## <a name="new-articles-created-recently"></a>최근에 만든 새로운 기사

다음 링크는 최근에 추가된 새로운 문서로 이동합니다.


1. [다중 서브넷 Always On 가용성 그룹 및 장애 조치 클러스터 인스턴스 구성](sql-server-linux-configure-multiple-subnet.md)
2. [만들기 및 Linux에서 SQL Server에 대 한 가용성 그룹 구성](sql-server-linux-create-availability-group.md)
3. [Linux에서 SQL Server에 대 한 Pacemaker 클러스터 배포](sql-server-linux-deploy-pacemaker-cluster.md)
4. [Linux에서 SQL Server가 질문과 대답 (FAQ)](sql-server-linux-faq.md)
5. [Linux 배포에 대 한 SQL Server 가용성 기본 사항](sql-server-linux-ha-basics.md)
6. [고가용성을 위해 Kubernetes에서 SQL Server 컨테이너 구성](tutorial-sql-server-containers-kubernetes.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>부분 업데이트 되는 문서

이 섹션에는 최근에 많이 업데이트된 문서에서 발췌한 업데이트 내용이 표시됩니다.

여기에 표시 된 부분 적절 한 의미 체계 컨텍스트에서 분리 된 나타납니다. 또한 때로는 실제 문서의 주위에 있는 중요 한 마크 다운 구문에서 발췌 한 구문을 분리 됩니다. 따라서 이러한 발췌 한이 내용에 대 한 일반적인 지침만 됩니다. 발췌 한 내용 관심 분야를 클릭 하 고 실제 문서를 참조 하는 데 시간이 걸리는 보증 있는지 여부를 알 수 있습니다에 사용 합니다.

이러한 및 기타 이유로 이러한 부분에서 코드를 복사 하지 않으려면 및 사용 하지 않습니다 정확한 진리도 모든 텍스트 발췌문 합니다. 대신 실제 문서를 참조 합니다.





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>Compact를 최근에 업데이트 하는 문서 목록

이 간결한 목록에는 발췌 섹션에 나열된 모든 업데이트된 문서로 연결되는 링크가 있습니다.

1. [Always On Linux에서 가용성 그룹](#TitleNum_1)
2. [추출, 변환 및 SSIS와 Linux에서 데이터 로드](#TitleNum_2)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-always-on-availability-groups-on-linuxsql-server-linux-availability-group-overviewmd"></a>1. &nbsp;[Always On Linux에서 가용성 그룹](sql-server-linux-availability-group-overview.md)

*업데이트 됨된: 2018-01-31* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([다음](#TitleNum_2))

<!-- Source markdown line 85.  ms.author= mikeray.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 85685bc8ad3528aa26ca3f2bba7b0112808ad6f9 51aff6e55104c8f775d2b4f4461e44f689a9ee6b  (PR=4768  ,  Filename=sql-server-linux-availability-group-overview.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=d4d880dd9c247d1e7fb7a728d5231bc9ac61c989) -->



다음 조건이 충족 되 면 AG의 자동 장애 조치 된 있습니다.

-   주 복제본과 보조 복제본은 동기 데이터 이동으로 설정 됩니다.
-   보조 동기화 (동기화 하지 않는) 동일한 데이터 요소에서 두 가지 의미의 상태를 있습니다.
-   클러스터 유형 외부로 설정 됩니다. 자동 장애 조치 none 클러스터 유형 수는 없습니다.
-   `sequence_number` 되도록 보조 복제본의 주에 시퀀스 번호가 가장 높은 – 즉, 보조 복제본의 `sequence_number` 원래 주 복제본에서 것과 일치 합니다.

이러한 조건이 충족 될 경우 주 복제본을 호스팅하는 서버 오류가 발생 하면 AG 동기 복제본 소유권을 변경 됩니다. 동기 복제본에 대 한 동작 (있는 있을 수 3의 총: 하나의 주 파일 그룹 및 두 개의 보조 복제본)를 통해 추가로 제어할 수 `required_synchronized_secondaries_to_commit`합니다. 이 Windows와 Linux 모두에서 Ag와 작동 하지만 완전히 다른 방식으로 구성 됩니다. Linux에서 값 자체 AG 리소스에서 클러스터에 의해 자동으로 구성 됩니다.

**구성 가능한 및 쿼럼**


또한 새 SQL Server 2017 CU1 당시에 구성 으로만 이동 가능한 복제본이입니다. Pacemaker WSFC 다르기 때문에 쿼럼 및 STONITH를 요구 하는 경우에 특히 더 2 노드 구성을 방금 작동 하지 않습니다 AG에 관한. FCI에 대 한 클러스터 계층에서 발생 하는 모든 FCI 장애 조치 중재 하기 때문에 Pacemaker에서 제공 하는 쿼럼 메커니즘 괜찮아 수 있습니다. AG에 대 한 linux 중재 모든 메타 데이터가 저장 된 SQL Server에서 발생 합니다. 구성 전용 복제에 발생 하는 위치입니다.

다른 항목 없이 세 번째 노드 및 동기화 된 복제본이 하나 이상 필요한 것입니다. 이 적용 되지 않는 SQL Server Standard 있으므로 두 개의 복제본 AG의 참여를 하나만 사용할 수 있습니다. 구성 전용 복제본 AG 구성의 다른 복제본과 동일 master 데이터베이스에서 AG 구성을 저장합니다. 구성 전용 복제본 AG에 참여 하는 사용자 데이터베이스는 수 없습니다. 구성 데이터는 주 데이터베이스에서 동기적으로 전송 됩니다. 이 구성 데이터가 든 상관 없이 자동 또는 수동 장애 조치 하는 동안 사용 됩니다.



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-extract-transform-and-load-data-on-linux-with-ssissql-server-linux-migrate-ssismd"></a>2. &nbsp;[추출, 변환 및 SSIS와 Linux에서 데이터 로드](sql-server-linux-migrate-ssis.md)

*업데이트 됨된: 2018-01-31* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([이전](#TitleNum_1))

<!-- Source markdown line 50.  ms.author= lle.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 9bba002ae3955ebb8376c7c85b7ec1ac8c706073 1533a8e0bfe553e5404de79129119b3f93185ee9  (PR=4768  ,  Filename=sql-server-linux-migrate-ssis.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=d4d880dd9c247d1e7fb7a728d5231bc9ac61c989) -->



    ```
    SSIS_PACKAGE_DECRYPT=test /opt/ssis/bin/dtexec /f package.dtsx
    ```

2.  지정 된 `/de[crypt]` 암호를 대화형으로 다음 예제와 같이 입력 하는 옵션:

    ```
    /opt/ssis/bin/dtexec /f package.dtsx /de

    Enter decryption password:
    ```

3.  지정 된 `/de` 다음 예제와 같이 명령줄에서 암호를 제공 하는 옵션입니다. 이 메서드는 명령 기록에서 명령 사용 하 여 암호 해독 암호를 저장 하기 때문에 권장 되지 않습니다.

    ```
    opt/ssis/bin/dtexec /f package.dtsx /de test

    Warning: Using /De[crypt] <password> may store decryption password in command history.

    You can use /De[crypt] instead to enter interactive mode,
    or use environment variable SSIS_PACKAGE_DECRYPT to set decryption password.
    ```

**패키지 디자인**


**ODBC 데이터 원본에 연결**합니다. 이상 Linux CTP 2.1 새로 고침에서 SSIS, SSIS 패키지는 Linux 기반 ODBC 연결 사용할 수 있습니다. 이 기능은 SQL Server 및 MySQL ODBC 드라이버와 함께 테스트 되었습니다 하지만 또한 ODBC 사양을 따르는 모든 유니코드 ODBC 드라이버와 함께 사용 해야 합니다. 디자인 타임에 ODBC 데이터;에 연결 하는 DSN 또는 연결 문자열 중 하나를 제공할 수 있습니다. 또한 Windows 인증을 사용할 수 있습니다. 자세한 내용은 참조는 [블로그 게시물 Linux ODBC 지원 발표](https://blogs.msdn.microsoft.com/ssis/2017/06/16/odbc-is-supported-in-ssis-on-linux-ssis-helsinki-ctp2-1-refresh/)합니다.







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
- [새로 추가되었거나 업데이트됨(1+1):&nbsp; **SQL Operations Studio** 문서](../sql-operations-studio/new-updated-sql-operations-studio.md)
- [새로 추가되었거나 업데이트됨(1+1):&nbsp; **Microsoft SQL Server** 문서](../sql-server/new-updated-sql-server.md)
- [새로 추가되었거나 업데이트됨(0+1):&nbsp; **SSDT(SQL Server Data Tools)** 문서](../ssdt/new-updated-ssdt.md)
- [새로 추가되었거나 업데이트됨(1+2):&nbsp; **SSMS(SQL Server Management Studio)** 문서](../ssms/new-updated-ssms.md)
- [새로 추가되었거나 업데이트됨(0+2):&nbsp; **Transact-SQL** 문서](../t-sql/new-updated-t-sql.md)



#### <a name="subject-areas-that-do-not-have-any-new-or-recently-updated-articles"></a>새로 추가되었거나 최근에 업데이트된 문서가 *없는* 주제 영역


- [새로 추가되었거나 업데이트됨(0+0): **SQL용 DMA(Data Migration Assistant)** 문서](../dma/new-updated-dma.md)
- [새 + 업데이트 (0 + 0): **ADO ActiveX Data Objects ()에 대 한 SQL** docs](../ado/new-updated-ado.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 Analysis Services** 문서](../analysis-services/new-updated-analysis-services.md)
- [새 + 업데이트 (0 + 0): **SQL에 대 한 데이터 품질 서비스** docs](../data-quality-services/new-updated-data-quality-services.md)
- [새 + 업데이트 (0 + 0): **확장 DMX (Data Mining) sql** docs](../dmx/new-updated-dmx.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 MDS(Master Data Services)** 문서](../master-data-services/new-updated-master-data-services.md)
- [새 + 업데이트 (0 + 0): **MDX (Multidimensional Expressions)에 대 한 SQL** docs](../mdx/new-updated-mdx.md)
- [새 + 업데이트 (0 + 0): **SQL에 대 한 ODBC (Open Database Connectivity)** docs](../odbc/new-updated-odbc.md)
- [새 + 업데이트 (0 + 0): **SQL에 대 한 샘플** docs](../samples/new-updated-samples.md)
- [새 + 업데이트 (0 + 0): **SQL Server Migration Assistant (SSMA)** docs](../ssma/new-updated-ssma.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 도구** 문서](../tools/new-updated-tools.md)
- [새 + 업데이트 (0 + 0): **SQL에 대 한 XQuery** docs](../xquery/new-updated-xquery.md)


