---
title: SQL Server 인스턴스 등록(SQL Server 유틸리티) | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql13.SWB.makemanaged.agentaccount.F1
- sql13.SWB.makemanaged.welcome.F1
- sql13.SWB.makemanaged.enrolling.F1
- sql13.SWB.makemanaged.instancename.F1
- sql13.SWB.makemanaged.Summary.F1
- sql13.SWB.makemanaged.progress.F1
- sql13.SWB.makemanaged.validation.F1
helpviewer_keywords:
- Enroll instance
ms.assetid: a801c619-611b-4e82-a8d8-d1e01691b7a1
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: ff7bffcb3a31a697300d98e0de03a7f3e3111701
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51681341"
---
# <a name="enroll-an-instance-of-sql-server-sql-server-utility"></a>SQL Server 인스턴스 등록(SQL Server 유틸리티)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 기존 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티에 등록하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 관리되는 인스턴스로서 성능과 구성을 모니터링할 수 있습니다. UCP(유틸리티 제어 지점)는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 관리되는 인스턴스에서 15분마다 구성 및 성능 정보를 수집합니다. 이 정보는 UCP의 UMDW(유틸리티 관리 데이터 웨어하우스)에 저장됩니다. UMDW의 파일 이름은 sysutility_mdw입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 성능 데이터를 정책과 비교하면 리소스 사용 병목 현상과 통합 기회를 식별하는 데 도움이 됩니다.  
  
 이 릴리스에서 UCP 및 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 관리되는 인스턴스는 다음 요구 사항을 충족해야 합니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 버전 10.50 이상이어야 합니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 유형은 [!INCLUDE[ssDE](../../includes/ssde-md.md)]이어야 합니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티는 단일 Windows 도메인이나 양방향 신뢰 관계가 있는 도메인에서 운영되어야 합니다.  
  
-   UCP 및 모든 SQL Server의 관리되는 인스턴스에 대한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 계정에는 Active Directory의 사용자에 대한 읽기 권한이 있어야 합니다.  
  
-   등록할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스는 SQL Azure일 수 없습니다.  
  
 이 릴리스에서 UCP는 다음 요구 사항을 충족해야 합니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스는 지원되는 버전이어야 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]버전에서 지원되는 기능 목록은 [SQL Server 2016 버전에서 지원하는 기능](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)을 참조하세요.  
  
-   대/소문자를 구분하는 SQL Server 인스턴스에서 UCP를 호스팅하는 것이 좋습니다.  
  
-   UCP 컴퓨터의 용량 계획 시 다음 권장 사항을 고려하십시오.  
  
    -   일반적인 시나리오의 경우 UCP의 UMDW 데이터베이스(sysutility_mdw)에 사용되는 디스크 공간은 SQL Server의 관리되는 인스턴스당 1년에 약 2GB입니다. 이 예상치는 관리되는 인스턴스가 수집하는 데이터베이스 및 시스템 개체의 수에 따라 달라집니다. UMDW(sysutility_mdw) 디스크 공간의 증가 속도는 처음 2일간이 가장 높습니다.  
  
    -   일반적인 시나리오의 경우 UCP의 msdb에 사용되는 디스크 공간은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 관리되는 인스턴스당 약 20MB입니다. 이 예상치는 리소스 사용률 정책과 관리되는 인스턴스가 수집하는 데이터베이스 및 시스템 개체의 수에 따라 다릅니다. 일반적으로 디스크 공간 사용은 정책 위반 횟수가 늘고 일시적 리소스의 이동 시간대 기간이 길어짐에 따라 증가합니다.  
  
    -   UCP에서 관리되는 인스턴스를 제거하더라도 관리되는 인스턴스에 대한 데이터 보존 기간이 만료되기 전까지는 UCP 데이터베이스에서 사용되는 디스크 공간이 줄어들지 않습니다.  
  
 이 릴리스에서 모든 SQL Server의 관리되는 인스턴스는 다음 요구 사항을 충족해야 합니다.  
  
