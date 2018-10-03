---
title: 공용 언어 런타임 (CLR) 통합을 사용 하 여 데이터베이스 개체 작성 | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
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
ms.openlocfilehash: 79589050b26e072b1081323e42fdaee2345a7d6a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47623083"
---
# <a name="building-database-objects-with-common-language-runtime-clr-integration"></a>CLR(공용 언어 런타임) 통합을 사용하여 데이터베이스 개체 작성
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]와 .NET Framework CLR(공용 언어 런타임)을 통합하여 데이터베이스 개체를 작성할 수 있습니다. 내부에서 실행 되는 코드를 관리할 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 를 "CLR 루틴" 이라고 이러한 루틴에는 다음과 같은 항목이 포함됩니다.  
  
-   스칼라 반환 사용자 정의 함수(스칼라 UDF)  
  
-   테이블 반환 사용자 정의 함수(TVF)  
  
-   UDP(사용자 정의 프로시저)  
  
-   사용자 정의 트리거  
  
 CLR 루틴은 관리 코드에서도 구조가 동일하고 클래스의 공용 및 정적([!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic .NET의 경우 공유) 메서드에 매핑됩니다. .NET Framework를 사용하면 루틴뿐만 아니라 UDT(사용자 정의 형식)와 사용자 정의 집계 함수도 정의할 수 있습니다. UDT와 사용자 정의 집계 함수는 .NET Framework 클래스 전체에 매핑됩니다.  
  
 각 .NET Framework 루틴 형식은 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 선언을 포함하며 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 [!INCLUDE[tsql](../../../includes/tsql-md.md)]과 동등한 항목이 허용되는 모든 위치에서 사용할 수 있습니다. 예를 들어 스칼라 UDF는 모든 스칼라 식에 사용할 수 있고, TVF는 모든 FROM 절에 사용할 수 있습니다. 프로시저는 EXEC 문에서 호출되거나 클라이언트 응용 프로그램에서 호출될 수 있습니다.  
  
> [!NOTE]  
>  쿼리 최적화 프로그램에서 적절하다고 판단할 경우 공용 언어 런타임에서 CLR 개체(사용자 정의 함수, 사용자 정의 형식 또는 트리거)의 실행은 여러 스레드(병렬 계획)에서 발생할 수 있습니다. 그러나 사용자 정의 함수는 데이터에 액세스하므로 직렬 계획에서 실행됩니다. [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] 이전의 서버 버전에서 LOB 매개 변수나 반환 값을 포함하는 사용자 정의 함수를 실행할 경우 직렬 계획에서도 해당 함수를 실행해야 합니다.  
  
 다음 표에는 이 섹션에서 다루는 항목이 나와 있습니다.  
  
 [CLR 통합 시작](../../../relational-databases/clr-integration/database-objects/getting-started-with-clr-integration.md)  
 CLR과 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 통합을 사용하여 개체를 컴파일하는 데 필요한 라이브러리와 네임스페이스에 대한 간략한 개요를 제공합니다. "Hello World" CLR 저장 프로시저의 예도 포함되어 있습니다.  
  
 [지원되는 .NET Framework 라이브러리](../../../relational-databases/clr-integration/database-objects/supported-net-framework-libraries.md)  
 CLR 통합에서 지원되는 .NET Framework 라이브러리에 대한 정보를 제공합니다.  
  
 [CLR 통합 프로그래밍 모델 제한 사항](../../../relational-databases/clr-integration/database-objects/clr-integration-programming-model-restrictions.md)  
 CLR 통합 프로그래밍의 모델 제한 사항에 대한 정보를 제공합니다.  
  
 [.NET Framework의 SQL Server 데이터 형식](../../../relational-databases/clr-integration-database-objects-types-net-framework/sql-server-data-types-in-the-net-framework.md)  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터 형식과 해당되는 .NET Framework 데이터 형식에 대해 간략하게 설명합니다.  
  
 [CLR 통합 사용자 지정 특성 개요](http://msdn.microsoft.com/library/ecf5c097-0972-48e2-a9c0-b695b7dd2820)  
 CLR 통합 사용자 지정 특성에 대한 정보를 제공합니다.  
  
 [CLR 사용자 정의 함수](../../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-functions.md)  
 테이블 반환 함수, 스칼라 함수, 사용자 정의 집계 함수 등 여러 가지 종류의 CLR 함수를 구현하고 사용하는 방법에 대해 설명합니다.  
  
 [CLR 사용자 정의 형식](../../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)  
 CLR 사용자 정의 형식을 구현하고 사용하는 방법에 대해 설명합니다.  
  
 [CLR 저장 프로시저](http://msdn.microsoft.com/library/bbdd51b2-a9b4-4916-ba6f-7957ac6c3f33)  
 CLR 저장 프로시저를 구현하고 사용하는 방법에 대해 설명합니다.  
  
 [CLR 트리거](http://msdn.microsoft.com/library/302a4e4a-3172-42b6-9cc0-4a971ab49c1c)  
 CLR 트리거를 구현하고 사용하는 방법에 대해 설명합니다.  
  
## <a name="see-also"></a>관련 항목  
 [공용 언어 런타임 &#40;CLR&#41; 통합 개요](../../../relational-databases/clr-integration/common-language-runtime-integration-overview.md)  
  
  
