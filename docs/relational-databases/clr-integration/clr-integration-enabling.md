---
title: CLR 통합 활성화 | 마이크로 소프트 문서
description: CLR을 호스팅하는 Microsoft SQL Server를 CLR 통합이라고 하며 기본적으로 비활성화됩니다. sp_configure 저장 프로시저를 사용하여 CLR 통합을 활성화합니다.
ms.custom: ''
ms.date: 09/17/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- clr enabled option
- common language runtime [SQL Server], enabling
ms.assetid: eb3e9c64-7486-42e7-baf6-c956fb311a2c
author: rothja
ms.author: jroth
ms.openlocfilehash: 7d161135c8c8b0c7d7932eb08aa98509efc4bc45
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2020
ms.locfileid: "81488116"
---
# <a name="clr-integration---enabling"></a>CLR 통합 - 사용
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  CLR(공용 언어 런타임) 통합 기능은 기본적으로 해제되어 있으며 CLR 통합을 사용하여 구현된 개체를 사용하려면 이 기능을 설정해야 합니다. CLR 통합을 사용하려면 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] **sp_configure** 저장 프로시저의 **clr 사용 옵션을** 사용합니다.  
  
```sql  
EXEC sp_configure 'clr enabled', 1;  
RECONFIGURE;  
GO  
```  
  
 **clr 사용 옵션을** 0으로 설정하여 CLR 통합을 비활성화할 수 있습니다. CLR 통합을 사용하지 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 않도록 설정하면 모든 사용자 정의 CLR 루틴 실행을 중지하고 모든 응용 프로그램 도메인을 언로드합니다. **계층 구조** 데이터 형식, `FORMAT` 함수, 복제 및 정책 기반 관리와 같은 CLR에 의존하는 기능은 이 설정의 영향을 받지 않으며 계속 작동합니다.
  
> [!NOTE]  
>  CLR 통합을 사용하려면 시스템 관리자 및 **서버** **관리자** 고정 서버 역할의 구성원이 암시적으로 보유하는 ALTER SETTINGS 서버 수준 권한이 있어야 합니다.  
  
> [!NOTE]  
>  많은 양의 메모리와 많은 수의 프로세서가 구성되어 있는 컴퓨터에서는 서버를 시작할 때 SQL Server의 CLR 통합 기능을 로드하지 못할 수 있습니다. 이 문제를 해결하려면 **-gmemory_to_reserve** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 시작 옵션을 사용하여 서버를 시작하고 충분히 큰 메모리 값을 지정합니다. 자세한 내용은 [Database Engine Service Startup Options](../../database-engine/configure-windows/database-engine-service-startup-options.md)을(를) 참조하세요.  
  
> [!NOTE]  
>  경량 풀링에서는 CLR(공용 언어 런타임) 실행이 지원되지 않습니다. CLR 통합 기능을 설정하려면 먼저 경량 풀링 기능을 해제해야 합니다. 자세한 내용은 [lightweight pooling Server Configuration Option](../../database-engine/configure-windows/lightweight-pooling-server-configuration-option.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [sp_configure &#40;거래 SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [clr 지원 서버 구성 옵션](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md)   
 [&#40;거래 SQL&#41;다시 구성](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [그랜트 &#40;거래 SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [서버 수준 역할](../../relational-databases/security/authentication-access/server-level-roles.md)  
  
  
