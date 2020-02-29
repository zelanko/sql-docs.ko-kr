---
title: SQL Server 유틸리티 제어 지점 만들기(SQL Server 유틸리티) | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- SQL12.SWB.create.ucp.progress.F1
- SQL12.SWB.create.ucp.welcome.F1
- SQL12.SWB.create.ucp.Summary.F1
- SQL12.SWB.create.ucp.validation.F1
- SQL12.SWB.create.ucp.instancename.F1
- SQL12.SWB.create.ucp.agentconfiguration.F1
helpviewer_keywords:
- Create UCP
- UCP
ms.assetid: d5335124-1625-47ce-b4ac-36078967158c
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: eefa464ae8cb694001d40c5ad9090f7f4efbd8e6
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/28/2020
ms.locfileid: "78175882"
---
# <a name="create-a-sql-server-utility-control-point-sql-server-utility"></a>SQL Server 유틸리티 제어 지점 만들기(SQL Server 유틸리티)
  엔터프라이즈에서는 여러 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티를 사용할 수 있으며 각 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티가 여러 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스와 데이터 계층 애플리케이션을 관리할 수 있습니다. 각 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티에는 UCP(유틸리티 제어 지점)가 하나씩 있습니다. 각 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티를 위한 새 UCP를 만들어야 합니다. 각 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 관리되는 인스턴스와 데이터 계층 애플리케이션은 한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티의 멤버이며 단일 UCP에 의해 관리됩니다.

 UCP는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 관리되는 인스턴스에서 15분마다 구성 및 성능 정보를 수집합니다. 이 정보는 UCP의 UMDW(유틸리티 관리 데이터 웨어하우스)에 저장됩니다. UMDW의 파일 이름은 sysutility_mdw입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 성능 데이터를 정책과 비교하면 리소스 사용 병목 현상과 통합 기회를 식별하는 데 도움이 됩니다.

## <a name="before-you-begin"></a>시작하기 전에
 UCP를 만들기 전에 다음 요구 사항 및 권장 사항을 검토하십시오.

 이 릴리스에서 UCP 및 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 관리되는 인스턴스는 다음 요구 사항을 충족해야 합니다.

-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 버전 10.50 이상이어야 합니다.

-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 유형은 [!INCLUDE[ssDE](../../includes/ssde-md.md)]이어야 합니다.

-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티는 단일 Windows 도메인이나 양방향 트러스트 관계가 있는 도메인에서 실행해야 합니다.

-   UCP 및 모든 SQL Server의 관리되는 인스턴스에 대한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 계정에는 Active Directory의 사용자에 대한 읽기 권한이 있어야 합니다.

 이 릴리스에서 UCP는 다음 요구 사항을 충족해야 합니다.

-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스는 지원되는 버전이어야 합니다. 버전에서 지원 되는 기능 목록은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [SQL Server 2014 버전에서 지 원하는 기능](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)을 참조 하세요.

-   대/소문자를 구분하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에서 UCP를 호스팅하는 것이 좋습니다.

 UCP 컴퓨터의 용량 계획 시 다음 권장 사항을 고려하십시오.

-   일반적인 시나리오의 경우 UCP의 UMDW 데이터베이스(sysutility_mdw)에 사용되는 디스크 공간은 SQL Server의 관리되는 인스턴스당 1년에 약 2GB입니다. 이 예상치는 관리되는 인스턴스가 수집하는 데이터베이스 및 시스템 개체의 수에 따라 달라집니다. UMDW(sysutility_mdw) 디스크 공간의 증가 속도는 처음 2일간이 가장 높습니다.

-   일반적인 시나리오의 경우 UCP의 msdb에 사용되는 디스크 공간은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 관리되는 인스턴스당 약 20MB입니다. 이 예상치는 리소스 사용률 정책과 관리되는 인스턴스가 수집하는 데이터베이스 및 시스템 개체의 수에 따라 다릅니다. 일반적으로 디스크 공간 사용은 정책 위반 횟수가 늘고 일시적 리소스의 이동 시간대 기간이 길어짐에 따라 증가합니다.

-   UCP에서 관리되는 인스턴스를 제거하더라도 관리되는 인스턴스에 대한 데이터 보존 기간이 만료되기 전까지는 UCP 데이터베이스에서 사용되는 디스크 공간이 줄어들지 않습니다.

 이 릴리스에서 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 관리되는 인스턴스는 다음 요구 사항을 충족해야 합니다.

-   UCP가 대/소문자를 구분하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에서 호스팅되는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 관리되는 인스턴스 역시 대/소문자를 구분하도록 설정하는 것이 좋습니다.

