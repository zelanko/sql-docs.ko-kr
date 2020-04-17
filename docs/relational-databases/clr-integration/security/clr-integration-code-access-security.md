---
title: CLR 통합 코드 액세스 보안 | 마이크로 소프트 문서
description: SQL Server CLR 통합의 경우 CLR은 코드 ID를 기반으로 어셈블리에 사용 권한이 부여된 관리 코드에 대한 코드 액세스 보안을 지원합니다.
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
ms.openlocfilehash: 912db3acb6f6dc21952e99da31a1484a9745ed0b
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2020
ms.locfileid: "81488316"
---
# <a name="clr-integration-code-access-security"></a>CLR 통합 코드 액세스 보안
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  CLR(공용 언어 런타임)은 관리 코드에 대해 코드 액세스 보안이라는 보안 모델을 지원합니다. 이 모델에서는 코드 ID를 기반으로 어셈블리에 사용 권한이 부여됩니다. 자세한 내용은 .NET Framework 소프트웨어 개발 키트의 "코드 액세스 보안" 섹션을 참조하십시오.  
  
 어셈블리에 부여되는 사용 권한을 결정하는 보안 정책은 다음 세 위치에서 정의됩니다.  
  
-   컴퓨터 정책: [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]가 설치된 컴퓨터에서 실행되는 모든 관리 코드에 적용되는 정책입니다.  
  
-   사용자 정책: 프로세스에서 호스팅하는 관리 코드에 적용되는 정책입니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 대한 사용자 정책은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서비스가 실행되는 Windows 계정과 관련이 있습니다.  
  
-   호스트 정책: CLR 호스트(이 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)])에 의해 설정되는 정책입니다. 이 정책은 해당 호스트에서 실행되는 관리 코드에 적용됩니다.  
  
 CLR에서 지원되는 코드 액세스 보안 메커니즘은 런타임에서 완전히 신뢰할 수 있는 코드와 부분적으로 신뢰할 수 있는 코드를 모두 호스팅할 수 있다는 가정을 기반으로 합니다. CLR 코드 액세스 보안을 통해 보호되는 리소스는 일반적으로 이 리소스에 대한 액세스를 허용하기 전에 먼저 해당 사용 권한을 요구하는 관리되는 응용 프로그래밍 인터페이스에 의해 래핑됩니다. 사용 권한 요청은 호출 스택의 어셈블리 수준에 있는 모든 호출자가 해당 리소스 사용 권한을 가지고 있는 경우에만 충족됩니다.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 내부에서 실행할 때 관리 코드에 부여되는 코드 액세스 보안 권한 집합은 위의 세 정책 수준에 의해 부여되는 권한 집합의 교집합입니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]가 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 로드된 어셈블리에 권한 집합을 부여하는 경우에도 사용자 코드에 부여되는 최종 권한 집합은 사용자 및 컴퓨터 수준 정책에 의해 보다 제한될 수 있습니다.  
  
## <a name="sql-server-host-policy-level-permission-sets"></a>SQL Server 호스트 정책 수준 권한 집합  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 호스트 정책 수준에서 어셈블리에 부여하는 코드 액세스 보안 권한 집합은 어셈블리를 만들 때 지정된 권한 집합에 의해 결정됩니다. 세 가지 권한 집합이 있습니다: **SAFE,** **EXTERNAL_ACCESS** 및 **안전하지** 않음(어셈블리 [만들기&#40;Transact-SQL&#41;](../../../t-sql/statements/create-assembly-transact-sql.md)만들기의 **PERMISSION_SET** 옵션을 사용하여 지정).  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서는 CLR을 호스팅하는 동안 호스트 수준 보안 정책을 CLR에 제공합니다. 이 정책은 항상 적용되는 두 가지 정책 수준 아래에 있는 추가 정책 수준입니다. 이 정책은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 만든 모든 애플리케이션 도메인에 대해 설정됩니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 CLR 인스턴스를 만들 때 적용되는 기본 애플리케이션 도메인에는 이 정책이 사용되지 않습니다.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 호스트 수준 정책은 시스템 어셈블리에 대한 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 고정 정책과 사용자 어셈블리에 대한 사용자 지정 정책을 조합한 것입니다.  
  
 CLR 어셈블리 및 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 시스템 어셈블리에 대한 고정 정책은 완전 신뢰를 부여합니다.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 호스트 정책에서 사용자 지정 부분은 어셈블리 소유자가 각 어셈블리에 대한 3가지 권한 집합 중 어떤 것을 지정하는지에 따라 달라집니다. 아래에 나열된 보안 권한에 대한 자세한 내용은 .NET Framework SDK를 참조하십시오.  
  
