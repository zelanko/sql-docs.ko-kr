---
title: 공용 언어 런타임 (CLR) 통합 개요 | Microsoft Docs
ms.custom: ''
ms.date: 06/20/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- managed code [SQL Server]
- common language runtime [SQL Server], about CLR integration
- cross-language integration
- integrating CLR [SQL Server]
- .NET Framework [SQL Server], common language runtime
- code access security [CLR integration]
- managed code [SQL Server], CLR integration
ms.assetid: 7be9e644-36a2-48fc-9206-faf59fdff4d7
caps.latest.revision: 64
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: d79fe5e7d56e58e48ae92a6f934b11f8b3b42b67
ms.sourcegitcommit: 022d67cfbc4fdadaa65b499aa7a6a8a942bc502d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37352655"
---
# <a name="common-language-runtime-integration-overview"></a>공용 언어 런타임 통합 개요
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 이제 통합된 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows용 .NET Framework의 CLR(공용 언어 런타임) 구성 요소를 제공합니다. CLR은 관리 코드에 언어 간 통합, 코드 액세스 보안, 개체 수명 관리 및 디버깅과 프로파일링 지원 등의 서비스를 제공합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 사용자 및 응용 프로그램 개발자는 이제 통합된 CLR을 사용하여 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic .NET 및 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C#을 포함한 .NET Framework 언어로 저장 프로시저, 트리거, 사용자 정의 형식, 사용자 정의 함수(스칼라 및 테이블 반환), 사용자 정의 집계 함수를 작성할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에는 .NET Framework 버전 4가 미리 설치되어 있습니다.  

>  [!WARNING]
>  CLR은 더 이상 보안 경계로 지원되지 않는 .NET Framework의 CAS(코드 액세스 보안)를 사용합니다. `PERMISSION_SET = SAFE`로 만든 CLR 어셈블리에서 외부 시스템 리소스에 액세스하고, 비관리 코드를 호출하고, sysadmin 권한을 얻을 수 있습니다. [!INCLUDE[sssqlv14](../../includes/sssqlv14-md.md)]부터 CLR 어셈블리의 보안을 강화하기 위해 `clr strict security`라는 `sp_configure` 옵션이 도입되었습니다. `clr strict security`는 기본적으로 사용되며 `SAFE` 및 `EXTERNAL_ACCESS` 어셈블리가 `UNSAFE`로 표시된 것처럼 처리됩니다. `clr strict security` 옵션은 이전 버전과의 호환성을 위해 사용하지 않도록 설정할 수 있지만 권장하지는 않습니다. 모든 어셈블리는 master 데이터베이스에서 `UNSAFE ASSEMBLY` 권한이 부여된 해당 로그인이 포함된 인증서 또는 비대칭 키로 서명하는 것이 좋습니다. 자세한 내용은 [CLR strict security](../../database-engine/configure-windows/clr-strict-security.md)를 참조하세요. 또한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 관리자는 데이터베이스 엔진에서 신뢰해야 하는 어셈블리 목록에 어셈블리를 추가할 수도 있습니다. 자세한 내용은 [sys.sp_add_trusted_assembly](../../relational-databases/system-stored-procedures/sys-sp-add-trusted-assembly-transact-sql.md)를 참조하세요.

 이 통합의 주요 이점은 다음과 같습니다.  
  
-   **개선 된 프로그래밍 모델입니다.** .NET Framework 언어는 여러 측면에서 Transact-SQL보다 기능이 풍부하며 이전에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 개발자에게 제공되지 않던 구문 및 기능을 제공합니다. 개발자는 또한 광범위한 클래스 집합을 제공하는 .NET Framework 라이브러리의 강력한 기능을 활용하여 프로그래밍 문제를 신속하고, 효율적으로 해결할 수 있습니다.  
  
-   **개선 된 안전성 및 보안입니다.** 관리 코드는 데이터베이스 엔진에 의해 호스팅되는 공용 언어 런타임 환경에서 실행됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 이를 활용하여 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 사용되던 확장 저장 프로시저보다 안전성 및 보안이 우수한 대안을 제공합니다.  
  
-   **데이터 형식 및 집계 함수를 정의할 수 있습니다.** 사용자 정의 형식과 사용자 정의 집계는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 저장소 및 쿼리 기능을 확장하는 새로운 관리되는 데이터베이스 개체입니다.  
  
-   **표준화 된 환경 통한 효율적인된 개발입니다.** [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Studio .NET 개발 환경의 후속 릴리스에 데이터베이스 개발이 통합되었습니다. 개발자는 중간 계층 또는 클라이언트 계층 .NET Framework 구성 요소와 서비스를 작성할 때 사용하는 도구와 똑같은 도구를 사용하여 데이터베이스 개체와 스크립트를 개발하고 디버깅할 수 있습니다.  
  
-   **성능 및 확장성 개선 가능성입니다.** .NET Framework 언어 컴파일 및 실행 모델은 일반적으로 Transact-SQL보다 개선된 성능을 제공합니다.  
  
 다음 표에서는 이 섹션에서 다루는 항목을 나열합니다.  
  
 [CLR 통합 개요](../../relational-databases/clr-integration/clr-integration-overview.md)  
 통합된 CLR을 사용하여 작성할 수 있는 개체 유형과 데이터베이스 개체를 작성하기 위한 요구 사항을 살펴봅니다.  
  
 [CLR 통합의 새로운 기능](../../relational-databases/clr-integration/clr-integration-what-s-new.md)  
 이 릴리스의 새로운 기능에 대해 설명합니다.  
  
 [CLR 통합 아키텍처](http://msdn.microsoft.com/library/05e4b872-3d21-46de-b4d5-739b5f2a0cf9)  
 통합된 CLR의 디자인 목표를 설명합니다.  
  
 [CLR 통합 사용](../../relational-databases/clr-integration/clr-integration-enabling.md)  
 통합된 CLR을 사용하는 방법을 설명합니다.  
  
## <a name="see-also"></a>관련 항목  
 [.NET Framework 설치](http://technet.microsoft.com/library/ms166014\(v=SQL.105\).aspx)   
 [통합된 CLR의 성능](../../relational-databases/clr-integration/clr-integration-architecture-performance.md)  
  
  
