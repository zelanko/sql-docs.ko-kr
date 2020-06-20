---
title: 가장 및 CLR 통합 보안 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: reference
helpviewer_keywords:
- impersonation [CLR integration]
- security [CLR integration]
- execution context [CLR integration]
- user impersonation [CLR integration]
- context [CLR integration]
ms.assetid: 1495a7af-2248-4cee-afdb-9269fb3a7774
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: a2313733c5a24f28c44571dd230ddc58fc9a1264
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84933560"
---
# <a name="impersonation-and-clr-integration-security"></a>가장 및 CLR 통합 보안
  관리 코드에서 외부 리소스를 액세스할 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 루틴이 실행되고 있는 현재 실행 컨텍스트를 자동으로 가장하지 않습니다. `EXTERNAL_ACCESS` 및 `UNSAFE` 어셈블리의 코드에서는 현재 실행 컨텍스트를 명시적으로 가장할 수 있습니다.  
  
> [!NOTE]  
>  가장의 동작 변경 내용에 대 한 자세한 내용은 [2014 SQL Server 데이터베이스 엔진 기능에 대 한 주요 변경 내용](../breaking-changes-to-database-engine-features-in-sql-server-2016.md)을 참조 하세요.  
  
 In-process 데이터 액세스 공급자는 현재 보안 컨텍스트와 연관된 토큰을 검색하는 데 사용할 수 있는 응용 프로그래밍 인터페이스 `SqlContext.WindowsIdentity`를 제공합니다. `EXTERNAL_ACCESS` 및 `UNSAFE` 어셈블리의 관리 코드에서는 이 메서드를 사용하여 컨텍스트를 검색할 수 있고 .NET Framework `WindowsIdentity.Impersonate` 메서드를 사용하여 해당 컨텍스트를 가장할 수 있습니다. 사용자 코드에서 명시적으로 가장할 때는 다음과 같은 제한 사항이 적용됩니다.  
  
-   관리 코드가 가장된 상태에 있는 경우 in-process 데이터 액세스가 허용되지 않습니다. 코드에서 가장을 실행 취소한 다음 in-process 데이터 액세스를 호출할 수 있습니다. 이를 위해서는 원래 `WindowsImpersonationContext` 메서드의 반환 값(`Impersonate` 개체)을 저장하고 이 `Undo`에서 `WindowsImpersonationContext` 메서드를 호출해야 합니다.  
  
     이 제한 사항은 in-process 데이터 액세스가 항상 세션에 대해 유효한 현재 보안 컨텍스트의 컨텍스트에서 발생한다는 것을 의미합니다. 이 사항은 관리 코드 내에서 명시적 가장으로 수정할 수 없습니다.  
  
-   `UNSAFE` 어셈블리를 통해 스레드를 만들고 코드를 비동기적으로 실행하는 것과 같이 관리 코드를 비동기적으로 실행하고 있는 경우에는 in-process 데이터 액세스가 허용되지 않습니다. 이는 가장을 사용하는 경우와 사용하지 않는 경우에 모두 적용됩니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]와 다른 가장된 컨텍스트에서 코드가 실행되고 있는 경우 in-process 데이터 액세스 호출을 수행할 수 없습니다. In-process 데이터 액세스를 호출하기 전에 먼저 가장 컨텍스트를 실행 취소해야 합니다. 관리 코드에서 in-process 데이터 액세스를 수행하는 경우 관리 코드에 대한 [!INCLUDE[tsql](../../includes/tsql-md.md)] 진입점의 원래 실행 컨텍스트가 항상 권한 부여를 위해 사용됩니다.  
  
 `EXTERNAL_ACCESS` 어셈블리와 `UNSAFE` 어셈블리는 모두 앞에서 설명한 대로 현재 보안 컨텍스트를 자발적으로 가장하지 않는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 계정을 사용하여 운영 체제 리소스에 액세스합니다. 따라서 `EXTERNAL_ACCESS` 어셈블리의 작성자에게는 `SAFE` 로그인 수준 권한으로 지정되는 `EXTERNAL ACCESS` 어셈블리보다 높은 신뢰 수준이 필요합니다. 따라서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 계정에서 코드를 실행하도록 트러스트된 로그인에게만 `EXTERNAL ACCESS` 권한을 부여해야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [CLR 통합 보안](../../relational-databases/clr-integration/security/clr-integration-security.md)   
 [연결에 대한 가장 및 자격 증명](../../relational-databases/clr-integration/data-access/impersonation-and-credentials-for-connections.md)  
  
  
