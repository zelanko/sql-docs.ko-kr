---
title: 사용자 정의 집계 만들기 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-udf
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- aggregate functions [SQL Server], user-defined
- user-defined functions [CLR integration]
ms.assetid: c278b746-6323-4b32-b460-239915acc067
caps.latest.revision: 28
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: b47cd4e09172a750d709a8da8c1600cb60112782
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36082647"
---
# <a name="create-user-defined-aggregates"></a>사용자 정의 집계 만들기
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 내에 CLR 어셈블리로 프로그래밍된 데이터베이스 개체를 만들 수 있습니다. CLR에서 제공하는 풍부한 프로그래밍 모델을 활용할 수 있는 데이터베이스 개체에는 트리거, 저장 프로시저, 함수, 집계 함수 및 형식이 있습니다.  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 제공되는 기본 제공 집계 함수와 마찬가지로 사용자 정의 집계 함수는 값 집합에 대한 계산을 수행한 후 단일 값을 반환합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 다음과 같은 방식으로 사용자 정의 집계 함수를 만들 수 있습니다.  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework 지원 언어의 클래스로 사용자 정의 집계 함수를 정의합니다. CLR로 사용자 정의 집계를 프로그래밍하는 방법은 [CLR 사용자 정의 집계](../clr-integration-database-objects-user-defined-functions/clr-user-defined-aggregates.md)를 참조하세요. 그런 다음 적절한 언어 컴파일러로 정의된 클래스를 컴파일하여 CLR 어셈블리를 빌드합니다.  
  
-   CREATE ASSEMBLY 문을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 어셈블리를 등록합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 어셈블리에 대한 자세한 내용은 [어셈블리&#40;데이터베이스 엔진&#41;](../clr-integration/assemblies-database-engine.md)를 참조하세요.  
  
-   CREATE AGGREGATE 문을 사용하여 등록된 어셈블리를 참조하는 사용자 정의 집계를 만듭니다.  
  
> [!NOTE]  
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 에서 SQL Server 프로젝트를 배포하면 해당 프로젝트에 대해 지정된 데이터베이스에 어셈블리가 등록됩니다. 또한 프로젝트를 배포하면 `SqlUserDefinedAggregate` 특성으로 주석이 지정된 모든 클래스 정의에 대해 데이터베이스에서 사용자 정의 집계를 만듭니다. 자세한 내용은 [Deploying CLR Database Objects](../clr-integration/deploying-clr-database-objects.md)을 참조하세요.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 CLR 코드 실행 기능은 기본적으로 해제되어 있습니다. 관리 코드 모듈을 참조하는 데이터베이스 개체를 만들고 변경하고 삭제할 수 있지만 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sp_configure(Transact-SQL) [를 사용하여](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md) clr enabled 옵션 [을 설정하지 않는 한 이러한 참조는](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)에서 실행되지 않습니다.  
  
 **어셈블리를 생성, 수정 또는 삭제하려면**  
  
-   [CREATE ASSEMBLY&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-assembly-transact-sql)  
  
-   [ALTER ASSEMBLY&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-assembly-transact-sql)  
  
-   [DROP ASSEMBLY&#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-assembly-transact-sql)  
  
 **사용자 정의 집계를 만들려면**  
  
-   [CREATE AGGREGATE&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-aggregate-transact-sql)  
  
## <a name="see-also"></a>관련 항목  
 [CLR&#40;공용 언어 런타임&#41; 통합 프로그래밍 개요](../clr-integration/common-language-runtime-clr-integration-programming-concepts.md)  
  
  
