---
title: CLR 통합 사용 | Microsoft Docs
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
ms.openlocfilehash: 07066dc7ffbd48273ace55e0c9867661b2cbfe59
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "71680854"
---
# <a name="clr-integration---enabling"></a>CLR 통합 - 사용
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  CLR(공용 언어 런타임) 통합 기능은 기본적으로 해제되어 있으며 CLR 통합을 사용하여 구현된 개체를 사용하려면 이 기능을 설정해야 합니다. CLR 통합을 사용 하도록 설정 하려면에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] **sp_configure** 저장 프로시저의 **clr enabled** 옵션을 사용 합니다.  
  
```sql  
EXEC sp_configure 'clr enabled', 1;  
RECONFIGURE;  
GO  
```  
  
 Clr **enabled** 옵션을 0으로 설정 하 여 clr 통합을 사용 하지 않도록 설정할 수 있습니다. CLR 통합을 사용 하지 않도록 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설정 하면에서 모든 사용자 정의 CLR 루틴의 실행을 중지 하 고 모든 응용 프로그램 도메인을 언로드합니다. **Hierarchyid** 데이터 형식, `FORMAT` 함수, 복제 및 정책 기반 관리와 같이 CLR에 의존 하는 기능은이 설정의 영향을 받지 않으며 계속 작동할 것입니다.
  
> [!NOTE]  
>  CLR 통합을 사용 하도록 설정 하려면 **sysadmin** 및 **serveradmin** 고정 서버 역할의 멤버가 암시적으로 소유 하는 ALTER SETTINGS 서버 수준 사용 권한이 있어야 합니다.  
  
> [!NOTE]  
>  많은 양의 메모리와 많은 수의 프로세서가 구성되어 있는 컴퓨터에서는 서버를 시작할 때 SQL Server의 CLR 통합 기능을 로드하지 못할 수 있습니다. 이 문제를 해결 하려면 **-gmemory_to_reserve** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 시작 옵션을 사용 하 여 서버를 시작 하 고 충분 한 크기의 메모리 값을 지정 합니다. 자세한 내용은 [Database Engine Service Startup Options](../../database-engine/configure-windows/database-engine-service-startup-options.md)을(를) 참조하세요.  
  
> [!NOTE]  
>  경량 풀링에서는 CLR(공용 언어 런타임) 실행이 지원되지 않습니다. CLR 통합 기능을 설정하려면 먼저 경량 풀링 기능을 해제해야 합니다. 자세한 내용은 [lightweight pooling Server Configuration Option](../../database-engine/configure-windows/lightweight-pooling-server-configuration-option.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [clr enabled 서버 구성 옵션](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md)   
 [RECONFIGURE&#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [GRANT&#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [서버 수준 역할](../../relational-databases/security/authentication-access/server-level-roles.md)  
  
  