-   UCP가 대/소문자 구분 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에서 호스팅되는 경우 SQL Server의 관리되는 인스턴스 역시 대/소문자를 구분하도록 설정하는 것이 좋습니다.  
  
-   FILESTREAM 데이터는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티 모니터링에서 지원되지 않습니다.  
  
 자세한 내용은 [SQL Server의 최대 용량 사양](../../sql-server/maximum-capacity-specifications-for-sql-server.md) 및 [SQL Server 2016 버전에서 지원하는 기능](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)을 참조하세요.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티 개념에 대한 자세한 내용은 [SQL Server 유틸리티 기능 및 태스크](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)를 참조하세요.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티 컬렉션 집합을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티 이외의 컬렉션 집합과 함께 사용하는 것이 가능합니다. 즉 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 관리되는 인스턴스가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티의 멤버이면 다른 컬렉션 집합으로 모니터링할 수 있습니다. 그러나 관리되는 인스턴스의 모든 컬렉션 집합은 해당 데이터를 유틸리티 관리 데이터 웨어하우스로 업로드합니다. 자세한 내용은 [같은 SQL Server 인스턴스에서 유틸리티 및 유틸리티 이외의 컬렉션 집합을 실행하기 위한 고려 사항](../../relational-databases/manage/run-utility-and-non-utility-collection-sets-on-same-sql-instance.md) 및 [유틸리티 제어 지점 데이터 웨어하우스 구성&#40;SQL Server 유틸리티&#41;](../../relational-databases/manage/configure-your-utility-control-point-data-warehouse-sql-server-utility.md)을 참조하세요.  
  
## <a name="wizard-steps"></a>마법사 단계  
 다음 섹션에서는 마법사 워크플로의 각 페이지에 대한 자세한 정보를 제공합니다. 링크를 클릭하여 마법사의 세부 정보 페이지로 이동할 수 있습니다. 이 작업의 PowerShell 스크립트에 대한 자세한 내용은 PowerShell [예](#PowerShell_enroll)를 참조하십시오.  
  
-   [인스턴스 등록 마법사 소개](#Welcome)  
  
-   [SQL Server 인스턴스 지정](#Instance_name)  
  
-   [연결 대화 상자](#Connection_dialog)  
  
-   [유틸리티 컬렉션 집합 계정](#Proxy_configuration)  
  
-   [SQL Server 인스턴스 유효성 검사](#Validation_rules)  
  
-   [인스턴스 등록 요약](#Summary)  
  
-   [SQL Server 인스턴스 등록](#Enrolling)  
  
##  <a name="Welcome"></a> 인스턴스 등록 마법사 소개  
 마법사를 시작하려면 유틸리티 제어 지점의 유틸리티 탐색기 트리를 확장하고 **관리되는 인스턴스**를 마우스 오른쪽 단추로 클릭한 다음 **관리되는 인스턴스 추가…** 를 선택합니다.  
  
 계속하려면 **다음**을 클릭합니다.  
  
##  <a name="Instance_name"></a> SQL Server 인스턴스 지정  
 연결 대화 상자에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 선택하려면 **연결…** 을 클릭합니다. 컴퓨터 이름과 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 이름을 ComputerName\InstanceName 형식으로 입력합니다. 자세한 내용은 [서버에 연결&#40;데이터베이스 엔진&#41;](https://msdn.microsoft.com/library/ee9017b4-8a19-4360-9003-9e6484082d41)을 참조하세요.  
  
 계속하려면 **다음**을 클릭합니다.  
  
##  <a name="Connection_dialog"></a> 연결 대화 상자  
 서버로 연결 대화 상자에서 서버 유형, 컴퓨터 이름 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 이름 정보를 확인합니다. 자세한 내용은 [서버에 연결&#40;데이터베이스 엔진&#41;](https://msdn.microsoft.com/library/ee9017b4-8a19-4360-9003-9e6484082d41)을 참조하세요.  
  
> [!NOTE]  
>  연결이 암호화되어 있으면 암호화 연결이 사용됩니다. 연결이 암호화되어 있지 않으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티는 암호화된 연결을 사용하여 다시 연결합니다.  
  
 계속하려면 **연결…** 을 클릭합니다.  
  
##  <a name="Proxy_configuration"></a> 유틸리티 컬렉션 집합 계정  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티 컬렉션 집합을 실행할 Windows 도메인 계정을 지정합니다. 이 계정은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티 컬렉션 집합에 대한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 프록시 계정으로 사용됩니다. 또는 기존 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스 계정을 사용할 수 있습니다. 유효성 검사 요구 사항을 통과하려면 계정을 지정할 때 다음 지침을 따릅니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스 계정 옵션을 지정하는 경우  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스 계정은 LocalSystem, NetworkService 또는 LocalService와 같은 기본 제공 계정이 아닌 Windows 도메인 계정이어야 합니다.  
  
 계속하려면 **다음**을 클릭합니다.  
  
##  <a name="Validation_rules"></a> SQL Server 인스턴스 유효성 검사  
 이 릴리스에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 다음 조건이 충족되어야 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티에 등록할 수 있습니다.  
  
|조건|수정 동작|  
|---------------|-----------------------|  
|지정된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 및 UCP에 대한 관리자 권한이 있어야 합니다.|지정된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 및 UCP에 대한 관리자 권한이 있는 계정으로 로그온합니다.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전이 인스턴스 등록을 지원해야 합니다.|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]버전에서 지원되는 기능 목록은 [SQL Server 2016 버전에서 지원하는 기능](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)을 참조하세요.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] UCP에서 TCP/IP를 사용하도록 설정해야 합니다.|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] UCP에서 TCP/IP를 사용하도록 설정합니다.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 이미 다른 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] UCP에 등록되어 있으면 안 됩니다.|지정하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 기존 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티의 일부로 이미 관리되고 있는 경우 이를 다른 UCP에 등록할 수 없습니다.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 이미 UCP이면 안 됩니다.|지정하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 연결하려는 UCP가 아닌 다른 UCP인 경우 이를 이 UCP에 등록할 수 없습니다.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티 컬렉션 집합이 설치되어 있어야 합니다.|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스를 다시 설치합니다.|  
|지정된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 컬렉션 집합은 중지해야 합니다.|지정된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스의 기존 컬렉션 집합을 중지합니다. 데이터 수집기가 해제된 경우 이를 설정하고 실행 중인 컬렉션 집합을 중지한 다음 UCP 생성 작업을 위한 유효성 검사 규칙을 다시 실행합니다.<br /><br /> 데이터 수집기를 활성화하려면<br /><br /> 개체 탐색기에서 **관리** 노드를 확장합니다.<br /><br /> **데이터 컬렉션**을 마우스 오른쪽 단추로 클릭한 다음 **데이터 컬렉션 사용**을 클릭합니다.<br /><br /> 컬렉션 집합을 중지하려면<br /><br /> 개체 탐색기에서 관리 노드, **데이터 컬렉션**, **시스템 데이터 컬렉션 집합**을 차례로 확장합니다.<br /><br /> 중지할 컬렉션 집합을 마우스 오른쪽 단추로 클릭한 다음 **데이터 컬렉션 집합 중지**를 클릭합니다.<br /><br /> 메시지 상자에 이 동작의 결과가 표시되며, 컬렉션 집합의 아이콘에 빨간색 원이 표시되어 컬렉션 집합이 중지되었음을 나타냅니다.|  
|지정한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스가 시작되어야 합니다.|지정한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에이전트 서비스를 시작합니다. 지정한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 장애 조치(failover) 클러스터 인스턴스일 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스를 수동으로 시작하도록 구성합니다. 그렇지 않을 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스가 자동으로 시작하도록 구성합니다.|  
|UCP에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스가 시작되어야 합니다.|UCP에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스를 시작합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] UCP가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 장애 조치(failover) 클러스터 인스턴스일 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스가 수동으로 시작되도록 구성합니다. 그렇지 않을 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스가 자동으로 시작하도록 구성합니다.|  
|WMI가 올바르게 구성되어 있어야 합니다.|WMI 구성 문제를 해결하려면 [SQL Server 유틸리티 문제 해결](https://msdn.microsoft.com/library/f5f47c2a-38ea-40f8-9767-9bc138d14453)을 참조하세요.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 프록시 계정이 UCP의 유효한 Windows 도메인 계정이어야 합니다.|유효한 Windows 도메인 계정을 지정합니다. 계정이 유효한지 확인하려면 Windows 도메인 계정을 사용하여 UCP로 로그온합니다.|  
|프록시 계정 옵션을 선택한 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 프록시 계정은 지정된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스의 유효한 Windows 도메인 계정이어야 합니다.|유효한 Windows 도메인 계정을 지정합니다. 계정이 유효한지 확인하려면 Windows 도메인 계정을 사용하여 지정된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스로 로그온합니다.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스 계정은 Network Service와 같은 기본 제공 계정일 수 없습니다.|Windows 도메인 계정으로 계정을 다시 할당합니다. 계정이 유효한지 확인하려면 Windows 도메인 계정을 사용하여 지정된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스로 로그온합니다.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스 계정이 UCP의 유효한 Windows 도메인 계정이어야 합니다.|유효한 Windows 도메인 계정을 지정합니다. 계정이 유효한지 확인하려면 Windows 도메인 계정을 사용하여 UCP로 로그온합니다.|  
|서비스 계정 옵션을 선택한 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 프록시 계정은 지정된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스의 유효한 Windows 도메인 계정이어야 합니다.|유효한 Windows 도메인 계정을 지정합니다. 계정이 유효한지 확인하려면 Windows 도메인 계정을 사용하여 지정된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스로 로그온합니다.|  
  
 유효성 검사 결과에 실패한 조건이 있으면 차단 문제를 수정하고 **유효성 검사 다시 실행** 을 클릭하여 컴퓨터 구성을 확인합니다.  
  
 유효성 검사 보고서를 저장하려면 **보고서 저장** 을 클릭한 다음 파일의 위치를 지정합니다.  
  
 계속하려면 **다음**을 클릭합니다.  
  
##  <a name="Summary"></a> 인스턴스 등록 요약  
 요약 페이지에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티에 추가되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대한 정보가 나열됩니다.  
  
 관리되는 인스턴스 설정:  
  
-   SQL Server 인스턴스 이름: ComputerName\InstanceName  
  
-   유틸리티 컬렉션 집합 계정: DomainName\UserName  
  
 계속하려면 **다음**을 클릭합니다.  
  
##  <a name="Enrolling"></a> SQL Server 인스턴스 등록  
 등록 페이지는 작업 상태를 제공합니다.  
  
-   인스턴스 등록을 준비합니다.  
  
-   수집된 데이터를 위한 캐시 디렉터리를 만듭니다.  
  
-   유틸리티 컬렉션 집합을 구성합니다.  
  
 등록 작업에 대한 보고서를 저장하려면 **보고서 저장** 을 클릭한 다음 파일의 위치를 지정합니다.  
  
 마법사를 완료하려면 **마침**을 클릭합니다.  
  
> [!NOTE]  
>  SQL Server 인증을 사용하여 SQL Server 인스턴스에 연결하여 등록할 경우 UCP가 위치한 도메인이 아닌 다른 Active Directory 도메인에 속한 프록시 계정을 지정하면 인스턴스 유효성 검사는 성공하지만 다음 오류 메시지와 함께 등록 작업이 실패합니다.  
>   
>  Transact-SQL 문 또는 일괄 처리를 실행하는 동안 예외가 발생했습니다. (Microsoft.SqlServer.ConnectionInfo)  
>   
>  추가 정보: Windows NT 그룹/사용자 '\<DomainName\AccountName>'에 대한 정보를 가져올 수 없습니다. 오류 코드 0x5. (Microsoft SQL Server, 오류: 15404)  
>   
>  이 문제를 해결하는 자세한 내용은 [SQL Server 유틸리티 문제 해결](https://msdn.microsoft.com/library/f5f47c2a-38ea-40f8-9767-9bc138d14453)을 참조하세요.  
  
> [!IMPORTANT]  
>  관리되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 있는 "유틸리티 정보" 컬렉션 집합의 속성은 변경하면 안 되며, 데이터 컬렉션은 유틸리티 에이전트 작업에 의해 제어되므로 데이터 컬렉션을 수동으로 설정/해제하면 안 됩니다.  
  
 인스턴스 등록 마법사를 완료한 다음 SSMS의 **유틸리티 탐색기 탐색** 창에서 **관리되는 인스턴스** 노드를 클릭합니다. 등록된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스는 **유틸리티 탐색기 내용** 창의 목록 뷰에 표시됩니다.  
  
 데이터 수집 프로세스는 즉시 시작되지만 최대 30분이 지나야 유틸리티 탐색기 내용 창의 대시보드와 뷰포인트에 데이터가 표시되기 시작합니다. 데이터 수집은 15분마다 한 번씩 수행됩니다. 데이터를 새로 고치려면 **유틸리티 탐색기 탐색** 창의 **관리되는 인스턴스** 노드를 마우스 오른쪽 단추로 클릭한 다음 **새로 고침**을 선택하거나 목록 뷰에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 이름을 마우스 오른쪽 단추로 클릭한 다음 **새로 고침**을 선택합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티에서 관리되는 인스턴스를 제거하려면 **유틸리티 탐색기 탐색** 창에서 **관리되는 인스턴스** 를 선택하여 목록 뷰에 관리되는 인스턴스를 표시한 다음 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티 탐색기 내용 **목록 뷰에서** 인스턴스 이름을 마우스 오른쪽 단추로 클릭하고 **관리되지 않는 인스턴스로 설정**을 선택합니다.  
  
##  <a name="PowerShell_enroll"></a> PowerShell을 사용하여 SQL Server 인스턴스 등록  
 다음 예를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 기존 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티에 등록할 수 있습니다.  
  
```  
> $UtilityInstance = new-object -Type Microsoft.SqlServer.Management.Smo.Server "ComputerName\UCP-Name";  
> $SqlStoreConnection = new-object -Type Microsoft.SqlServer.Management.Sdk.Sfc.SqlStoreConnection $UtilityInstance.ConnectionContext.SqlConnectionObject;  
> $Utility = [Microsoft.SqlServer.Management.Utility.Utility]::Connect($SqlStoreConnection);  
> $Instance = new-object -Type Microsoft.SqlServer.Management.Smo.Server "ComputerName\ManagedInstanceName";  
> $InstanceConnection = new-object -Type Microsoft.SqlServer.Management.Sdk.Sfc.SqlStoreConnection $Instance.ConnectionContext.SqlConnectionObject;  
> $ManagedInstance = $Utility.EnrollInstance($InstanceConnection, "ProxyAccount", "ProxyPassword");  
```  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 유틸리티 기능 및 태스크](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)   
 [SQL Server 유틸리티에서 SQL Server 인스턴스 모니터링](../../relational-databases/manage/monitor-instances-of-sql-server-in-the-sql-server-utility.md)   
 [SQL Server 유틸리티 문제 해결](https://msdn.microsoft.com/library/f5f47c2a-38ea-40f8-9767-9bc138d14453)  
  
  
