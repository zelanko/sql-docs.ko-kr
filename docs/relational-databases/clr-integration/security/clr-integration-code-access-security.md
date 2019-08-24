---
title: CLR 통합 코드 액세스 보안 | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
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
ms.openlocfilehash: f49968392dd813b48f43e5e63586fd0c6bec71d8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68118523"
---
# <a name="clr-integration-code-access-security"></a>CLR 통합 코드 액세스 보안
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  CLR(공용 언어 런타임)은 관리 코드에 대해 코드 액세스 보안이라는 보안 모델을 지원합니다. 이 모델에서는 코드 ID를 기반으로 어셈블리에 사용 권한이 부여됩니다. 자세한 내용은 .NET Framework 소프트웨어 개발 키트의 "코드 액세스 보안" 섹션을 참조하십시오.  
  
 어셈블리에 부여되는 사용 권한을 결정하는 보안 정책은 다음 세 위치에서 정의됩니다.  
  
-   컴퓨터 정책: 컴퓨터에서 실행 되는 모든 관리 코드에는 정책 적용입니다 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 설치 됩니다.  
  
-   사용자 정책: 이 프로세스에 의해 호스팅되는 관리 되는 코드에 적용 되는 정책입니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 대한 사용자 정책은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서비스가 실행되는 Windows 계정과 관련이 있습니다.  
  
-   호스트 정책: CLR의 호스트를 통해 설정 하는 정책입니다 (이 예제의 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]) 해당 호스트에서 실행 하는 관리 코드에 적용 되는 합니다.  
  
 CLR에서 지원되는 코드 액세스 보안 메커니즘은 런타임에서 완전히 신뢰할 수 있는 코드와 부분적으로 신뢰할 수 있는 코드를 모두 호스팅할 수 있다는 가정을 기반으로 합니다. CLR 코드 액세스 보안으로 보호 되는 리소스를 리소스에 대 한 액세스를 허용 하기 전에 해당 권한이 필요로 하는 관리 되는 응용 프로그램 프로그래밍 인터페이스에서 일반적으로 래핑됩니다. 사용 권한 요청은 호출 스택의 어셈블리 수준에 있는 모든 호출자가 해당 리소스 사용 권한을 가지고 있는 경우에만 충족됩니다.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 내부에서 실행할 때 관리 코드에 부여되는 코드 액세스 보안 권한 집합은 위의 세 정책 수준에 의해 부여되는 권한 집합의 교집합입니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]가 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 로드된 어셈블리에 권한 집합을 부여하는 경우에도 사용자 코드에 부여되는 최종 권한 집합은 사용자 및 컴퓨터 수준 정책에 의해 보다 제한될 수 있습니다.  
  
## <a name="sql-server-host-policy-level-permission-sets"></a>SQL Server 호스트 정책 수준 권한 집합  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 호스트 정책 수준에서 어셈블리에 부여하는 코드 액세스 보안 권한 집합은 어셈블리를 만들 때 지정된 권한 집합에 의해 결정됩니다. 세 가지 권한 집합을 가지 있습니다. **안전한**, **EXTERNAL_ACCESS** 및 **UNSAFE** (사용 하 여 지정 합니다 **PERMISSION_SET** 옵션 [CREATE ASSEMBLY &#40; Transact-SQL&#41;](../../../t-sql/statements/create-assembly-transact-sql.md)).  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서는 CLR을 호스팅하는 동안 호스트 수준 보안 정책을 CLR에 제공합니다. 이 정책은 항상 적용되는 두 가지 정책 수준 아래에 있는 추가 정책 수준입니다. 이 정책은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 만든 모든 애플리케이션 도메인에 대해 설정됩니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 CLR 인스턴스를 만들 때 적용되는 기본 애플리케이션 도메인에는 이 정책이 사용되지 않습니다.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 호스트 수준 정책은 시스템 어셈블리에 대한 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 고정 정책과 사용자 어셈블리에 대한 사용자 지정 정책을 조합한 것입니다.  
  
 CLR 어셈블리 및 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 시스템 어셈블리에 대한 고정 정책은 완전 신뢰를 부여합니다.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 호스트 정책에서 사용자 지정 부분은 어셈블리 소유자가 각 어셈블리에 대한 3가지 권한 집합 중 어떤 것을 지정하는지에 따라 달라집니다. 아래에 나열된 보안 권한에 대한 자세한 내용은 .NET Framework SDK를 참조하십시오.  
  
