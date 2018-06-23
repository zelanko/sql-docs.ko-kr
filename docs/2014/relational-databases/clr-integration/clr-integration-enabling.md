---
title: CLR 통합 사용 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- clr enabled option
- common language runtime [SQL Server], enabling
ms.assetid: eb3e9c64-7486-42e7-baf6-c956fb311a2c
caps.latest.revision: 17
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 15ad6087fc711de1ab818b10d591cd48512bb9a3
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36172901"
---
# <a name="enabling-clr-integration"></a>CLR 통합 사용
  CLR(공용 언어 런타임) 통합 기능은 기본적으로 해제되어 있으며 CLR 통합을 사용하여 구현된 개체를 사용하려면 이 기능을 설정해야 합니다. CLR 통합을 사용 하려면는 **사용 하도록 설정 하는 clr** 의 옵션은 **sp_configure** 저장 프로시저:  
  
```  
  
sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE;  
GO  
sp_configure 'clr enabled', 1;  
GO  
RECONFIGURE;  
GO  
```  
  
 CLR 통합을 사용 하지 않도록 설정 하 여 수는 **사용 하도록 설정 하는 clr** 옵션을 0으로 합니다. CLR 통합 기능을 해제하면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 모든 CLR 루틴 실행을 중지하고 모든 응용 프로그램 도메인을 언로드합니다.  
  
> [!NOTE]  
>  CLR 통합을 설정 하려면 ALTER SETTINGS 서버 수준 사용 권한의 구성원으로 암시적으로 소유 있어야는 **sysadmin** 및 **serveradmin** 고정 서버 역할입니다.  
  
> [!NOTE]  
>  많은 양의 메모리와 많은 수의 프로세서가 구성되어 있는 컴퓨터에서는 서버를 시작할 때 SQL Server의 CLR 통합 기능을 로드하지 못할 수 있습니다. 이 문제를 해결 하기 위해 사용 하 여 서버를 시작는 **-gmemory_to_reserve** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서비스 시작 옵션을 하 고 충분히 큰 메모리 값을 지정 합니다. 자세한 내용은 [Database Engine Service Startup Options](../../database-engine/configure-windows/database-engine-service-startup-options.md)을(를) 참조하세요.  
  
> [!NOTE]  
>  경량 풀링에서는 CLR(공용 언어 런타임) 실행이 지원되지 않습니다. CLR 통합 기능을 설정하려면 먼저 경량 풀링 기능을 해제해야 합니다. 자세한 내용은 [lightweight pooling Server Configuration Option](../../database-engine/configure-windows/lightweight-pooling-server-configuration-option.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)   
 [clr enabled 서버 구성 옵션](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md)   
 [RECONFIGURE&#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [GRANT&#40;Transact-SQL&#41;](/sql/t-sql/statements/grant-transact-sql)   
 [서버 수준 역할](../security/authentication-access/server-level-roles.md)  
  
  
