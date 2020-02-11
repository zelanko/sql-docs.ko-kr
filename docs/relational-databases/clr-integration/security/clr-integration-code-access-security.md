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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68118523"
---
# <a name="clr-integration-code-access-security"></a>CLR 통합 코드 액세스 보안
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  CLR(공용 언어 런타임)은 관리 코드에 대해 코드 액세스 보안이라는 보안 모델을 지원합니다. 이 모델에서는 코드 ID를 기반으로 어셈블리에 사용 권한이 부여됩니다. 자세한 내용은 .NET Framework 소프트웨어 개발 키트의 "코드 액세스 보안" 섹션을 참조하십시오.  
  
 어셈블리에 부여되는 사용 권한을 결정하는 보안 정책은 다음 세 위치에서 정의됩니다.  
  
-   컴퓨터 정책: [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]가 설치된 컴퓨터에서 실행되는 모든 관리 코드에 적용되는 정책입니다.  
  
-   사용자 정책: 프로세스에서 호스팅하는 관리 코드에 적용되는 정책입니다. 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 대한 사용자 정책은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서비스가 실행되는 Windows 계정과 관련이 있습니다.  
  
-   호스트 정책: CLR 호스트(이 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)])에 의해 설정되는 정책입니다. 이 정책은 해당 호스트에서 실행되는 관리 코드에 적용됩니다.  
  
 CLR에서 지원되는 코드 액세스 보안 메커니즘은 런타임에서 완전히 신뢰할 수 있는 코드와 부분적으로 신뢰할 수 있는 코드를 모두 호스팅할 수 있다는 가정을 기반으로 합니다. CLR 코드 액세스 보안을 통해 보호되는 리소스는 일반적으로 이 리소스에 대한 액세스를 허용하기 전에 먼저 해당 사용 권한을 요구하는 관리되는 응용 프로그래밍 인터페이스에 의해 래핑됩니다. 사용 권한 요청은 호출 스택의 어셈블리 수준에 있는 모든 호출자가 해당 리소스 사용 권한을 가지고 있는 경우에만 충족됩니다.  
  
 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 내부에서 실행할 때 관리 코드에 부여되는 코드 액세스 보안 권한 집합은 위의 세 정책 수준에 의해 부여되는 권한 집합의 교집합입니다. 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]가 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 로드된 어셈블리에 권한 집합을 부여하는 경우에도 사용자 코드에 부여되는 최종 권한 집합은 사용자 및 컴퓨터 수준 정책에 의해 보다 제한될 수 있습니다.  
  
