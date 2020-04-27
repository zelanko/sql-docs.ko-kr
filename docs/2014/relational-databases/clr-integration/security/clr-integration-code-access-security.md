---
title: CLR 통합 코드 액세스 보안 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- UNSAFE assemblies
- permissions [CLR integration]
- common language runtime [SQL Server], security
- SAFE assemblies
- code access security [CLR integration]
- EXTERNAL_ACCESS assemblies
ms.assetid: 2111cfe0-d5e0-43b1-93c3-e994ac0e9729
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: d829ef131bc8772ce2d84391513ffa52b2f2ff1a
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62873736"
---
# <a name="clr-integration-code-access-security"></a>CLR 통합 코드 액세스 보안
  CLR(공용 언어 런타임)은 관리 코드에 대해 코드 액세스 보안이라는 보안 모델을 지원합니다. 이 모델에서는 코드 ID를 기반으로 어셈블리에 사용 권한이 부여됩니다. 자세한 내용은 .NET Framework 소프트웨어 개발 키트의 "코드 액세스 보안" 섹션을 참조하십시오.  
  
 어셈블리에 부여되는 사용 권한을 결정하는 보안 정책은 다음 세 위치에서 정의됩니다.  
  
-   컴퓨터 정책: [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]가 설치된 컴퓨터에서 실행되는 모든 관리 코드에 적용되는 정책입니다.  
  
-   사용자 정책: 프로세스에서 호스팅하는 관리 코드에 적용되는 정책입니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서비스가 실행 되 고 있습니다.  
  
-   호스트 정책: CLR 호스트(이 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)])에 의해 설정되는 정책입니다. 이 정책은 해당 호스트에서 실행되는 관리 코드에 적용됩니다.  
  
 CLR에서 지원되는 코드 액세스 보안 메커니즘은 런타임에서 완전히 신뢰할 수 있는 코드와 부분적으로 신뢰할 수 있는 코드를 모두 호스팅할 수 있다는 가정을 기반으로 합니다. CLR 코드 액세스 보안을 통해 보호 되는 리소스는 일반적으로 리소스에 대 한 액세스를 허용 하기 전에 해당 사용 권한을 requirethe 관리 되는 응용 프로그래밍 인터페이스에 의해 래핑됩니다. 호출 스택의 모든 호출자 (어셈블리 수준)에 해당 리소스 권한이 있는 경우에만 demandfor 권한이 충족 됩니다.  
  
 내부 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에서 실행할 때 관리 코드에 부여 되는 코드 액세스 보안 권한 집합은에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]로드 된 어셈블리에 대 한 사용 권한 집합을 부여 하 고, 사용자 코드에 제공 되는 최종 권한 집합은 사용자 및 컴퓨터 수준 정책에 의해 추가로 제한 될 수 있습니다.  
  
## <a name="sql-server-host-policy-level-permission-sets"></a>SQL Server 호스트 정책 수준 권한 집합  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 호스트 정책 수준에서 어셈블리에 부여하는 코드 액세스 보안 권한 집합은 어셈블리를 만들 때 지정된 권한 집합에 의해 결정됩니다. `SAFE`에는 세 가지 권한 집합, `EXTERNAL_ACCESS` 및 `UNSAFE` ([CREATE ASSEMBLY &#40;transact-sql&#41;](/sql/t-sql/statements/create-assembly-transact-sql)) **PERMISSION_SET** 옵션을 사용 하 여 지정 됩니다.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 CLR 인스턴스를 만들 때 적용되는 기본 애플리케이션 도메인에는 이 정책이 사용되지 않습니다.  
  
 사용자 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 어셈블리에 대 한 사용자 지정 정책 및 시스템 어셈블리에 대 한 fixedpolicy입니다.  
  
 CLR 어셈블리 및 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 시스템 어셈블리에 대한 고정 정책은 완전 신뢰를 부여합니다.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 호스트 정책에서 사용자 지정 부분은 어셈블리 소유자가 각 어셈블리에 대한 3가지 권한 집합 중 어떤 것을 지정하는지에 따라 달라집니다. 아래에 나열된 보안 권한에 대한 자세한 내용은 .NET Framework SDK를 참조하십시오.  
  
