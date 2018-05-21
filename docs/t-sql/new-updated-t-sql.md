---
title: 업데이트됨 - T-SQL 문서 | Microsoft Docs
description: Transact-SQL의 설명서에서 최근에 변경된 업데이트된 콘텐츠의 일부를 표시합니다.
manager: craigg
author: MightyPen
ms.author: genemi
ms.topic: article
ms.custom: UpdArt.exe
ms.suite: sql
ms.technology: release-landing
ms.prod: sql
ms.prod_service: sql-non-specified
ms.component: t-sql
ms.date: 04/28/2018
ms.openlocfilehash: b1bc891bf7edc4cd82c38c8d647c279828190298
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="new-and-recently-updated-transact-sql-docs"></a>새로 추가되었거나 최근에 업데이트됨: Transact-SQL 문서



Microsoft에서는 거의 매일 [Docs.Microsoft.com](http://docs.microsoft.com/) 설명서 웹 사이트에서 기존 문서 일부를 업데이트합니다. 이 문서에는 최근 업데이트된 문서에서 발췌한 내용이 표시됩니다. 새 문서로 연결되는 링크도 나열될 수 있습니다.

이 문서는 주기적으로 다시 실행되는 프로그램에 의해 생성됩니다. 경우에 따라 발췌한 내용의 형식이 완전하지 않거나 원본 문서의 표식(markdown)으로 표시될 수 있습니다. 이미지는 여기에 표시되지 않습니다.

다음 날짜 범위 및 주제에 대한 최근 업데이트가 보고됩니다.



- 업데이트 날짜 범위: &nbsp; **2018-02-03**&nbsp; - &nbsp;**2018-04-28**
- *주제 영역:* &nbsp; **T-SQL**




&nbsp;

## <a name="new-articles-created-recently"></a>최근에 만든 새로운 문서

다음 링크는 최근에 추가된 새로운 문서로 이동합니다.


***지금은 나열할 새 문서가 없습니다.***



&nbsp;

## <a name="updated-articles-with-excerpts"></a>업데이트된 문서의 발췌 내용

이 섹션에는 최근에 많이 업데이트된 문서에서 발췌한 업데이트 내용이 표시됩니다.

여기에 표시된 발췌 내용은 적절한 의미 체계 맥락과 분리되어 표시됩니다. 또한 발췌 내용은 때때로 실제 문서에서 이 내용의 주변에 있는 중요한 markdown 구문과도 분리되어 표시됩니다. 따라서 이러한 발췌 내용은 일반적인 지침을 제공하기 위한 것입니다. 이 발췌 내용에서는 관심 내용을 클릭하여 실제 문서를 참조할 가치가 있을지 여부만 파악할 수 있습니다.

따라서 이러한 발췌 내용에서 코드를 복사하거나 발췌 내용을 정확한 사실로 간주하지 마세요. 대신 실제 문서를 참조하세요.





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>최근 업데이트된 문서의 간결한 목록

이 간결한 목록에는 발췌 섹션에 나열된 모든 업데이트된 문서로 연결되는 링크가 있습니다.

1. [ALTER DATABASE SCOPED CONFIGURATION(Transact-SQL)](#TitleNum_1)
2. [RESTORE 문(Transact-SQL)](#TitleNum_2)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-alter-database-scoped-configuration-transact-sqlstatementsalter-database-scoped-configuration-transact-sqlmd"></a>1. &nbsp; [ALTER DATABASE SCOPED CONFIGURATION(Transact-SQL)](statements/alter-database-scoped-configuration-transact-sql.md)

*업데이트됨: 2018-04-13* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;([다음](#TitleNum_2))

<!-- Source markdown line 150.  ms.author= "carlrab".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 f6833910b664d0059a9073589807b195052325b3 bf969f123b22e6ebc650380a6905156f26ed6ca6  (PR=0  ,  Filename=alter-database-scoped-configuration-transact-sql.md  ,  Dirpath=docs\t-sql\statements\  ,  MergeCommitSha40=f70f24bff1677b33c661abd13726f491ce32b305) -->



XTP_PROCEDURE_EXECUTION_STATISTICS  **=** { ON | **OFF** }

**적용 대상**: *{Included-Content-Goes-Here}*

현재 데이터베이스에 있는 고유하게 컴파일된 T-SQL 모듈에 대한 모듈 수준 실행 통계 수집을 활성화하거나 비활성화합니다. 기본값은 OFF입니다. 실행 통계는 [sys.dm_exec_procedure_stats]에 반영됩니다.

고유하게 컴파일된 T-SQL 모듈에 대한 모듈 수준 실행 통계는 이 옵션이 켜져 있거나 통계 수집이 [sp_xtp_control_proc_exec_stats]를 통해 활성화된 경우 수집됩니다.

XTP_QUERY_EXECUTION_STATISTICS  **=** { ON | **OFF** }

**적용 대상**: *{Included-Content-Goes-Here}*

현재 데이터베이스에 있는 고유하게 컴파일된 T-SQL 모듈에 대한 명령문 수준 실행 통계 수집을 활성화하거나 비활성화합니다. 기본값은 OFF입니다. 실행 통계는 [sys.dm_exec_query_stats] 및 [쿼리 저장소]에 반영됩니다.

고유하게 컴파일된 T-SQL 모듈에 대한 명령문 수준 실행 통계는 이 옵션이 켜져 있거나 통계 수집이 [sp_xtp_control_query_exec_stats]를 통해 활성화된 경우 수집됩니다.

고유하게 컴파일된 T-SQL 모듈의 성능 모니터링에 대한 자세한 내용은 [고유하게 컴파일된 저장 프로시저의 성능 모니터링]을 참조하세요.



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-restore-statements-transact-sqlstatementsrestore-statements-transact-sqlmd"></a>2. &nbsp; [RESTORE 문(Transact-SQL)](statements/restore-statements-transact-sql.md)

*업데이트됨: 2018-04-13* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;([이전](#TitleNum_1))

<!-- Source markdown line 339.  ms.author= "barbkess".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 2902efb58bb964d3e9a0660956690d37f0397c00 36186a7cffd26ffa54a83e383ffd752dbc568a4d  (PR=0  ,  Filename=restore-statements-transact-sql.md  ,  Dirpath=docs\t-sql\statements\  ,  MergeCommitSha40=f70f24bff1677b33c661abd13726f491ce32b305) -->



**일반적인 주의 사항 - SQL Database 관리되는 인스턴스**


비동기 복원의 경우 클라이언트 연결을 중단하는 경우에도 복원은 계속됩니다. 사용자 연결을 드롭하는 경우 복원 작업의 상태에 대한 [sys.dm_operation_status] 보기를 확인할 수 있습니다(데이터베이스의 CREATE 및 DROP 경우 포함).

다음 데이터베이스 옵션은 설정/재정의되며 나중에 변경할 수 없습니다.

- NEW_BROKER(broker가 .bak 파일에서 활성화되지 않은 경우)
- ENABLE_BROKER(broker가 .bak 파일에서 활성화되지 않은 경우)
- AUTO_CLOSE=OFF(.bak 파일의 데이터베이스에 AUTO_CLOSE=ON이 있는 경우)
- RECOVERY FULL(.bak 파일의 데이터베이스에 SIMPLE 또는 BULK_LOGGED 복구 모드가 있는 경우)
- 메모리에 최적화된 파일 그룹이 추가되고 원본 .bak 파일에 없는 경우 XTP를 호출합니다. 모든 기존 메모리에 최적화된 파일 그룹은 XTP로 이름이 변경됩니다.
- SINGLE_USER 및 RESTRICTED_USER 옵션은 MULTI_USER로 변환됩니다.

**제한 사항 - SQL Database 관리되는 인스턴스**

다음과 같은 제한이 적용됩니다.

- 여러 백업 세트를 포함하는 .BAK 파일은 복원할 수 없습니다.
- 여러 로그 파일을 포함하는 .BAK 파일은 복원할 수 없습니다.
- .bak에 FILESTREAM 데이터가 포함된 경우 복원이 실패합니다.
- 활성 메모리 내 개체가 있는 데이터베이스를 포함하는 백업은 현재 복원할 수 없습니다.
- 어느 지점에 메모리 내 개체가 있는 데이터베이스를 포함하는 백업은 현재 복원할 수 없습니다.
- 읽기 전용 모드인 데이터베이스를 포함하는 백업은 현재 복원할 수 없습니다. 이 제한 사항은 곧 삭제될 예정입니다.

자세한 내용은 [관리되는 인스턴스] 참조







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

