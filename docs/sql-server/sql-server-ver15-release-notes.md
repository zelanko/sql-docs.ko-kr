---
title: SQL Server 2019 릴리스 정보 | Microsoft Docs
ms.date: 03/27/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: release-landing
ms.topic: article
ms.assetid: 13942af8-5a40-4cef-80f5-918386767a47
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: = sql-server-ver15 || = sqlallproducts-allversions
ms.openlocfilehash: 3362a03fe1437b15985fdc557fac6536db5fd2f7
ms.sourcegitcommit: 46a2c0ffd0a6d996a3afd19a58d2a8f4b55f93de
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/15/2019
ms.locfileid: "59582877"
---
# <a name="sql-server-2019-preview-release-notes"></a>SQL Server 2019 미리 보기 릴리스 정보
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

이 문서에서는 [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP(Community Technology Preview) 릴리스의 제한 사항 및 알려진 문제에 대해 설명합니다. 관련 내용은 다음을 참조하세요.
- [SQL Server 2019의 새로운 기능](../sql-server/what-s-new-in-sql-server-ver15.md)

> [!NOTE]
> [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 미리 보기 릴리스는 예정된 릴리스의 기능을 체험할 수 있도록 하기 위해 제공됩니다. 프로덕션 용도로 지원되거나 사용이 허가되지 않습니다. 다음 시나리오는 명시적으로 지원되지 않습니다.
>
> - 다른 버전의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]과 병렬로 설치
> - 모든 버전에서 SQL Server의 기존 인스턴스 업그레이드

**체험하기[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)]**
- [![평가 센터에서 다운로드](../includes/media/download2.png)](https://go.microsoft.com/fwlink/?LinkID=862101) [다운로드하여 [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] Windows에 설치](https://go.microsoft.com/fwlink/?LinkID=862101)
- [Red Hat Enterprise Server](../linux/quickstart-install-connect-red-hat.md), [SUSE Linux Enterprise Server](../linux/quickstart-install-connect-suse.md) 및 [Ubuntu](../linux/quickstart-install-connect-ubuntu.md)용 Linux에 설치
- [Docker의 SQL Server 2019에서 실행](../linux/quickstart-install-connect-docker.md)

## <a name="ctp-24"></a>CTP 2.4
[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 2.4는 [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)]의 최신 공개 릴리스입니다.

[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 2.4는 Evaluation Edition으로만 사용 가능합니다. 다른 에디션은 사용할 수 없습니다. CTP 릴리스에 대한 지원은 설치 미디어를 포함하는 `license_Eval.rtf`에 설명되어 있습니다.

제한되는 지원은 다음 위치 중 하나에서 확인할 수 있습니다.

- 포럼
  - [SQL Server 피드백](https://aka.ms/sqlfeedback)
  - [SQL Server 시작](https://social.msdn.microsoft.com/Forums/sqlserver/en-US/home?forum=sqlgetstarted)
  - [Transact-SQL](https://social.msdn.microsoft.com/Forums/sqlserver/en-US/home?forum=transactsql)
  - [SQL Server 설명서](https://social.msdn.microsoft.com/Forums/sqlserver/en-US/home?forum=sqldocumentation)

- 또는 [@SQLServer](https://twitter.com/SQLServer) with [#sqlhelp](https://twitter.com/search?q=%23sqlhelp)를 사용하여 트윗

### <a name="documentation-ctp-24"></a>설명서(CTP 2.4)

- **문제 및 고객에게 미치는 영향**: SQL Server 2019(15.x)의 설명서는 제한되며 내용은 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] 설명서 세트에 포함되어 있습니다. SQL Server 2019(15.x)와 관련된 문서의 내용은 **적용 대상**에서 설명합니다.

- **문제 및 고객에게 미치는 영향**: [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 설명서는 버전별로 필터링할 수 있습니다. 각 설명서 페이지의 왼쪽 맨 위에 있는 컨트롤을 사용하여 요구 사항에 맞게 필터링합니다.

- **문제 및 고객에게 미치는 영향**: SQL Server 2019(15.x) 관련 오프라인 콘텐츠는 제공되지 않습니다.

### <a name="hardware-and-software-requirements-ctp-24"></a>하드웨어 및 소프트웨어 요구 사항(CTP 2.4)

- **문제 및 고객에게 미치는 영향**: 하드웨어 및 소프트웨어 요구 사항은 계속 검토 중이며 제품 릴리스에 포함할 최종 내용이 아닙니다.

  - **하드웨어**
    - [Windows - 프로세서, 메모리 및 운영 체제 요구 사항](../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md#pmosr)
    - [Linux - 시스템 요구 사항](../linux/sql-server-linux-setup.md#system)
  - **소프트웨어**
    - Windows Server 2016 이상. 추가 요구 사항은 [SQL Server 설치 요구 사항](../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)을 참조하세요.
    - Microsoft .NET Framework 4.6.2. [다운로드 센터](https://www.microsoft.com/download/details.aspx?id=53344)에서 제공됩니다.
    - Linux의 경우 [Linux - 지원되는 플랫폼](../linux/sql-server-linux-setup.md#supportedplatforms)을 참조하세요.

### <a name="updated-compiler"></a>컴파일러 업데이트

- **문제 및 고객에게 미치는 영향**: [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)]는 업데이트 컴파일러를 사용하여 빌드됩니다. CTP 2.1에서는 부동 소수점 및 다른 변환 시나리오가 업데이트된 컴파일러 때문에 이전 버전과 다른 값을 반환할 수 있다는 알려진 문제가 발생했습니다. CTP 2.2에는 영향을 받는 시나리오가 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]라는 이전 버전과 동일한 결과를 반환하는지 확인하는 작업이 포함됩니다. CTP 2.3 릴리스부터는 다른 문제가 발생하지 않았습니다. [!INCLUDE[ss2017](../includes/sssqlv14-md.md)]와 비교하여 비정상적인 결과를 즉시 [[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 팀](http://aka.ms/sqlfeedback)에게 보고해주세요.

- **해결 방법**: 해당 사항 없음

- **적용 대상**: SQL Server 2019 CTP 2.4, CTP 2.3, CTP 2.2, CTP 2.1

### <a name="utf-8-collations"></a>UTF-8 데이터 정렬

- **문제 및 고객에게 미치는 영향**: UTF-8 사용 데이터 정렬을 다른 일부 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 기능과 함께 사용할 수 없습니다. UTF-8은 다음 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 기능이 사용 중일 때 지원되지 않습니다.

  - 연결된 서버
  - 메모리 내 OLTP
  - PolyBase용 외부 테이블
  - Always Encrypted

  > [!Note]
  > 현재 Azure Data Studio 또는 SSDT(SQL Server Data Tools)에서 UTF-8 사용 데이터 정렬을 선택하도록 UI를 지원하지 않습니다. 최신 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)](SSMS) 버전은 UI의 다양한 UTF-8 사용 데이터 정렬 선택 옵션을 지원합니다.
 
- **해결 방법**: [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP에 대한 해결 방법은 없습니다.

- **적용 대상**: [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 2.4, CTP 2.3, CTP 2.2, CTP 2.1, CTP 2.0.

### <a name="sql-graph"></a>SQL 그래프

- **문제 및 고객에게 미치는 영향**: 가져오기-내보내기처럼 DacFx에 종속적인 도구는 새 그래프 기능인 Edge 제약 조건 또는 병합 DML에 작동하지 않습니다. [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]의 스크립팅이 작동하지 않을 수 있습니다.

- **해결 방법**: [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 또는 SQLCMD를 사용하여 [!INCLUDE[tsql](../includes/tsql-md.md)] 스크립트를 작성하고 서버에 대해 실행하면 됩니다. 에지 제약 조건을 만들거나, 새로운 병합 DML 구문을 포함하거나, 그래프 개체에 대한 파생 테이블/뷰를 만드는 데이터베이스 개체를 내보내거나 가져올 수 없습니다. 사용자는 [!INCLUDE[tsql](../includes/tsql-md.md)] 스크립트를 사용하여 해당 데이터베이스에서 이러한 개체를 수동으로 만들어야 합니다. 

- **적용 대상**: [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 2.4, CTP 2.3, CTP 2.2, CTP 2.1, 2.0.

### <a name="always-encrypted-with-secure-enclaves"></a>보안 Enclave를 사용한 Always Encrypted

- **문제 및 고객에게 미치는 영향**: 리치 계산은 몇 가지 성능 최적화가 보류 중이며, 제한된 기능을 포함하고(인덱싱 없음 등), 현재 기본적으로 사용하지 않도록 설정되어 있습니다.

- **해결 방법**: 리치 계산을 사용하도록 설정하려면 `DBCC traceon(127,-1)`을 실행합니다. 자세한 내용은 [리치 계산 사용](../relational-databases/security/encryption/configure-always-encrypted-enclaves.md#configure-a-secure-enclave)을 참조하세요.

- **적용 대상**: [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 2.4, CTP 2.3, 2.2, CTP 2.1, 2.0.

### <a name="system-dynamic-management-views"></a>시스템 동적 관리 뷰

- **문제 및 고객에게 미치는 영향**: 시스템 테이블 반환 함수 [sys.dm_db_objects_disabled_on_compatibility_level_change](../relational-databases/system-dynamic-management-views/spatial-data-sys-dm-db-objects-disabled-on-compatibility-level-change.md)는 `dependency` 열의 임의 값을 반환합니다.

- **적용 대상**: [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 2.4, CTP 2.3.

[!INCLUDE[get-help-options-msft-only](../includes/paragraph-content/get-help-options.md)]

![MS_Logo_X-Small](../sql-server/media/ms-logo-x-small.png)