### <a name="safe"></a>SAFE  
 내부 계산 및 로컬 데이터 액세스만 허용됩니다. **안전한** 는 가장 제한적인 권한 집합입니다. 코드를 사용 하 여 어셈블리에서 실행 **안전한** 권한을 파일, 네트워크, 환경 변수 또는 레지스트리 같은 외부 시스템 리소스에 액세스할 수 없습니다.  
  
 **안전한** 어셈블리 사용 권한 및 값은:  
  
|사용 권한|값/설명|  
|----------------|-----------------------------|  
|**SecurityPermission**|**실행:** 관리 되는 코드를 실행할 수 있는 권한입니다.|  
|**SqlClientPermission**|**컨텍스트 연결 = true**하십시오 **컨텍스트 연결 = yes**: 컨텍스트 연결만 사용할 수 있으며 연결 문자열의 값에만 지정할 수 있습니다만 "컨텍스트 연결 = true" 또는 "컨텍스트 연결 = yes"입니다.<br /><br /> **AllowBlankPassword = false.**  빈 암호는 허용 되지 않습니다.|  
  
### <a name="external_access"></a>EXTERNAL_ACCESS  
 EXTERNAL_ACCESS 어셈블리와 동일한 권한을 갖습니다 **안전한** 어셈블리 파일, 네트워크, 환경 변수 및 레지스트리와 같은 외부 시스템 리소스에 액세스 하는 추가 기능이 있습니다.  
  
 **EXTERNAL_ACCESS** 어셈블리에는 또한 다음 사용 권한 및 값에:  
  
|사용 권한|값/설명|  
|----------------|-----------------------------|  
|**DistributedTransactionPermission**|**무제한:** 분산된 트랜잭션이 허용 됩니다.|  
|**DNSPermission**|**무제한:** 도메인 이름 서버에서 정보를 요청 하는 권한입니다.|  
|**EnvironmentPermission**|**무제한:** 시스템 및 사용자 환경 변수에 대 한 전체 액세스가 허용 됩니다.|  
|**EventLogPermission**|**관리:** 다음 작업을 허용할지: 이벤트 원본 만들기, 이벤트 원본 또는 이벤트를 수신 하 고 모든 이벤트 로그의 컬렉션에 액세스 하는 이벤트 로그 지우기, 엔트리에 응답 로그 삭제, 기존 로그 읽기.|  
|**FileIOPermission**|**무제한:** 파일 및 폴더에 대 한 전체 액세스가 허용 됩니다.|  
|**KeyContainerPermission**|**무제한:** 키 컨테이너에 대 한 전체 액세스가 허용 됩니다.|  
|**NetworkInformationPermission**|**액세스:** Ping을 실행이 허용 됩니다.|  
|**RegistryPermission**|에 대 한 읽기 권한을 허용 **HKEY_CLASSES_ROOT**, **HKEY_LOCAL_MACHINE**합니다 **HKEY_CURRENT_USER**를 **HKEY_CURRENT_CONFIG**, 및  **HKEY_USERS 합니다.**|  
|**SecurityPermission**|**어설션:** 이 코드의 모든 호출자에 게 작업에 대 한 필수 권한이 있다고 어설션하 기능입니다.<br /><br /> **ControlPrincipal:** 보안 주체 개체를 조작 하는 기능입니다.<br /><br /> **실행:** 관리 되는 코드를 실행할 수 있는 권한입니다.<br /><br /> **하십시오.** Serialization 서비스를 제공할 수 있습니다.|  
|**SmtpPermission**|**액세스:** SMTP 호스트 포트 25에 아웃 바운드 연결이 허용 됩니다.|  
|**SocketPermission**|**연결 합니다.** 아웃 바운드 연결 (모든 포트, 모든 프로토콜) 전송 주소에 대해 허용 됩니다.|  
|**SqlClientPermission**|**무제한:** 데이터 원본에 대 한 전체 액세스가 허용 됩니다.|  
|**StorePermission**|**무제한:** X.509 인증서 저장소에 대 한 전체 액세스가 허용 됩니다.|  
|**WebPermission**|**연결 합니다.** 웹 리소스에 대 한 아웃 바운드 연결 허용 됩니다.|  
  
### <a name="unsafe"></a>UNSAFE  
 UNSAFE는 어셈블리에 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 내부 및 외부의 리소스에 대한 무제한적인 액세스를 제공합니다. 내에서 실행 되는 코드를 **UNSAFE** 어셈블리는 관리 되지 않는 코드를 호출할 수도 있습니다.  
  
 **안전 하지 않은** 어셈블리에 지정 됩니다 **FullTrust**합니다.  
  
