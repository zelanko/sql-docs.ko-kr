---
title: clr enabled 서버 구성 옵션 | Microsoft Docs
ms.custom: ''
ms.date: 06/20/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- assemblies [CLR integration], verifying can run
- clr enabled option
ms.assetid: 0722d382-8fd3-4fac-b4a8-cd2b7a7e0293
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 71392e537cb034976b3c47d819897356e3bb58cb
ms.sourcegitcommit: 445842da7c7d216b94a9576e382164c67f54e19a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/30/2019
ms.locfileid: "71682086"
---
# <a name="clr-enabled-server-configuration-option"></a>clr enabled 서버 구성 옵션
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  clr enabled 옵션을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 사용자 어셈블리를 실행할 수 있는지 여부를 지정합니다. clr enabled 옵션은 다음 값을 제공합니다. 
  
|값|설명|  
|-----------|-----------------|  
|0|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 어셈블리를 실행할 수 없습니다.|  
|1|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 어셈블리를 실행할 수 없습니다.|  
  
WOW64에만 해당합니다. 설정 변경 내용을 적용하려면 WOW64 서버를 다시 시작합니다. 다른 서버 유형의 경우에는 서버를 다시 시작하지 않아도 됩니다.  

RECONFIGURE를 실행하고 clr enabled 옵션을 1에서 0으로 변경하면 사용자 어셈블리가 포함된 모든 애플리케이션 도메인이 즉시 언로드됩니다.  
  
>  **경량 풀링에서는 CLR(공용 언어 런타임) 실행이 지원되지 않습니다.** "clr enabled" 또는 "lightweight pooling" 옵션 중 하나를 해제하세요. CLR을 사용하며 파이버 모드에서 제대로 작동하지 않는 기능으로 **hierarchyid** 데이터 형식, `FORMAT` 함수, 복제 및 정책 기반 관리가 있습니다.  
> 
> [!WARNING]
>  CLR은 더 이상 보안 경계로 지원되지 않는 .NET Framework의 CAS(코드 액세스 보안)를 사용합니다. `PERMISSION_SET = SAFE`로 만든 CLR 어셈블리에서 외부 시스템 리소스에 액세스하고, 비관리 코드를 호출하고, sysadmin 권한을 얻을 수 있습니다. [!INCLUDE[sssqlv14](../../includes/sssqlv14-md.md)]부터 CLR 어셈블리의 보안을 강화하기 위해 `clr strict security`라는 `sp_configure` 옵션이 도입되었습니다. `clr strict security`는 기본적으로 사용되며 `SAFE` 및 `EXTERNAL_ACCESS` 어셈블리가 `UNSAFE`로 표시된 것처럼 처리됩니다. `clr strict security` 옵션은 이전 버전과의 호환성을 위해 사용하지 않도록 설정할 수 있지만 권장하지는 않습니다. 모든 어셈블리는 master 데이터베이스에서 `UNSAFE ASSEMBLY` 권한이 부여된 해당 로그인이 포함된 인증서 또는 비대칭 키로 서명하는 것이 좋습니다. 또한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 관리자는 데이터베이스 엔진에서 신뢰해야 하는 어셈블리 목록에 어셈블리를 추가할 수도 있습니다. 자세한 내용은 [sys.sp_add_trusted_assembly](../../relational-databases/system-stored-procedures/sys-sp-add-trusted-assembly-transact-sql.md)를 참조하세요.
  
## <a name="example"></a>예제  
 다음 예에서는 먼저 clr enabled 옵션의 현재 설정을 표시한 다음 옵션 값을 1로 설정하여 옵션을 사용하도록 설정합니다. 옵션을 해제하려면 값을 0으로 설정합니다.  
  
```sql  
EXEC sp_configure 'clr enabled';  
EXEC sp_configure 'clr enabled' , '1';  
RECONFIGURE;    
```  
  
## <a name="see-also"></a>참고 항목  
 [경량 풀링 서버 구성 옵션](../../database-engine/configure-windows/lightweight-pooling-server-configuration-option.md)   
 [서버 구성 옵션&#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [경량 풀링 서버 구성 옵션](../../database-engine/configure-windows/lightweight-pooling-server-configuration-option.md)  
  
  