## <a name="sql-server-host-policy-level-permission-sets"></a>SQL Server 호스트 정책 수준 권한 집합  
 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 호스트 정책 수준에서 어셈블리에 부여하는 코드 액세스 보안 권한 집합은 어셈블리를 만들 때 지정된 권한 집합에 의해 결정됩니다. 권한 집합에는 **SAFE**, **EXTERNAL_ACCESS** 및 **UNSAFE** ( [CREATE ASSEMBLY &#40;transact-sql&#41;](../../../t-sql/statements/create-assembly-transact-sql.md)의 **PERMISSION_SET** 옵션을 사용 하 여 지정) 세 가지가 있습니다.  
  
 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서는 CLR을 호스팅하는 동안 호스트 수준 보안 정책을 CLR에 제공합니다. 이 정책은 항상 적용되는 두 가지 정책 수준 아래에 있는 추가 정책 수준입니다. 이 정책은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 만든 모든 애플리케이션 도메인에 대해 설정됩니다. 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 CLR 인스턴스를 만들 때 적용되는 기본 애플리케이션 도메인에는 이 정책이 사용되지 않습니다.  
  
 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 호스트 수준 정책은 시스템 어셈블리에 대한 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 고정 정책과 사용자 어셈블리에 대한 사용자 지정 정책을 조합한 것입니다.  
  
 CLR 어셈블리 및 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 시스템 어셈블리에 대한 고정 정책은 완전 신뢰를 부여합니다.  
  
 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 호스트 정책에서 사용자 지정 부분은 어셈블리 소유자가 각 어셈블리에 대한 3가지 권한 집합 중 어떤 것을 지정하는지에 따라 달라집니다. 아래에 나열된 보안 권한에 대한 자세한 내용은 .NET Framework SDK를 참조하십시오.  
  
### <a name="safe"></a>SAFE  
 내부 계산 및 로컬 데이터 액세스만 허용됩니다. **SAFE** 는 가장 제한적인 권한 집합입니다. **SAFE** 권한이 있는 어셈블리에 의해 실행 되는 코드는 파일, 네트워크, 환경 변수 또는 레지스트리와 같은 외부 시스템 리소스에 액세스할 수 없습니다.  
  
 **SAFE** 어셈블리에는 다음과 같은 사용 권한 및 값이 있습니다.  
  
|사용 권한|값/설명|  
|----------------|-----------------------------|  
|**SecurityPermission**|**실행:** 관리 코드를 실행할 수 있는 권한입니다.|  
|**System.data.sqlclient.sqlclientpermission**|**Context connection = true**, **context connection = yes**: 컨텍스트 연결만 사용할 수 있으며 연결 문자열은 "context connection = true" 또는 "context connection = yes" 값만 지정할 수 있습니다.<br /><br /> **AllowBlankPassword = false:**  빈 암호는 허용 되지 않습니다.|  
  
### <a name="external_access"></a>EXTERNAL_ACCESS  
 EXTERNAL_ACCESS 어셈블리는 파일, 네트워크, 환경 변수 및 레지스트리와 같은 외부 시스템 리소스에 액세스 하는 추가 기능을 통해 **안전한** 어셈블리와 동일한 사용 권한을 갖습니다.  
  
 **EXTERNAL_ACCESS** 어셈블리에는 다음과 같은 사용 권한 및 값도 있습니다.  
  
|사용 권한|값/설명|  
|----------------|-----------------------------|  
|**DistributedTransactionPermission**|**제한 없음:** 분산 트랜잭션이 허용 됩니다.|  
|**DNSPermission**|**제한 없음:** 도메인 이름 서버에서 정보를 요청할 수 있는 권한입니다.|  
|**환경 권한**|**제한 없음:** 시스템 및 사용자 환경 변수에 대 한 모든 액세스 권한이 허용 됩니다.|  
|**EventLogPermission**|**관리:** 이벤트 원본 만들기, 기존 로그 읽기, 이벤트 원본 또는 로그 삭제, 엔트리에 응답, 이벤트 로그 지우기, 이벤트 수신, 모든 이벤트 로그 컬렉션에 액세스 등의 작업을 수행할 수 있습니다.|  
|**FileIOPermission**|**제한 없음:** 파일 및 폴더에 대 한 모든 액세스 권한이 허용 됩니다.|  
|**KeyContainerPermission**|**제한 없음:** 키 컨테이너에 대 한 모든 액세스 권한이 허용 됩니다.|  
|**NetworkInformationPermission**|**액세스:** Ping은 허용 됩니다.|  
|**RegistryPermission**|**HKEY_CLASSES_ROOT**, **HKEY_LOCAL_MACHINE**, **HKEY_CURRENT_USER**, **HKEY_CURRENT_CONFIG**및 HKEY_USERS에 대 한 읽기 권한을 허용 **합니다.**|  
|**SecurityPermission**|**어설션:** 이 코드의 모든 호출자에 게 작업에 대 한 필수 권한이 있음을 어설션 하는 기능입니다.<br /><br /> **Controlprincipal:** Principal 개체를 조작 하는 기능입니다.<br /><br /> **실행:** 관리 코드를 실행할 수 있는 권한입니다.<br /><br /> **SerializationFormatter:** Serialization 서비스를 제공 하는 기능.|  
|**SmtpPermission**|**액세스:** SMTP 호스트 포트 25에 대 한 아웃 바운드 연결이 허용 됩니다.|  
|**SocketPermission**|**연결:** 전송 주소에 대 한 아웃 바운드 연결 (모든 포트, 모든 프로토콜)이 허용 됩니다.|  
|**System.data.sqlclient.sqlclientpermission**|**제한 없음:** 데이터 원본에 대 한 모든 액세스 권한이 허용 됩니다.|  
|**에 대 한 권한**|**제한 없음:** X.509 인증서 저장소에 대 한 모든 액세스 권한이 허용 됩니다.|  
|**WebPermission**|**연결:** 웹 리소스에 대 한 아웃 바운드 연결이 허용 됩니다.|  
  
### <a name="unsafe"></a>UNSAFE  
 UNSAFE는 어셈블리에 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 내부 및 외부의 리소스에 대한 무제한적인 액세스를 제공합니다. **UNSAFE** 어셈블리 내에서 실행 되는 코드는 비관리 코드를 호출할 수도 있습니다.  
  
 **안전 하지 않은** 어셈블리에는 **FullTrust**가 지정 됩니다.  
  
> [!IMPORTANT]  
>  **SAFE** 는 외부 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]리소스에 액세스 하지 않고 계산 및 데이터 관리 작업을 수행 하는 어셈블리에 권장 되는 권한 설정입니다. **** 외부 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]리소스에 액세스 하는 어셈블리에는 EXTERNAL_ACCESS를 사용 하는 것이 좋습니다. **EXTERNAL_ACCESS** 어셈블리는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 기본적으로 서비스 계정으로 실행 됩니다. **EXTERNAL_ACCESS** 코드에서 호출자의 Windows 인증 보안 컨텍스트를 명시적으로 가장할 수 있습니다. 기본값은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서비스 계정으로 실행 하기 때문에 **EXTERNAL_ACCESS** 실행 권한은 서비스 계정으로 실행 하도록 신뢰할 수 있는 로그인에만 부여 해야 합니다. 보안 관점에서 **EXTERNAL_ACCESS** 와 **안전 하지 않은** 어셈블리는 동일 합니다. 그러나 **EXTERNAL_ACCESS** 어셈블리는 **안전** 하지 않은 어셈블리에 없는 다양 한 안정성 및 견고성 보호 기능을 제공 합니다. **UNSAFE** 를 지정 하면 어셈블리의 코드가 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 프로세스 공간에 대해 잘못 된 작업을 수행할 수 있으므로의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]견고성과 확장성이 손상 될 수 있습니다. 에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]clr 어셈블리를 만드는 방법에 대 한 자세한 내용은 [Clr 통합 어셈블리 관리](../../../relational-databases/clr-integration/assemblies/managing-clr-integration-assemblies.md)를 참조 하세요.  
  
