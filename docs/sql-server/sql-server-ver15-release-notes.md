---
title: SQL Server 2019 릴리스 정보 | Microsoft Docs
ms.custom: ''
ms.date: 09/24/2018
ms.prod: sql-server-2018
ms.reviewer: ''
ms.technology:
- server-general
ms.topic: article
ms.assetid: 13942af8-5a40-4cef-80f5-918386767a47
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: = sql-server-ver15 || = sqlallproducts-allversions
ms.openlocfilehash: c1c65ad5e2fc495479ec7801b779b242677c1c96
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47717593"
---
# <a name="sql-server-2019-preview-release-notes"></a>SQL Server 2019 미리 보기 릴리스 정보

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

이 문서에서는 [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP(Community Technology Preview) 릴리스의 제한 사항 및 알려진 문제에 대해 설명합니다. 관련 내용은 다음을 참조하세요.
- [SQL Server 2019의 새로운 기능](../sql-server/what-s-new-in-sql-server-ver15.md)

> [!NOTE]
> [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 미리 보기 릴리스는 예정된 릴리스의 기능을 체험할 수 있도록 하기 위해 제공됩니다. 프로덕션 용도로 지원되거나 사용이 허가되지 않습니다. 다음 시나리오는 명시적으로 지원되지 않습니다.
>
> - 다른 버전의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]과 병렬로 설치
> - 제거
> - 이전 SQL Server 에디션에서 업그레이드

**체험하기[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)]**
- [![평가 센터에서 다운로드](../includes/media/download2.png)](http://go.microsoft.com/fwlink/?LinkID=862101) [다운로드하여 [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] Windows에 설치](http://go.microsoft.com/fwlink/?LinkID=862101)
- [Red Hat Enterprise Server](../linux/quickstart-install-connect-red-hat.md), [SUSE Linux Enterprise Server](../linux/quickstart-install-connect-suse.md) 및 [Ubuntu](../linux/quickstart-install-connect-ubuntu.md)용 Linux에 설치
- [Docker의 SQL Server 2019에서 실행](../linux/quickstart-install-connect-docker.md)

## <a name="ctp-20-september-2018"></a>CTP 2.0(2018년 9월)

[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 2.0은 [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)]의 첫 번째 공개 릴리스입니다.

[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 2.0은 Evaluation Edition으로만 사용 가능합니다. 다른 에디션은 사용할 수 없습니다. CTP 2.0 지원은 설치 미디어를 포함하는 license_Eval.rtf에 설명되어 있습니다.

제한되는 지원은 다음 위치 중 하나에서 확인할 수 있습니다.

- 포럼
  - [SQL Server 피드백](http://aka.ms/sqlfeedback)
  - [SQL Server 시작](https://social.msdn.microsoft.com/Forums/sqlserver/en-US/home?forum=sqlgetstarted)
  - [Transact-SQL](https://social.msdn.microsoft.com/Forums/sqlserver/en-US/home?forum=transactsql)
  - [SQL Server 설명서](https://social.msdn.microsoft.com/Forums/sqlserver/en-US/home?forum=sqldocumentation)

- 또는 [@SQLServer](http://twitter.com/SQLServer) with [#sqlhelp](https://twitter.com/search?q=%23sqlhelp)를 사용하여 트윗

### <a name="documentation-ctp-20"></a>설명서(CTP 2.0)

- **문제 및 고객에게 미치는 영향**: SQL Server 2019(15.x)의 설명서는 제한되며 내용은 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] 설명서 집합에 포함되어 있습니다. SQL Server 2019(15.x)와 관련된 문서의 내용은 **적용 대상**에서 설명합니다.

- **문제 및 고객에게 미치는 영향**: [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 설명서는 버전별로 필터링할 수 있습니다. 각 설명서 페이지의 왼쪽 맨 위에 있는 컨트롤을 사용하여 요구 사항에 맞게 필터링합니다. 

- **문제 및 고객에게 미치는 영향**: SQL Server 2019(15.x) 관련 오프라인 콘텐츠는 제공되지 않습니다.

### <a name="hardware-and-software-requirements"></a>하드웨어 및 소프트웨어 요구 사항

- **문제 및 고객에게 미치는 영향**: 하드웨어 및 소프트웨어 요구 사항은 계속 검토 중이며 제품 릴리스에 포함할 최종 내용이 아닙니다.

  - **하드웨어**
    - [Windows - 프로세서, 메모리 및 운영 체제 요구 사항](../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md#pmosr)
    - [Linux - 시스템 요구 사항](../linux/sql-server-linux-setup.md#system)
  - **소프트웨어**
    - Windows Server 2016 이상. 추가 요구 사항은 [SQL Server 설치 요구 사항](../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)을 참조하세요.
    - Linux의 경우 [Linux - 지원되는 플랫폼](../linux/sql-server-linux-setup.md#supportedplatforms)을 참조하세요.

### <a name="sql-graph"></a>SQL 그래프

**문제 및 고객에게 미치는 영향**: 가져오기-내보내기처럼 DacFx에 종속성을 갖는 도구는 새 그래프 기능인 에지 제약 조건 또는 병합 DML에 작동하지 않습니다. [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]의 스크립팅이 작동하지 않을 수 있습니다.

**해결 방법**: [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 또는 SQLCMD를 사용하여 [!INCLUDE[tsql](../includes/tsql-md.md)] 스크립트를 작성하고 서버에 대해 실행하면 됩니다. 에지 제약 조건을 만들거나, 새로운 병합 DML 구문을 포함하거나, 그래프 개체에 대한 파생 테이블/뷰를 만드는 데이터베이스 개체를 내보내거나 가져올 수 없습니다. 사용자는 [!INCLUDE[tsql](../includes/tsql-md.md)] 스크립트를 사용하여 해당 데이터베이스에서 이러한 개체를 수동으로 만들어야 합니다. 

**적용 대상:** [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 2.0

### <a name="utf-8-collations"></a>UTF-8 데이터 정렬

**문제 및 고객에게 미치는 영향**: UTF-8 사용 데이터 정렬을 일부 다른 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 기능과 함께 사용할 수 없습니다. UTF-8은 다음 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 기능이 사용 중일 때 지원되지 않습니다.

- SQL  Server  복제
- 연결된 서버
- 메모리 내 OLTP
- Polybase용 외부 테이블

  또한 현재 Azure Data Studio 또는 SSDT에서 UTF-8 사용 데이터 정렬을 선택하기 위한 UI 지원은 없습니다. 최신 SSMS 버전은 UI의 다양한 UTF-8 사용 데이터 정렬 선택 옵션을 지원합니다.

**해결 방법**: [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 2.0에 대한 해결 방법은 없습니다.

**적용 대상:** [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 2.0

### <a name="lightweight-query-profiling-infrastructure"></a>간단한 쿼리 프로파일링 인프라

**문제 및 고객에게 미치는 영향**: 명령 `ALTER DATABASE SCOPED CONFIGURATION SET LIGHTWEIGHT_QUERY_PROFILING = ON`을 실행하면 구문 오류가 반환됩니다. 이 명령 실행에 의존하는 모든 시나리오는 실패합니다.

> [!NOTE]
> 현재 간단한 쿼리 프로파일링 인프라(LWP)를 개별 데이터베이스 수준에서 제어할 수 없으며 기본적으로 모든 데이터베이스에 대해 사용 가능 상태로 유지됩니다. LWP에 대한 자세한 내용은 [SQL Server 2019의 새로운 기능](../sql-server/what-s-new-in-sql-server-ver15.md)을 참조하세요.

**해결 방법**: [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 2.0에 대한 해결 방법은 없습니다.

**적용 대상:** [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 2.0

### <a name="always-encrypted-with-secure-enclaves"></a>보안 Enclave를 사용한 Always Encrypted

**문제 및 고객에게 미치는 영향**: 리치 계산은 몇 가지 성능 최적화가 보류 중이며, 제한된 기능을 포함하고(인덱싱 없음 등), 현재 기본적으로 사용하지 않도록 설정되어 있습니다.

**해결 방법**: 리치 계산을 사용하도록 설정하려면 `DBCC traceon(127,-1)`을 실행합니다. 자세한 내용은 [리치 계산 사용](../relational-databases/security/encryption/configure-always-encrypted-enclaves.md#configure-a-secure-enclave)을 참조하세요.

**적용 대상:** [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 2.0

### <a name="sql-server-integration-services-ssis-transfer-database-task"></a>SSIS(SQL Server Integration Services) 데이터베이스 전송 태스크

**문제 및 고객에게 미치는 영향**: `Transfer Database Task`를 `Database Online` 모드에서 데이터베이스에 전송하도록 구성하면 다음 오류를 나타내며 실패할 수 있습니다.

>태스크의 Execute 메서드가 오류 코드 0x80131500을 반환했습니다(데이터를 전송하는 동안 오류가 발생했습니다. 자세한 내용은 내부 예외를 참조하세요.). Execute 메서드는 성공해야 하며 "out" 매개 변수를 사용하여 결과를 나타내야 합니다.

**해결 방법**: 서버에서 `DBCC TRACEON (7416,-1)`을 실행하고 다시 시도하세요.

### <a name="sql-server-machine-learning-services-installation-failure"></a>SQL Server Machine Learning 서비스 설치 실패

**문제/고객에게 미치는 영향**: 주 도메인과 트러스트 관계 문제가 있는 컴퓨터에서 SQL Server Machine Learning Services 설치가 실패합니다. 이 경우 로그에 다음 오류가 표시됩니다.
 
>  오류: 0 : System.SystemException:System.Security.Principal.NTAccount.TranslateToSids(IdentityReferenceCollection sourceAccounts, Boolean& someFailed)에서 이 워크스테이션과 주 도메인 간의 트러스트 관계가 실패했습니다.

다음 위치의 로그에서 확인하세요.

* `C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\R_SERVICES\library\RevoScaleR\rxLibs\x64\RegisterRExt.log`
* `C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\PYTHON_SERVICES\Lib\site-packages\revoscalepy\rxLibs\RegisterRExt.log`
**해결 방법**: 도메인 트러스트 문제를 해결하고 설치를 다시 시도하세요.

**적용 대상**: SQL Server 2019 CTP 2.0

[!INCLUDE[get-help-options-msft-only](../includes/paragraph-content/get-help-options.md)]

![MS_Logo_X-Small](../sql-server/media/ms-logo-x-small.png)
