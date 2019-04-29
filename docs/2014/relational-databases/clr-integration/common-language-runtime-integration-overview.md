---
title: 공용 언어 런타임 (CLR) 통합 개요 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
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
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: a7764c6e8e45b56e43e592e70b1c85b8d4744b69
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62919316"
---
# <a name="common-language-runtime-clr-integration-overview"></a>CLR(공용 언어 런타임) 통합 개요
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서는 이제 통합된 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows용 .NET Framework의 CLR(공용 언어 런타임) 구성 요소를 제공합니다. CLR은 관리 코드에 언어 간 통합, 코드 액세스 보안, 개체 수명 관리 및 디버깅과 프로파일링 지원 등의 서비스를 제공합니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 사용자 및 응용 프로그램 개발자는 이제 통합된 CLR을 사용하여 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic .NET 및 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual C#을 포함한 .NET Framework 언어로 저장 프로시저, 트리거, 사용자 정의 형식, 사용자 정의 함수(스칼라 및 테이블 반환), 사용자 정의 집계 함수를 작성할 수 있습니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에는 .NET Framework 버전 4가 미리 설치되어 있습니다.  
  
 이 통합의 주요 이점은 다음과 같습니다.  
  
-   **개선 된 프로그래밍 모델입니다.** .NET Framework 언어는 여러 측면에서 Transact-SQL보다 기능이 풍부하며 이전에는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 개발자에게 제공되지 않던 구문 및 기능을 제공합니다. 개발자는 또한 광범위한 클래스 집합을 제공하는 .NET Framework 라이브러리의 강력한 기능을 활용하여 프로그래밍 문제를 신속하고, 효율적으로 해결할 수 있습니다.  
  
-   **개선 된 안전성 및 보안입니다.** 관리 코드는 데이터베이스 엔진에 의해 호스팅되는 공용 언어 런타임 환경에서 실행됩니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]는 이를 활용하여 이전 버전의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 사용되던 확장 저장 프로시저보다 안전성 및 보안이 우수한 대안을 제공합니다.  
  
-   **데이터 형식 및 집계 함수를 정의할 수 있습니다.** 사용자 정의 형식과 사용자 정의 집계는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 저장소 및 쿼리 기능을 확장하는 새로운 관리되는 데이터베이스 개체입니다.  
  
-   **표준화 된 환경 통한 효율적인된 개발입니다.** [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Studio .NET 개발 환경의 후속 릴리스에 데이터베이스 개발이 통합되었습니다. 개발자는 중간 계층 또는 클라이언트 계층 .NET Framework 구성 요소와 서비스를 작성할 때 사용하는 도구와 똑같은 도구를 사용하여 데이터베이스 개체와 스크립트를 개발하고 디버깅할 수 있습니다.  
  
-   **성능 및 확장성 개선 가능성입니다.** .NET Framework 언어 컴파일 및 실행 모델은 일반적으로 Transact-SQL보다 개선된 성능을 제공합니다.  
  
 다음 표에서는 이 섹션에서 다루는 항목을 나열합니다.  
  
 [CLR 통합 개요](clr-integration-overview.md)  
 통합된 CLR을 사용하여 작성할 수 있는 개체 유형과 데이터베이스 개체를 작성하기 위한 요구 사항을 살펴봅니다.  
  
 [CLR 통합의 새로운 기능](clr-integration-what-s-new.md)  
 이 릴리스의 새로운 기능에 대해 설명합니다.  
  
 [CLR 통합 아키텍처](../../database-engine/dev-guide/architecture-of-clr-integration.md)  
 통합된 CLR의 디자인 목표를 설명합니다.  
  
 [CLR 통합 사용](clr-integration-enabling.md)  
 통합된 CLR을 사용하는 방법을 설명합니다.  
  
## <a name="see-also"></a>관련 항목  
 [.NET Framework 설치](https://technet.microsoft.com/library/ms166014\(v=SQL.105\).aspx)   
 [통합된 CLR의 성능](clr-integration-architecture-performance.md)  
  
  