> [!IMPORTANT]  
>  **안전한** 외부 리소스에 액세스 하지 않고 계산 및 데이터 관리 태스크를 수행 하는 어셈블리에 대 한 권장 되는 권한 설정 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]합니다. **EXTERNAL_ACCESS** 외부 리소스에 액세스 하는 어셈블리에 대 한 것이 좋습니다 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]합니다. **EXTERNAL_ACCESS** 어셈블리는 기본적으로 실행 된 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서비스 계정입니다. 있기 **EXTERNAL_ACCESS** 명시적으로 호출자의 Windows 인증 보안 컨텍스트를 가장 하는 코드입니다. 기본으로 실행 하는 것 이므로 합니다 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서비스 계정으로 실행할 수 있는 권한이 **EXTERNAL_ACCESS** 서비스 계정으로 실행 하도록 신뢰할 수 있는 로그인에만 부여 해야 합니다. 보안 관점에서는 **EXTERNAL_ACCESS** 하 고 **UNSAFE** 어셈블리가 동일 합니다. 그러나 **EXTERNAL_ACCESS** 에 없는 다양 한 안정성 및 견고성 보호 기능을 제공 하는 어셈블리 **UNSAFE** 어셈블리입니다. 지정 **UNSAFE** 에 대해 잘못 된 작업을 수행 하는 어셈블리에 코드를 허용 합니다 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 공간을 처리 하 고 따라서 잠재적으로 손상 시킬 수 있습니다 견고성과 확장성을 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. CLR 어셈블리를 만드는 방법에 대 한 자세한 내용은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]를 참조 하세요 [CLR 통합 어셈블리 관리](../../../relational-databases/clr-integration/assemblies/managing-clr-integration-assemblies.md)합니다.  
  
## <a name="accessing-external-resources"></a>외부 리소스 액세스  
 사용자 정의 형식 (UDT), 저장된 프로시저 또는 다른 유형의 구문 어셈블리가 등록 되어 있으면 합니다 **안전** , 사용 권한 집합을 외부 리소스에 액세스할 수 없는 구문에서 관리 되는 코드를 실행 합니다. 그러나 경우 합니다 **EXTERNAL_ACCESS** 또는 **UNSAFE** 권한 집합이 지정 되 고 관리 코드가 외부 리소스에 액세스 하려고 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 다음 규칙을 적용 합니다.  
  
|If|작업|  
|--------|----------|  
|실행 컨텍스트가 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 로그인에 해당합니다.|외부 리소스에 액세스하려고 하면 거부되고 보안 예외가 발생합니다.|  
|실행 컨텍스트가 Windows 로그인에 해당하고 원래 호출자입니다.|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서비스 계정의 보안 컨텍스트에서 외부 리소스가 액세스됩니다.|  
|호출자가 원래 호출자가 아닙니다.|액세스가 거부되고 보안 예외가 발생합니다.|  
|실행 컨텍스트가 Windows 로그인에 해당하고 원래 호출자인데 호출자를 가장했습니다.|서비스 계정이 아니라 호출자 보안 컨텍스트가 액세스에 사용됩니다.|  
  
## <a name="permission-set-summary"></a>권한 집합 요약  
 다음 차트에 부여 된 사용 권한과 제한을 요약 합니다 **안전한**, **EXTERNAL_ACCESS**, 및 **UNSAFE** 권한 집합입니다.  
  
|||||  
|-|-|-|-|  
||**SAFE**|**EXTERNAL_ACCESS**|**UNSAFE**|  
|**코드 액세스 보안 권한**|실행 전용|실행 및 외부 리소스 액세스|제한 없음(P/Invoke 포함)|  
|**프로그래밍 모델 제한 사항**|사용자 계정 컨트롤|사용자 계정 컨트롤|제한 없음|  
|**안정성 요구 사항**|사용자 계정 컨트롤|예|아니요|  
|**로컬 데이터 액세스**|사용자 계정 컨트롤|예|사용자 계정 컨트롤|  
|**네이티브 코드를 호출 하는 기능**|아니요|아니요|사용자 계정 컨트롤|  
  
## <a name="see-also"></a>관련 항목  
 [CLR 통합 보안](../../../relational-databases/clr-integration/security/clr-integration-security.md)   
 [호스트 보호 특성 및 CLR 통합 프로그래밍](../../../relational-databases/clr-integration-security-host-protection-attributes/host-protection-attributes-and-clr-integration-programming.md)   
 [CLR 통합 프로그래밍 모델 제한 사항](../../../relational-databases/clr-integration/database-objects/clr-integration-programming-model-restrictions.md)   
 [CLR 호스팅 환경](../../../relational-databases/clr-integration/clr-integration-architecture-clr-hosted-environment.md)  
  
  
