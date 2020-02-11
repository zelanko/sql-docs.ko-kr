---
title: CLR (공용 언어 런타임) 통합을 사용 하 여 데이터베이스 개체 빌드 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- routines [CLR integration]
- database objects [CLR integration], building
- common language runtime [SQL Server], building database objects
- managed code [SQL Server], database objects
- building database objects [CLR integration]
- .NET Framework routines [SQL Server]
ms.assetid: ce34132c-bfa3-447b-9131-b6e17c672efe
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 8dc507d455636bf6256fd7ba4649dba53d32884e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62919249"
---
# <a name="building-database-objects-with-common-language-runtime-clr-integration"></a>CLR(공용 언어 런타임) 통합을 사용하여 데이터베이스 개체 작성
  을 사용 하 여 [!INCLUDE[ssNoVersion](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터베이스 개체를 빌드할 수 있습니다. "CLR 루틴" 이라고 합니다. 이러한 루틴에는 다음과 같은 항목이 포함됩니다.  
  
-   스칼라 반환 사용자 정의 함수(스칼라 UDF)  
  
-   테이블 반환 사용자 정의 함수(TVF)  
  
-   UDP(사용자 정의 프로시저)  
  
-   사용자 정의 트리거  
  
 CLR 루틴은 관리 코드에서도 구조가 동일하고 클래스의 공용 및 정적([!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic .NET의 경우 공유) 메서드에 매핑됩니다. .NET Framework를 사용하면 루틴뿐만 아니라 UDT(사용자 정의 형식)와 사용자 정의 집계 함수도 정의할 수 있습니다. UDT와 사용자 정의 집계 함수는 .NET Framework 클래스 전체에 매핑됩니다.  
  
 .NET Framework 루틴의 각 형식에는 [!INCLUDE[tsql](../../../includes/ssnoversion-md.md)] 해당 하 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 는를 사용할 수 있는가 있습니다. 예를 들어 스칼라 UDF는 모든 스칼라 식에 사용할 수 있고, TVF는 모든 FROM 절에 사용할 수 있습니다. 프로시저는 EXEC 문에서 호출되거나 클라이언트 애플리케이션에서 호출될 수 있습니다.  
  
> [!NOTE]  
>  쿼리 최적화 프로그램에서 적절하다고 판단할 경우 공용 언어 런타임에서 CLR 개체(사용자 정의 함수, 사용자 정의 형식 또는 트리거)의 실행은 여러 스레드(병렬 계획)에서 발생할 수 있습니다. 그러나 사용자 정의 함수는 데이터에 액세스하므로 직렬 계획에서 실행됩니다. 
  [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] 이전의 서버 버전에서 LOB 매개 변수나 반환 값을 포함하는 사용자 정의 함수를 실행할 경우 직렬 계획에서도 해당 함수를 실행해야 합니다.  
  
 다음 표에는 이 섹션에서 다루는 항목이 나와 있습니다.  
  
 [CLR 통합으로 작업 시작](getting-started-with-clr-integration.md)  
 CLR과 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 통합을 사용하여 개체를 컴파일하는 데 필요한 라이브러리와 네임스페이스에 대한 간략한 개요를 제공합니다. "Hello World" CLR 저장 프로시저의 예도 포함되어 있습니다.  
  
 [지원되는 .NET Framework 라이브러리](supported-net-framework-libraries.md)  
 CLR 통합에서 지원되는 .NET Framework 라이브러리에 대한 정보를 제공합니다.  
  
 [CLR 통합 프로그래밍 모델 제한 사항](clr-integration-programming-model-restrictions.md)  
 CLR 통합 프로그래밍의 모델 제한 사항에 대한 정보를 제공합니다.  
  
 [.NET Framework의 SQL Server 데이터 형식](../../clr-integration-database-objects-types-net-framework/sql-server-data-types-in-the-net-framework.md)  
 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터 형식과 해당되는 .NET Framework 데이터 형식에 대해 간략하게 설명합니다.  
  
 [CLR 통합 사용자 지정 특성 개요](../../../database-engine/dev-guide/overview-of-clr-integration-custom-attributes.md)  
 CLR 통합 사용자 지정 특성에 대한 정보를 제공합니다.  
  
 [CLR 사용자 정의 함수](../../clr-integration-database-objects-user-defined-functions/clr-user-defined-functions.md)  
 테이블 반환 함수, 스칼라 함수, 사용자 정의 집계 함수 등 여러 가지 종류의 CLR 함수를 구현하고 사용하는 방법에 대해 설명합니다.  
  
 [CLR 사용자 정의 형식](../../clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)  
 CLR 사용자 정의 형식을 구현하고 사용하는 방법에 대해 설명합니다.  
  
 [CLR 저장 프로시저](../../../database-engine/dev-guide/clr-stored-procedures.md)  
 CLR 저장 프로시저를 구현하고 사용하는 방법에 대해 설명합니다.  
  
 [CLR 트리거](../../../database-engine/dev-guide/clr-triggers.md)  
 CLR 트리거를 구현하고 사용하는 방법에 대해 설명합니다.  
  
## <a name="see-also"></a>참고 항목  
 [공용 언어 런타임 &#40;CLR&#41; 통합 개요](../common-language-runtime-integration-overview.md)  
  
  