### <a name="safe"></a>SAFE  
 내부 계산 및 로컬 데이터 액세스만 허용됩니다. `SAFE`는 가장 제한적인 권한 집합입니다. `SAFE` 권한을 사용하여 어셈블리에서 실행한 코드는 파일, 네트워크, 환경 변수 또는 레지스트리와 같은 외부 시스템 리소스에 액세스할 수 없습니다.  
  
 `SAFE` 어셈블리는 다음과 같은 사용 권한 및 값을 갖습니다.  
  
|사용 권한|값/설명|  
|----------------|-----------------------------|  
|`SecurityPermission`|`Execution:` 관리 코드를 실행하는 데 필요한 권한입니다.|  
|`SqlClientPermission`|`Context connection = true`, `context connection = yes`: 컨텍스트 연결만 사용할 수 있으며 연결 문자열은 "context connection=true" 또는 "context connection=yes" 값만 지정할 수 있습니다.<br /><br /> **AllowBlankPassword = false:**  빈 암호는 허용 되지 않습니다.|  
  
### <a name="external_access"></a>EXTERNAL_ACCESS  
 EXTERNAL_ACCESS 어셈블리에는 파일, 네트워크 `SAFE` , 환경 변수 및 레지스트리와 같은 외부 시스템 리소스에 액세스 하는 추가 기능을 사용 하 여 어셈블리와 동일한 사용 권한이 있습니다.  
  
 또한 `EXTERNAL_ACCESS` 어셈블리는 다음과 같은 사용 권한 및 값을 갖습니다.  
  
|사용 권한|값/설명|  
|----------------|-----------------------------|  
|`DistributedTransactionPermission`|`Unrestricted:`분산 트랜잭션이 허용 됩니다.|  
|`DNSPermission`|`Unrestricted:`도메인 이름 서버에서 정보를 요청할 수 있는 권한입니다.|  
|`EnvironmentPermission`|`Unrestricted:` 시스템 및 사용자 환경 변수에 대한 모든 액세스 권한이 허용됩니다.|  
|`EventLogPermission`|`Administer:` 이벤트 원본 만들기, 기존 로그 읽기, 이벤트 원본 또는 로그 삭제, 엔트리에 응답, 이벤트 로그 지우기, 이벤트 수신, 모든 이벤트 로그 컬렉션에 액세스 등의 동작이 허용됩니다.|  
|`FileIOPermission`|`Unrestricted:` 파일 및 폴더에 대한 모든 액세스 권한이 허용됩니다.|  
|`KeyContainerPermission`|`Unrestricted:` 키 컨테이너에 대한 모든 액세스 권한이 허용됩니다.|  
|`NetworkInformationPermission`|`Access:` Ping 수행이 허용됩니다.|  
|`RegistryPermission`|`HKEY_CLASSES_ROOT`, `HKEY_LOCAL_MACHINE`, `HKEY_CURRENT_USER`, `HKEY_CURRENT_CONFIG` 및 `HKEY_USERS.`에 대한 읽기 권한을 허용합니다.|  
|`SecurityPermission`|`Assertion:` 이 코드의 모든 호출자에게 작업에 대한 필수 권한이 있다고 어설션하는 기능입니다.<br /><br /> `ControlPrincipal:` 보안 주체 개체를 조작하는 기능입니다.<br /><br /> `Execution:` 관리 코드를 실행하는 데 필요한 권한입니다.<br /><br /> `SerializationFormatter:` 직렬화 서비스를 제공하는 기능입니다.|  
|**SmtpPermission**|`Access:` SMTP 호스트 포트 25에 대한 아웃바운드 연결이 허용됩니다.|  
|`SocketPermission`|`Connect:` 전송 주소에 대해 아웃바운드 연결(모든 포트, 모든 프로토콜)이 허용됩니다.|  
|`SqlClientPermission`|`Unrestricted:` 데이터 원본에 대한 모든 액세스 권한이 허용됩니다.|  
|`StorePermission`|`Unrestricted:` X.509 인증서 저장소에 대한 모든 액세스 권한이 허용됩니다.|  
|`WebPermission`|`Connect:` 웹 리소스에 대한 아웃바운드 연결이 허용됩니다.|  
  