-   FILESTREAM 데이터는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티 모니터링에서 지원되지 않습니다.

 자세한 내용은 [SQL Server의 최대 용량 사양](../../sql-server/maximum-capacity-specifications-for-sql-server.md) 및 [SQL Server 2014 버전에서 지 원하는 기능](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)을 참조 하세요.

### <a name="remove-previous-utility-control-points-before-installing-a-new-one"></a>새 유틸리티 제어 지점을 설치하기 전에 이전 유틸리티 제어 지점 제거
 이전에 UCP(유틸리티 제어 지점)로 구성된 적이 없는 UCP를 SQL Server 인스턴스에 설치하는 경우 설치하기 전에 SQL Server의 관리되는 인스턴스 및 해당 UCP를 모두 제거해야 합니다. 이 작업은 **sp_sysutility_ucp_remove** 저장 프로시저를 실행하여 수행할 수 있습니다.

 프로시저를 실행하기 전에 다음 요구 사항을 확인하십시오.

-   UCP에 해당하는 컴퓨터에서 이 절차를 실행해야 합니다.

-   UCP를 만들 때 필요한 권한인 sysadmin 권한의 사용자가 이 절차를 실행해야 합니다.

-   모든 SQL Server의 관리되는 인스턴스는 해당 UCP에서 제거되어야 합니다. 즉, UCP가 SQL Server의 관리되는 인스턴스입니다. 자세한 내용은 [방법: SQL Server 유틸리티에서 SQL Server 인스턴스 제거](https://go.microsoft.com/fwlink/?LinkId=169392)를 참조하세요.

 이 프로시저를 사용하여 SQL Server 유틸리티에서 SQL Server UCP를 제거합니다. 제거가 완료되면 SQL Server 인스턴스에서 UCP를 다시 만들 수 있습니다.

 SQL Server Management Studio를 사용하여 UCP에 연결한 후 다음 스크립트를 실행합니다.

```sql
EXEC msdb.dbo.sp_sysutility_ucp_remove;
```

> [!NOTE]
>  UCP가 제거된 SQL Server 인스턴스에 유틸리티 이외의 데이터 컬렉션 집합이 있는 경우 sysutility_mdw 데이터베이스는 이 프로시저로 삭제되지 않습니다. 이런 경우 UCP를 다시 만들기 전에 sysutility_mdw 데이터베이스를 수동으로 삭제해야 합니다.

 각 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 관리되는 인스턴스와 데이터 계층 애플리케이션은 한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티의 멤버이며 단일 UCP에 의해 관리됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티 개념에 대한 자세한 내용은 [SQL Server 유틸리티 기능 및 태스크](sql-server-utility-features-and-tasks.md)를 참조하세요.

 UCP는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티의 중심 원리 지점입니다. UCP를 사용하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 관리되는 인스턴스와 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 계층 애플리케이션에서 수집된 구성 및 성능 데이터를 볼 수 있으며 일반적인 용량 계획 작업을 수행할 수 있습니다. UCP는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 등록 및 제거하기 위한 시작 지점입니다.

 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 등록하면 관리되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 및 데이터 계층 애플리케이션의 리소스 상태를 모니터링하여 통합 기회를 식별하고 리소스 병목 현상을 격리할 수 있습니다. 자세한 내용은 [SQL Server 유틸리티에서 SQL Server 인스턴스 모니터링](monitor-instances-of-sql-server-in-the-sql-server-utility.md)을 참조하세요.

> [!IMPORTANT]
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티 컬렉션 집합을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티 이외의 컬렉션 집합과 함께 사용하는 것이 가능합니다. 즉 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 관리되는 인스턴스가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티의 멤버이면 다른 컬렉션 집합으로 모니터링할 수 있습니다. 그러나 관리되는 인스턴스의 모든 컬렉션 집합은 해당 데이터를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티 관리 데이터 웨어하우스로 업로드합니다. 자세한 내용은 [같은 SQL Server 인스턴스에서 유틸리티 및 유틸리티 이외의 컬렉션 집합을 실행하기 위한 고려 사항](run-utility-and-non-utility-collection-sets-on-same-sql-instance.md) 및 [유틸리티 제어 지점 데이터 웨어하우스 구성&#40;SQL Server 유틸리티&#41;](configure-your-utility-control-point-data-warehouse-sql-server-utility.md)을 참조하세요.

## <a name="wizard-steps"></a>마법사 단계
 ![](../../database-engine/media/create-ucp.gif "Create_UCP")

 다음 섹션에서는 마법사 워크플로의 각 페이지에서 새 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] UCP를 만들기 위한 정보를 제공합니다. 마법사를 시작하여 새 UCP를 만들려면 SSMS의 보기 메뉴에서 유틸리티 탐색기 창을 열고, 유틸리티 탐색기 창의 맨 위에 있는 ![](../../database-engine/media/create-ucp.gif "Create_UCP") **UCP 만들기** 단추를 클릭합니다.

 아래 목록의 링크를 클릭하여 마법사 페이지에 대한 세부 정보를 탐색할 수 있습니다.

 이 작업의 PowerShell 스크립트에 대한 자세한 내용은 [예](#PowerShell_create_UCP)를 참조하십시오.

-   [UCP 만들기 마법사 소개](#Welcome)

-   [인스턴스 지정](#Instance_name)

-   [연결 대화 상자](#Connection_dialog)

-   [유틸리티 컬렉션 집합 계정](#Agent_configuration)

-   [유효성 검사 규칙](#Validation_rules)

-   [요약](#Summary)

-   [유틸리티 제어 지점 만들기](#Creating_UCP)

##  <a name="Welcome"></a> UCP 만들기 마법사 소개
 유틸리티 탐색기를 열 때 연결된 유틸리티 제어 지점이 없으면 기존 항목에 연결하거나 새 항목을 만들어야 합니다.

 **기존 UCP에 연결** - 배포 환경에 기존 유틸리티 제어 지점이 있는 경우 유틸리티 탐색기 창의 맨 위에 있는 ![](../../database-engine/media/connect-to-utility.gif "Connect_to_Utility")**유틸리티에 연결** 단추를 클릭하여 연결할 수 있습니다. 기존 UCP에 연결하려면 관리자 자격 증명이 있거나 유틸리티 읽기 역할의 멤버여야 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티당 UCP는 하나만 있을 수 있으며 사용자는 SSMS 인스턴스에서 하나의 UCP에만 연결할 수 있습니다.

 **새 UCP 만들기** - 새 유틸리티 제어 지점을 만들려면 유틸리티 탐색기 창의 맨 위에 있는 ![](../../database-engine/media/create-ucp.gif "Create_UCP")**UCP 만들기** 단추를 클릭합니다. 새 UCP를 만들려면 연결 대화 상자에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 이름을 지정하고 관리자 자격 증명을 제공해야 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티 한 개마다 UCP를 한 개만 사용할 수 있습니다.

##  <a name="Instance_name"></a> 인스턴스 지정
 만들려는 UCP에 대한 다음 정보를 지정합니다.

-   **인스턴스 이름** - 연결 대화 상자에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 선택하려면 **연결...** 을 클릭합니다. 컴퓨터 이름과 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 이름을 ComputerName\InstanceName 형식으로 입력합니다.

-   **유틸리티 이름** - 네트워크에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티를 식별하는 데 사용되는 이름을 지정합니다.

 계속하려면 **다음**을 클릭합니다.

##  <a name="Connection_dialog"></a> 연결 대화 상자
 서버로 연결 대화 상자에서 서버 유형, 컴퓨터 이름 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 이름 정보를 확인합니다. 자세한 내용은 [서버에 연결&#40;데이터베이스 엔진&#41;](../../ssms/f1-help/connect-to-server-database-engine.md)을 참조하세요.

> [!NOTE]
>  연결이 암호화되어 있으면 암호화 연결이 사용됩니다. 연결이 암호화되어 있지 않으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티는 암호화된 연결을 사용하여 다시 연결합니다.

 계속하려면 **연결...** 을 클릭합니다.

##  <a name="Agent_configuration"></a> 유틸리티 컬렉션 집합 계정
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티 컬렉션 집합을 실행할 Windows 도메인 계정을 지정합니다. 이 계정은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티 컬렉션 집합에 대한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 프록시 계정으로 사용됩니다. 또는 기존 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스 계정을 사용할 수 있습니다. 유효성 검사 요구 사항을 통과하려면 계정을 지정할 때 다음 지침을 따릅니다.

 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스 계정 옵션을 지정하는 경우

-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스 계정은 LocalSystem, NetworkService 또는 LocalService와 같은 기본 제공 계정이 아닌 Windows 도메인 계정이어야 합니다.

 계속하려면 **다음**을 클릭합니다.

##  <a name="Validation_rules"></a> 유효성 검사 규칙
 이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]릴리스에서는 UCP를 만들려는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 다음 조건이 충족되어야 합니다.

|유효성 검사 규칙|정정 작업|
|---------------------|-----------------------|
|유틸리티 제어 지점이 생성될 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대한 관리자 권한이 있어야 합니다.|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 대한 관리자 권한이 있는 계정으로 로그온합니다.|
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전이 10.50 이상이어야 합니다.|UCP를 호스팅할 다른 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 지정합니다.|
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스는 지원되는 버전이어야 합니다. 버전에서 지원 되는 기능 목록은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [SQL Server 2014 버전에서 지 원하는 기능](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)을 참조 하세요.|UCP를 호스팅할 다른 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 지정합니다.|
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 다른 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] UCP에 등록된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스여서는 안됩니다.|UCP를 호스팅할 다른 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 지정하거나, 현재 관리되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 있는 UCP에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스의 등록을 해제합니다.|
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 이미 다른 유틸리티 제어 지점을 호스팅하고 있으면 안 됩니다.|UCP를 호스팅할 다른 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 지정합니다.|
|지정한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 TCP/IP를 사용하도록 설정해야 합니다.|지정한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 대해 TCP/IP를 사용하도록 설정합니다.|
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 "sysutility_mdw"라는 데이터베이스가 있으면 안 됩니다.|UCP 만들기 작업을 수행하면 "sysutility_mdw"라는 UMDW(유틸리티 관리 데이터 웨어하우스)가 생성됩니다. 이 작업을 수행하려면 유효성 검사가 실행되는 시점에 컴퓨터에 이 이름이 존재하지 않아야 합니다. 계속하려면 "sysutility_mdw"라는 데이터베이스를 제거하거나 이름을 변경해야 합니다. 이름을 변경하는 방법은 [ALTER DATABASE&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)를 참조하세요.|
|지정된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 컬렉션 집합은 중지해야 합니다.|지정된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 UCP가 생성되는 동안 기존 컬렉션 집합을 중지합니다. 데이터 수집기가 해제된 경우 이를 설정하고 실행 중인 컬렉션 집합을 중지한 다음 UCP 생성 작업을 위한 유효성 검사 규칙을 다시 실행합니다.<br /><br /> 데이터 수집기를 활성화하려면<br /><br /> 개체 탐색기에서 **관리** 노드를 확장합니다.<br /><br /> **데이터 컬렉션**을 마우스 오른쪽 단추로 클릭한 다음 **데이터 컬렉션 사용**을 클릭합니다.<br /><br /> 컬렉션 집합을 중지하려면<br /><br /> 개체 탐색기에서 관리 노드, **데이터 컬렉션**, **시스템 데이터 컬렉션 집합**을 차례로 확장합니다.<br /><br /> 중지할 컬렉션 집합을 마우스 오른쪽 단추로 클릭한 다음 **데이터 컬렉션 집합 중지**를 클릭합니다.<br /><br /> 메시지 상자에 이 동작의 결과가 표시되며, 컬렉션 집합의 아이콘에 빨간색 원이 표시되어 컬렉션 집합이 중지되었음을 나타냅니다.|
|지정한 인스턴스에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스가 시작해야 합니다. 지정한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 장애 조치(failover) 클러스터 인스턴스일 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스가 수동으로 시작되도록 구성되어야 합니다. 그렇지 않을 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스가 자동으로 시작하도록 구성되어야 합니다.|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스를 시작합니다. 지정한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 장애 조치(failover) 클러스터 인스턴스일 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스를 수동으로 시작하도록 구성합니다. 그렇지 않을 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스가 자동으로 시작하도록 구성합니다.|
|WMI가 올바르게 구성되어 있어야 합니다.|WMI 구성 문제를 해결하려면 [SQL Server 유틸리티 문제 해결](../../database-engine/troubleshoot-the-sql-server-utility.md)을 참조하세요.|
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 프록시 계정은 Network Service와 같은 기본 제공 계정일 수 없습니다.|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 프록시 계정이 Network Service와 같은 기본 제공 계정인 경우 계정을 sysadmin인 Windows 도메인 계정으로 다시 할당하세요.|
|프록시 계정 옵션을 선택한 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 프록시 계정은 유효한 Windows 도메인 계정이어야 합니다.|유효한 Windows 도메인 계정을 지정합니다. 계정이 유효한지 확인하려면 Windows 도메인 계정을 사용하여 지정된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스로 로그온합니다.|
|서비스 계정 옵션을 선택한 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스 계정은 Network Service와 같은 기본 제공 계정일 수 없습니다.|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스 계정이 Network Service와 같은 기본 제공 계정인 경우 계정을 Windows 도메인 계정으로 다시 할당하세요.|
|서비스 계정 옵션을 선택한 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스 계정은 유효한 Windows 도메인 계정이어야 합니다.|유효한 Windows 도메인 계정을 지정합니다. 계정이 유효한지 확인하려면 Windows 도메인 계정을 사용하여 지정된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스로 로그온합니다.|

 유효성 검사 결과에 실패한 조건이 있으면 차단 문제를 수정하고 **유효성 검사 다시 실행** 을 클릭하여 컴퓨터 구성을 확인합니다.

 유효성 검사 보고서를 저장하려면 **보고서 저장** 을 클릭한 다음 파일의 위치를 지정합니다.

 계속하려면 **다음**을 클릭합니다.

##  <a name="Summary"></a> 요약
 요약 페이지에는 UCP에 대해 제공한 정보가 표시됩니다.

-   UCP를 호스팅하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 이름

-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티 이름

-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티 데이터 컬렉션용 작업을 실행하는 데 사용되는 계정 이름

 UCP 구성 설정을 변경하려면 **이전**을 클릭합니다. 계속하려면 **다음**을 클릭합니다.

##  <a name="Creating_UCP"></a> 유틸리티 제어 지점 만들기
 마법사는 UCP를 만드는 작업 중에 단계를 표시하고 상태를 제공합니다.

-   UCP를 만들기 위해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 준비하고 있습니다.

-   UMDW(유틸리티 관리 데이터 웨어하우스)를 만들고 있습니다.

-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] UMDW를 초기화하고 있습니다. UMDW의 파일 이름은 sysutility_mdw입니다.

-   UCP를 구성하고 있습니다.

-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티 컬렉션 집합을 구성하고 있습니다.

 UCP 만들기 작업에 대한 보고서를 저장하려면 **보고서 저장** 을 클릭한 다음 파일의 위치를 지정합니다.

 마법사를 완료하려면 **마침**을 클릭합니다.

 UCP 만들기 마법사를 완료한 후에는 SSMS의 유틸리티 탐색기 탐색 창에 UCP에 대한 노드가 표시되며 이 노드 아래에는 배포된 데이터 계층 애플리케이션, 관리되는 인스턴스 및 유틸리티 관리 노드가 표시됩니다. UCP는 자동으로 관리되는 인스턴스가 됩니다.

 데이터 수집 프로세스는 즉시 시작되지만 최대 30분이 지나야 유틸리티 탐색기 내용 창의 대시보드와 뷰포인트에 데이터가 표시되기 시작합니다. 데이터 수집은 15분마다 한 번씩 수행됩니다. 초기 데이터는 UCP 자체에 대한 것입니다. 즉, UCP가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티의 첫 번째 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 관리되는 인스턴스입니다.

 대시보드를 표시하려면 SSMS 메뉴에서 **보기** 를 클릭하고 **유틸리티 탐색기 내용** 을 선택합니다. 데이터를 새로 고치려면 유틸리티 탐색기 창에서 유틸리티 이름을 마우스 오른쪽 단추로 클릭하고 **새로 고침**을 선택합니다.

 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 추가 인스턴스를 등록하는 방법에 대한 자세한 내용은 [SQL Server 인스턴스 등록&#40;SQL Server 유틸리티&#41;](enroll-an-instance-of-sql-server-sql-server-utility.md)를 참조하세요. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티에서 관리되는 인스턴스인 UCP를 제거하려면 **유틸리티 탐색기** 창에서 **관리되는 인스턴스** 를 선택하여 목록 뷰에 관리되는 인스턴스를 표시한 다음 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티 탐색기 내용 **목록 뷰에서** 인스턴스 이름을 마우스 오른쪽 단추로 클릭하고 **관리되지 않는 인스턴스로 설정**을 선택합니다.

##  <a name="PowerShell_create_UCP"></a> PowerShell을 사용하여 유틸리티 제어 지점 만들기
 다음 예를 사용하여 새 유틸리티 제어 지점을 만들 수 있습니다.

```powershell
$UtilityInstance = new-object -Type Microsoft.SqlServer.Management.Smo.Server "ComputerName\UCP-Name";
$SqlStoreConnection = new-object -Type Microsoft.SqlServer.Management.Sdk.Sfc.SqlStoreConnection $UtilityInstance.ConnectionContext.SqlConnectionObject;
$Utility = [Microsoft.SqlServer.Management.Utility.Utility]::CreateUtility("Utility", $SqlStoreConnection, "ProxyAccount", "ProxyAccountPassword");
```

## <a name="see-also"></a>참고 항목
 [SQL Server 유틸리티 기능 및 작업](sql-server-utility-features-and-tasks.md) [SQL Server 유틸리티 문제 해결](../../database-engine/troubleshoot-the-sql-server-utility.md)
