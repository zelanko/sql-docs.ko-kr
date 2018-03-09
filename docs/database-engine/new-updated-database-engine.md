---
title: "업데이트됨 - 데이터베이스 엔진 설명서 | Microsoft Docs"
description: "데이터베이스 엔진 설명서에서 최근에 변경되어 업데이트된 내용 중에서 발췌한 부분을 표시합니다."
manager: craigg
author: MightyPen
ms.author: genemi
ms.topic: article
ms.custom: UpdArt.exe
ms.suite: sql
ms.prod_service: sql-non-specified
ms.component: database-engine
ms.date: 02/03/2018
ms.openlocfilehash: d01d9fa13342709a74d98033d093d9856ab5d680
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/09/2018
---
# <a name="new-and-recently-updated-database-engine-docs"></a>신규 및 최근 업데이트: 데이터베이스 엔진 설명서



Microsoft에서는 거의 매일 [Docs.Microsoft.com](http://docs.microsoft.com/) 설명서 웹 사이트에서 기존 문서 일부를 업데이트합니다. 이 문서에는 최근 업데이트된 문서에서 발췌한 내용이 표시됩니다. 새 문서로 연결되는 링크도 나열될 수 있습니다.

이 문서는 주기적으로 다시 실행되는 프로그램에 의해 생성됩니다. 경우에 따라 발췌한 내용의 형식이 완전하지 않거나 원본 문서의 표식(markdown)으로 표시될 수 있습니다. 이미지는 여기에 표시되지 않습니다.

다음 날짜 범위 및 주제에 대한 최근 업데이트가 보고됩니다.



- *업데이트 날짜 범위:*  &nbsp; **2017-12-03** &nbsp;부터 &nbsp; **2018-02-03**까지
- *주제 영역:* &nbsp; **데이터베이스 엔진**




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

1. [Always On 가용성 그룹 복제본 인스턴스 업그레이드](#TitleNum_1)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-upgrading-always-on-availability-group-replica-instancesavailability-groupswindowsupgrading-always-on-availability-group-replica-instancesmd"></a>1. &nbsp; [Always On 가용성 그룹 복제본 인스턴스 업그레이드](availability-groups/windows/upgrading-always-on-availability-group-replica-instances.md)

*업데이트됨: 2018-01-29* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; 

<!-- Source markdown line 174.  ms.author= "mikeray".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 20ca282e8965889a7a530fb67e125cc876410e41 9f27d0f9a74333b291c1cdc1529edc13960fae29  (PR=4741  ,  Filename=upgrading-always-on-availability-group-replica-instances.md  ,  Dirpath=docs\database-engine\availability-groups\windows\  ,  MergeCommitSha40=0a44ce9993ebf61f86e409255a1d58d47993951a) -->



**변경 데이터 캡처 또는 복제를 위한 특별한 단계**


적용하는 업데이트에 따라 변경 데이터 캡처 또는 복제가 활성화된 AG 복제본 데이터베이스에 추가 단계가 필요할 수 있습니다. 업데이트에 대한 릴리스 정보를 참조하여 다음 단계가 필요한지 확인하세요.

1. 각 보조 복제본을 업그레이드합니다.

1. 모든 보조 복제본이 업그레이드된 후 AG를 업그레이드된 인스턴스로 장애 조치(failover)합니다.

1. 주 복제본을 호스트하는 인스턴스에서 다음 Transact-SQL을 실행합니다.

   ```
   EXECUTE [master].[sys].[sp_vupgrade_replication];
   ```

   >[!NOTE]
   >이 명령을 실행하는 데 몇 분 정도 걸릴 수 있습니다.

1. 원래 주 복제본이었던 인스턴스를 업그레이드합니다.

자세한 내용은 [최신 CU로 업그레이드한 후 CDC 기능이 중단될 수 있음](http://blogs.msdn.microsoft.com/sql_server_team/cdc-functionality-may-break-after-upgrading-to-the-latest-cu-for-sql-server-2012-2014-and-2016/)을 참조하세요.









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
- [새로 추가되었거나 업데이트됨(1+1):&nbsp; **SQL 작업 Studio** 문서](../sql-operations-studio/new-updated-sql-operations-studio.md)
- [새로 추가되었거나 업데이트됨(1+1):&nbsp; **Microsoft SQL Server** 문서](../sql-server/new-updated-sql-server.md)
- [새로 추가되었거나 업데이트됨(0+1):&nbsp; **SSDT(SQL Server Data Tools)** 문서](../ssdt/new-updated-ssdt.md)
- [새로 추가되었거나 업데이트됨(1+2):&nbsp; **SSMS(SQL Server Management Studio)** 문서](../ssms/new-updated-ssms.md)
- [새로 추가되었거나 업데이트됨(0+2):&nbsp; **Transact-SQL** 문서](../t-sql/new-updated-t-sql.md)



#### <a name="subject-areas-that-do-not-have-any-new-or-recently-updated-articles"></a>새로 추가되었거나 최근에 업데이트된 문서가 *없는* 주제 영역


- [새로 추가되었거나 업데이트됨(0+0): **SQL용 DMA(Data Migration Assistant)** 문서](../dma/new-updated-dma.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 ADO(ActiveX Data Objects)** 문서](../ado/new-updated-ado.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 Analysis Services** 문서](../analysis-services/new-updated-analysis-services.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 Data Quality Services** 문서](../data-quality-services/new-updated-data-quality-services.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 DMX(Data Mining Extension)** 문서](../dmx/new-updated-dmx.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 MDS(Master Data Services)** 문서](../master-data-services/new-updated-master-data-services.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 MDX(Multidimensional Expression)** 문서](../mdx/new-updated-mdx.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 ODBC(Open Database Connectivity)** 문서](../odbc/new-updated-odbc.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 샘플** 문서](../sample/new-updated-sample.md)
- [새로 추가되었거나 업데이트됨(0+0): **SSMA(SQL Server Migration Assistant)** 문서](../ssma/new-updated-ssma.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 도구** 문서](../tools/new-updated-tools.md)
- [새로 추가되었거나 업데이트됨(0+0): **SQL용 XQuery** 문서](../xquery/new-updated-xquery.md)