## <a name="accessing-external-resources"></a>외부 리소스 액세스  
 UDT (사용자 정의 형식), 저장 프로시저 또는 다른 유형의 구문 어셈블리가 **SAFE** 권한 집합에 등록 된 경우 구문에서 실행 되는 관리 코드는 외부 리소스에 액세스할 수 없습니다. 그러나 **EXTERNAL_ACCESS** 또는 **UNSAFE** 권한 집합을 지정 하 고 관리 코드에서 외부 리소스에 액세스 하려고 하는 경우는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 다음 규칙을 적용 합니다.  
  
|이|결과|  
|--------|----------|  
|실행 컨텍스트가 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 로그인에 해당합니다.|외부 리소스에 액세스하려고 하면 거부되고 보안 예외가 발생합니다.|  
|실행 컨텍스트가 Windows 로그인에 해당하고 원래 호출자입니다.|
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서비스 계정의 보안 컨텍스트에서 외부 리소스가 액세스됩니다.|  
|호출자가 원래 호출자가 아닙니다.|액세스가 거부되고 보안 예외가 발생합니다.|  
|실행 컨텍스트가 Windows 로그인에 해당하고 원래 호출자인데 호출자를 가장했습니다.|서비스 계정이 아니라 호출자 보안 컨텍스트가 액세스에 사용됩니다.|  
  
## <a name="permission-set-summary"></a>권한 집합 요약  
 다음 차트에는 **SAFE**, **EXTERNAL_ACCESS**및 **UNSAFE** 권한 집합에 부여 된 제한 사항 및 권한이 요약 되어 있습니다.  
  
|||||  
|-|-|-|-|  
||**SAFE**|**EXTERNAL_ACCESS**|**UNSAFE**|  
|**코드 액세스 보안 권한**|실행 전용|실행 및 외부 리소스 액세스|제한 없음(P/Invoke 포함)|  
|**프로그래밍 모델 제한 사항**|yes|yes|제한 없음|  
|**안정성 요구 사항**|yes|yes|예|  
|**로컬 데이터 액세스**|yes|yes|yes|  
|**네이티브 코드를 호출하는 기능**|예|예|yes|  
  
## <a name="see-also"></a>참고 항목  
 [CLR 통합 보안](../../../relational-databases/clr-integration/security/clr-integration-security.md)   
 [호스트 보호 특성 및 CLR 통합 프로그래밍](../../../relational-databases/clr-integration-security-host-protection-attributes/host-protection-attributes-and-clr-integration-programming.md)   
 [CLR 통합 프로그래밍 모델 제한 사항](../../../relational-databases/clr-integration/database-objects/clr-integration-programming-model-restrictions.md)   
 [CLR 호스팅 환경](../../../relational-databases/clr-integration/clr-integration-architecture-clr-hosted-environment.md)  
  
  