### <a name="safe"></a>SAFE  
 내부 계산 및 로컬 데이터 액세스만 허용됩니다. **SAFE는** 가장 제한적인 사용 권한 집합입니다. **SAFE** 권한이 있는 어셈블리에서 실행한 코드는 파일, 네트워크, 환경 변수 또는 레지스트리와 같은 외부 시스템 리소스에 액세스할 수 없습니다.  
  
 **SAFE** 어셈블리에는 다음과 같은 사용 권한과 값이 있습니다.  
  
|사용 권한|값/설명|  
|----------------|-----------------------------|  
|**SecurityPermission**|**실행:** 관리 코드를 실행할 수 있는 권한입니다.|  
|**SqlClientPermission**|**컨텍스트 연결 = true**, **컨텍스트 연결 = 예**: 컨텍스트 연결만 사용할 수 있으며 연결 문자열은 "컨텍스트 연결=true" 또는 "컨텍스트 연결=예"의 값만 지정할 수 있습니다.<br /><br /> **허용공백암호 = false:**  빈 암호는 허용되지 않습니다.|  
  
### <a name="external_access"></a>EXTERNAL_ACCESS  
 EXTERNAL_ACCESS 어셈블리에는 **SAFE** 어셈블리와 동일한 권한이 있으며 파일, 네트워크, 환경 변수 및 레지스트리와 같은 외부 시스템 리소스에 액세스할 수 있는 추가 기능이 있습니다.  
  
 **EXTERNAL_ACCESS** 어셈블리에는 다음과 같은 사용 권한과 값도 있습니다.  
  
|사용 권한|값/설명|  
|----------------|-----------------------------|  
|**DistributedTransactionPermission**|**무제한:** 분산 트랜잭션은 허용됩니다.|  
|**DNS권한**|**무제한:** 도메인 이름 서버에서 정보를 요청할 수 있는 권한입니다.|  
|**EnvironmentPermission**|**무제한:** 시스템 및 사용자 환경 변수에 대한 전체 액세스가 허용됩니다.|  
|**EventLogPermission**|**관리:** 이벤트 소스 만들기, 기존 로그 읽기, 이벤트 원본 또는 로그 삭제, 항목에 응답, 이벤트 로그 지우기, 이벤트 수신 대기, 모든 이벤트 로그 컬렉션 액세스 등의 작업이 허용됩니다.|  
|**FileIOPermission**|**무제한:** 파일 및 폴더에 대한 전체 액세스가 허용됩니다.|  
|**KeyContainerPermission**|**무제한:** 키 컨테이너에 대한 모든 액세스가 허용됩니다.|  
|**NetworkInformationPermission**|**액세스:** Ping이 허용됩니다.|  
|**RegistryPermission**|**읽기**권한을 HKEY_CLASSES_ROOT, **HKEY_LOCAL_MACHINE**, **HKEY_CURRENT_USER,** **HKEY_CURRENT_CONFIG**및 HKEY_USERS **수 있습니다.**|  
|**SecurityPermission**|**어설션:** 이 코드의 모든 호출자에게 작업에 필요한 권한이 있음을 어설션하는 기능입니다.<br /><br /> **컨트롤 교장:** 주 개체를 조작하는 기능입니다.<br /><br /> **실행:** 관리 코드를 실행할 수 있는 권한입니다.<br /><br /> **직렬화포물질:** 직렬화 서비스를 제공할 수 있는 기능입니다.|  
|**SmtpPermission**|**액세스:** SMTP 호스트 포트 25에 대한 아웃바운드 연결이 허용됩니다.|  
|**SocketPermission**|**연결:** 전송 주소의 아웃바운드 연결(모든 포트, 모든 프로토콜)은 허용됩니다.|  
|**SqlClientPermission**|**무제한:** 데이터 원본에 대한 전체 액세스가 허용됩니다.|  
|**StorePermission**|**무제한:** X.509 인증서 저장소에 대한 모든 액세스가 허용됩니다.|  
|**WebPermission**|**연결:** 웹 리소스에 대한 아웃바운드 연결이 허용됩니다.|  
  
### <a name="unsafe"></a>UNSAFE  
 UNSAFE는 어셈블리에 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 내부 및 외부의 리소스에 대한 무제한적인 액세스를 제공합니다. **안전하지 않은** 어셈블리 내에서 실행되는 코드는 관리되지 않는 코드를 호출할 수도 있습니다.  
  
 **안전하지 않은** 어셈블리에는 **FullTrust가**제공됩니다.  
  
