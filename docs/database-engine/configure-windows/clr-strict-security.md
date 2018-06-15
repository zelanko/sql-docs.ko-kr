---
title: CLR 엄격한 보안 | Microsoft Docs
description: SQL Server에서 CLR 엄격한 보안을 구성하는 방법
ms.custom: ''
ms.date: 06/20/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.suite: sql
ms.technology: configuration
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- clr strict security
- clr_strict_security_TSQL
- clr strict security
- strict_security_TSQL
helpviewer_keywords:
- assemblies [CLR integration], strick security
- clr strict security option
ms.assetid: ''
caps.latest.revision: 0
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 3889d749e7b50300a42a165c46a029daee5feb56
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32871068"
---
# <a name="clr-strict-security"></a>CLR 엄격한 보안   
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 `SAFE`, `EXTERNAL ACCESS`, `UNSAFE` 권한의 해석을 제어합니다.   

|값 |Description | 
|----- |----- | 
|0 |Disabled - 이전 버전과의 호환성을 위해 제공됩니다. `Disabled` 값은 사용하지 않는 것이 좋습니다. | 
|1 |Enabled - [!INCLUDE[ssde-md](../../includes/ssde-md.md)]에서 어셈블리에 대한 `PERMISSION_SET` 정보를 무시하도록 하고 항상 `UNSAFE`로 해석합니다.  `Enabled`는 [!INCLUDE[sssqlv14](../../includes/sssqlv14-md.md)]에 대한 기본값입니다. | 

>  [!WARNING]
>  CLR은 더 이상 보안 경계로 지원되지 않는 .NET Framework의 CAS(코드 액세스 보안)를 사용합니다. `PERMISSION_SET = SAFE`로 만든 CLR 어셈블리에서 외부 시스템 리소스에 액세스하고, 비관리 코드를 호출하고, sysadmin 권한을 얻을 수 있습니다. [!INCLUDE[sssqlv14](../../includes/sssqlv14-md.md)]부터 CLR 어셈블리의 보안을 강화하기 위해 `clr strict security`라는 `sp_configure` 옵션이 도입되었습니다. `clr strict security`는 기본적으로 사용되며 `SAFE` 및 `EXTERNAL_ACCESS` 어셈블리가 `UNSAFE`로 표시된 것처럼 처리됩니다. `clr strict security` 옵션은 이전 버전과의 호환성을 위해 사용하지 않도록 설정할 수 있지만 권장하지는 않습니다. 모든 어셈블리는 master 데이터베이스에서 `UNSAFE ASSEMBLY` 권한이 부여된 해당 로그인이 포함된 인증서 또는 비대칭 키로 서명하는 것이 좋습니다. 또한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 관리자는 데이터베이스 엔진에서 신뢰해야 하는 어셈블리 목록에 어셈블리를 추가할 수도 있습니다. 자세한 내용은 [sys.sp_add_trusted_assembly](../../relational-databases/system-stored-procedures/sys-sp-add-trusted-assembly-transact-sql.md)를 참조하세요.

## <a name="remarks"></a>Remarks   

사용하도록 설정되면 `CREATE ASSEMBLY` 및 `ALTER ASSEMBLY` 문의 `PERMISSION_SET` 옵션은 런타임에서 무시되지만 `PERMISSION_SET` 옵션은 메타데이터에서 유지됩니다. 이 옵션을 무시하면 기존 코드 문의 중단을 최소화합니다.

`CLR strict security`는 `advanced option`입니다.  

>  [!IMPORTANT]  
>  strict security(엄격한 보안)를 사용하도록 설정하면 서명되지 않은 어셈블리는 로드되지 않습니다. 서버에 대한 `UNSAFE ASSEMBLY` 권한이 있는 해당 로그인이 포함된 인증서 또는 비대칭 키로 서명되도록 각 어셈블리를 변경하거나 삭제한 다음 다시 만들어야 합니다.

## <a name="permissions"></a>사용 권한 

### <a name="to-change-this-option"></a>이 옵션을 변경하려면,  
`CONTROL SERVER` 권한 또는 `sysadmin` 고정 서버 역할의 멤버 자격이 필요합니다.

### <a name="to-create-an-clr-assembly"></a>CLR 어셈블리를 만들려면,   
`CLR strict security`를 사용할 때 CLR 어셈블리를 만드는 데 필요한 권한은 다음과 같습니다.

- 사용자에게 `CREATE ASSEMBLY` 권한이 있어야 합니다.  
- 다음 조건 중 하나가 충족되어야 합니다.  
  - 어셈블리는 서버에 대한 `UNSAFE ASSEMBLY` 권한이 있는 해당 로그인이 포함된 인증서 또는 비대칭 키로 서명됩니다. 어셈블리에 서명하는 것이 좋습니다.  
  - 데이터베이스는 `ON`으로 설정된 `TRUSTWORTHY` 속성을 가지고 있고 서버에 대한 `UNSAFE ASSEMBLY` 권한이 있는 로그인으로 소유됩니다. 이 방법은 권장되지 않습니다.  

  
## <a name="see-also"></a>참고 항목  
  
 [서버 구성 옵션&#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [CRL 사용 서버 구성 옵션](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md)
