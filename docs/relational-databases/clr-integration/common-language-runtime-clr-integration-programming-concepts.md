---
title: CLR (공용 언어 런타임) 통합 프로그래밍 개념 | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- CLR [SQL Server] See common language runtime [SQL Server]
- Database Engine [SQL Server], .NET Framework
- .NET Framework [SQL Server], Database Engine programming
- common language runtime [SQL Server]
- .NET Framework [SQL Server]
ms.assetid: 951bf851-3e6e-4361-ae6a-2bcd5b837ebd
author: rothja
ms.author: jroth
ms.openlocfilehash: b172399d5e7a04365cf8005b5dc52ebc9795c13a
ms.sourcegitcommit: 734529a6f108e6ee6bfce939d8be562d405e1832
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/02/2019
ms.locfileid: "70212384"
---
# <a name="common-language-runtime-clr-integration-programming-concepts"></a>CLR(공용 언어 런타임) 통합 프로그래밍 개요
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]부터 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 통합된 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows용 .NET Framework의 CLR(공용 언어 런타임) 구성 요소를 제공합니다. 이를 통해 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic .NET 및 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C#을 포함한 모든 .NET Framework 언어를 사용하여 저장 프로시저, 트리거, 사용자 정의 형식, 사용자 정의 함수, 사용자 정의 집계 및 스트리밍 테이블 반환 함수를 작성할 수 있습니다.  
  
 The Microsoft.SqlServer.Server 네임스페이스에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 CLR 프로그래밍에 대한 핵심 기능이 포함되어 있습니다. 그러나 Microsoft.SqlServer.Server 네임스페이스는 .NET Framework SDK에 설명되어 있는데, 이 설명서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 온라인 설명서에 포함되어 있지 않습니다.  
  
> [!IMPORTANT]  
>  기본적으로 .NET Framework는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 설치하면 자동으로 설치되지만 .NET Framework SDK는 그렇지 않습니다. 컴퓨터에 SDK가 설치되지 않아 온라인 설명서 컬렉션이 포함되어 있지 않을 경우 이 섹션의 SDK 내용에 대한 링크가 작동하지 않습니다. 따라서 .NET Framework SDK를 설치하는 것이 좋습니다. 설치 되 면 [.NET FRAMEWORK Sdk 설치](https://technet.microsoft.com/library/bb686823\(v=SQL.105\).aspx)의 지침에 따라 온라인 설명서 컬렉션과 목차에 sdk를 추가 합니다.  
  
> [!NOTE]  
>  CLR 기능 (예: CLR 사용자 함수)은 Azure SQL Database에 대해 지원 *되지 않습니다* .  
  
 다음 표에서는 이 섹션에서 다루는 항목을 나열합니다.  
  
 [CLR&#41; (공용 &#40;언어 런타임) 통합 개요](../../relational-databases/clr-integration/common-language-runtime-integration-overview.md)  
 CLR에 대한 간략한 개요를 제공하고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 이 기술을 사용하는 방법과 그 이유에 대해 설명합니다. 또한 CLR을 사용하여 데이터베이스 개체를 만들 경우의 이점에 대해서도 설명합니다.  
  
 [어셈블리&#40;데이터베이스 엔진&#41;](../../relational-databases/clr-integration/assemblies-database-engine.md)  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 어셈블리를 사용하여 함수, 저장 프로시저, 트리거, 사용자 정의 집계, [!INCLUDE[msCoName](../../includes/msconame-md.md)]로 작성되지 않고 [!INCLUDE[tsql](../../includes/tsql-md.md)] .NET Framework CLR(공용 언어 런타임)로 호스팅되는 관리 코드 언어 중 하나로 작성된 사용자 정의 형식을 배포하는 방법을 설명합니다.  
  
 [CLR &#40;&#41; (공용 언어 런타임) 통합을 사용 하 여 데이터베이스 개체 빌드](../../relational-databases/clr-integration/database-objects/building-database-objects-with-common-language-runtime-clr-integration.md)  
 CLR을 사용하여 작성할 수 있는 개체 유형에 대해 설명하고 CLR 데이터베이스 개체를 작성하기 위한 요구 사항을 살펴봅니다.  
  
 [CLR 데이터베이스 개체에서 데이터 액세스](../../relational-databases/clr-integration/data-access/data-access-from-clr-database-objects.md)  
 CLR 루틴을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 저장된 데이터에 액세스하는 방법에 대해 설명합니다.  
  
 [CLR 통합 보안](../../relational-databases/clr-integration/security/clr-integration-security.md)  
 CLR 통합 보안 모델에 대해 설명합니다.  
  
 [CLR 데이터베이스 개체 디버깅](../../relational-databases/clr-integration/debugging-clr-database-objects.md)  
 CLR 데이터베이스 개체의 디버깅에 대한 제한 사항 및 요구 사항에 대해 설명합니다.  
  
 [CLR 데이터베이스 개체 배포](../../relational-databases/clr-integration/deploying-clr-database-objects.md)  
 프로덕션 서버에 어셈블리를 배포하는 방법에 대해 설명합니다.  
  
 [CLR 통합 어셈블리 관리](../../relational-databases/clr-integration/assemblies/managing-clr-integration-assemblies.md)  
 CLR 통합 어셈블리를 만들고 삭제하는 방법에 대해 설명합니다.  
  
 [관리되는 데이터베이스 개체 모니터링 및 문제 해결](../../relational-databases/clr-integration/monitoring-and-troubleshooting-managed-database-objects.md)  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 실행 중인 관리되는 데이터베이스 개체와 어셈블리를 모니터링하고 문제를 해결하는 데 사용할 수 있는 도구에 대한 정보를 제공합니다.  
  
 [공용 언어 런타임 &#40;CLR&#41; 통합에 대한 사용 시나리오 및 예제](https://msdn.microsoft.com/library/33aac25f-abb4-4f29-af88-4a0dacd80ae7)  
 CLR 개체를 사용하는 사용 시나리오 및 코드 예제에 대해 설명합니다.  
  
## <a name="see-also"></a>관련 항목  
 [어셈블리 &#40;데이터베이스 엔진&#41;](../../relational-databases/clr-integration/assemblies-database-engine.md)   
 [.NET Framework SDK 설치](https://technet.microsoft.com/library/bb686823\(v=SQL.105\).aspx)  
  
  