> [!IMPORTANT]  
>  **SAFE는** 외부 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]리소스에 액세스하지 않고 계산 및 데이터 관리 작업을 수행하는 어셈블리에 권장되는 사용 권한 설정입니다. **외부리소스에** 액세스하는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]어셈블리에는 EXTERNAL_ACCESS. **EXTERNAL_ACCESS** 어셈블리는 기본적으로 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서비스 계정으로 실행됩니다. **EXTERNAL_ACCESS** 코드가 호출자의 Windows 인증 보안 컨텍스트를 명시적으로 가장할 수 있습니다. 기본값은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서비스 계정으로 실행되기 때문에 **서비스** 계정으로 실행하도록 신뢰할 수 있는 로그인에만 EXTERNAL_ACCESS 실행할 수 있는 권한을 부여해야 합니다. 보안 관점에서 **EXTERNAL_ACCESS** 안전하지 **않은** 어셈블리는 동일합니다. 그러나 **EXTERNAL_ACCESS** 어셈블리는 **안전하지 않은** 어셈블리에 없는 다양한 안정성 및 견고성 보호 기능을 제공합니다. 안전하지 **않음을** 지정하면 어셈블리의 코드가 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 프로세스 공간에 대해 잘못된 작업을 수행할 수 있으므로 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 견고성과 확장성이 손상될 수 있습니다. CLR [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]어셈블리를 만드는 데 대한 자세한 내용은 [CLR 통합 어셈블리 관리를](../../../relational-databases/clr-integration/assemblies/managing-clr-integration-assemblies.md)참조하십시오.  
  
## <a name="accessing-external-resources"></a>외부 리소스 액세스  
 사용자 정의 형식(UDT), 저장 프로시저 또는 다른 유형의 구문 어셈블리가 **SAFE** 권한 집합에 등록된 경우 구문에서 실행되는 관리 코드는 외부 리소스에 액세스할 수 없습니다. 그러나 **EXTERNAL_ACCESS** 또는 **안전하지 않은** 권한 집합을 지정하고 관리 되는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 코드가 외부 리소스에 액세스하려고 하면 다음 규칙이 적용됩니다.  
  
|다음과 같은 경우|작업|  
|--------|----------|  
|실행 컨텍스트가 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 로그인에 해당합니다.|외부 리소스에 액세스하려고 하면 거부되고 보안 예외가 발생합니다.|  
|실행 컨텍스트가 Windows 로그인에 해당하고 원래 호출자입니다.|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서비스 계정의 보안 컨텍스트에서 외부 리소스가 액세스됩니다.|  
|호출자가 원래 호출자가 아닙니다.|액세스가 거부되고 보안 예외가 발생합니다.|  
|실행 컨텍스트가 Windows 로그인에 해당하고 원래 호출자인데 호출자를 가장했습니다.|서비스 계정이 아니라 호출자 보안 컨텍스트가 액세스에 사용됩니다.|  
  
## <a name="permission-set-summary"></a>권한 집합 요약  
 다음 차트에는 **SAFE,** **EXTERNAL_ACCESS**및 **안전하지 않은** 권한 집합에 부여된 제한 및 사용 권한이 요약되어 있습니다.  
  
|||||  
|-|-|-|-|  
||**안전 금고**|**EXTERNAL_ACCESS**|**하지 않은**|  
|**코드 액세스 보안 권한**|실행 전용|실행 및 외부 리소스 액세스|제한 없음(P/Invoke 포함)|  
|**프로그래밍 모델 제한 사항**|예|예|제한 없음|  
|**안정성 요구 사항**|예|예|예|  
|**로컬 데이터 액세스**|예|예|예|  
|**네이티브 코드를 호출하는 기능**|예|예|예|  
  
## <a name="see-also"></a>참고 항목  
 [CLR 통합 보안](../../../relational-databases/clr-integration/security/clr-integration-security.md)   
 [호스트 보호 특성 및 CLR 통합 프로그래밍](../../../relational-databases/clr-integration-security-host-protection-attributes/host-protection-attributes-and-clr-integration-programming.md)   
 [CLR 통합 프로그래밍 모델 제한](../../../relational-databases/clr-integration/database-objects/clr-integration-programming-model-restrictions.md)   
 [CLR 호스팅 환경](../../../relational-databases/clr-integration/clr-integration-architecture-clr-hosted-environment.md)  
  
  