### <a name="unsafe"></a>UNSAFE  
 UNSAFE는 어셈블리에 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 내부 및 외부의 리소스에 대한 무제한적인 액세스를 제공합니다. `UNSAFE` 어셈블리 내에서 실행되는 코드는 비관리 코드를 호출할 수도 있습니다.  
  
 `UNSAFE` 어셈블리에는 `FullTrust`가 부여됩니다.  
  
> [!IMPORTANT]  
>  `SAFE`는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스의 외부 리소스에 액세스하지 않고 계산 및 데이터 관리 태스크를 수행하는 어셈블리에 권장되는 사용 권한 설정입니다. `EXTERNAL_ACCESS`기본적으로 어셈블리는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서비스 계정으로 실행 됩니다. 실행할 `EXTERNAL_ACCESS` 권한은 서비스 계정으로 실행 하도록 신뢰할 수 있는 로그인에만 부여 해야 합니다. 보안 측면에서 `EXTERNAL_ACCESS` 및 `UNSAFE` 어셈블리는 같습니다. 그러나 `EXTERNAL_ACCESS` 어셈블리는 `UNSAFE` 어셈블리에 없는 다양한 안정성 및 견고성 보호 기능을 제공합니다. 를 `UNSAFE` 지정 하면 어셈블리의 코드가에 대해 잘못 된 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]작업을 수행할 수 있습니다. 에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]clr 어셈블리를 만드는 방법에 대 한 자세한 내용은 [Clr 통합 어셈블리 관리](../../../relational-databases/clr-integration/assemblies/managing-clr-integration-assemblies.md)를 참조 하세요.  
  
## <a name="accessing-external-resources"></a>외부 리소스 액세스  
 UDT(사용자 정의 형식), 저장 프로시저 또는 다른 유형의 구문 어셈블리가 `SAFE` 권한 집합에 등록되어 있으면 구문에서 실행되는 관리 코드가 외부 리소스에 액세스할 수 없습니다. 하지만 `EXTERNAL_ACCESS` 또는 `UNSAFE` 권한 집합이 지정된 경우 관리 코드가 외부 리소스에 액세스하려고 하면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 다음 규칙을 적용합니다.  
  
|다음과 같은 경우|작업|  
|--------|----------|  
|실행 컨텍스트가 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 로그인에 해당합니다.|외부 리소스에 액세스하려고 하면 거부되고 보안 예외가 발생합니다.|  
|실행 컨텍스트가 Windows 로그인에 해당하고 원래 호출자입니다.|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서비스 계정의 보안 컨텍스트에서 외부 리소스가 액세스됩니다.|  
|호출자가 원래 호출자가 아닙니다.|액세스가 거부되고 보안 예외가 발생합니다.|  
|실행 컨텍스트가 Windows 로그인에 해당하고 원래 호출자인데 호출자를 가장했습니다.|서비스 계정이 아니라 호출자 보안 컨텍스트가 액세스에 사용됩니다.|  
  
## <a name="permission-set-summary"></a>권한 집합 요약  
 다음 차트에서는 `SAFE`, `EXTERNAL_ACCESS` 및 `UNSAFE` 권한 집합에 부여되는 사용 권한과 제한을 요약하여 보여 줍니다.  
  
|||||  
|-|-|-|-|  
||`SAFE`|`EXTERNAL_ACCESS`|`UNSAFE`|  
|`Code Access Security Permissions`|실행 전용|실행 및 외부 리소스 액세스|제한 없음(P/Invoke 포함)|  
|`Programming model restrictions`|예|예|제한 없음|  
|`Verifiability requirement`|예|예|예|  
|`Local data access`|예|예|예|  
|`Ability to call native code`|아니요|예|예|  
  
## <a name="see-also"></a>참고 항목  
 [CLR 통합 보안](clr-integration-security.md)   
 [호스트 보호 특성 및 CLR 통합 프로그래밍](../../clr-integration-security-host-protection-attributes/host-protection-attributes-and-clr-integration-programming.md)   
 [CLR 통합 프로그래밍 모델 제한 사항](../../../relational-databases/clr-integration/database-objects/clr-integration-programming-model-restrictions.md)   
 [CLR 호스팅 환경](../clr-integration-architecture-clr-hosted-environment.md)  
  
  
