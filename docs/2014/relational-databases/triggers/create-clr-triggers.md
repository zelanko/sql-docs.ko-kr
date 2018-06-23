---
title: CLR 트리거 만들기 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-dml
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- CRL triggers
- DML triggers, CLR triggers
- DDL triggers, CLR triggers
ms.assetid: 31f41703-134d-49fc-9850-76c297351c2c
caps.latest.revision: 27
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 398470880fb412048c96a3114f6d3c648ef4bc1a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36089021"
---
# <a name="create-clr-triggers"></a>CLR 트리거 만들기
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] CLR(공용 언어 런타임)에 만들어진 어셈블리에 프로그래밍된 데이터베이스 개체를 만들 수 있습니다. CLR에서 제공하는 다양한 기능의 프로그래밍 모델을 활용할 수 있는 데이터베이스 개체에는 DML 트리거, DDL 트리거, 저장 프로시저, 함수, 집계 함수 및 유형이 있습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 CLR 트리거(DML 또는 DDL)를 만드는 단계는 다음과 같습니다.  
  
-   .NET Framework 지원 언어로 트리거를 클래스로 정의합니다. CLR에서 트리거를 프로그래밍하는 방법은 [CLR 트리거](../../database-engine/dev-guide/clr-triggers.md)를 참조하세요. 그런 다음 적절한 언어 컴파일러를 사용하여 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 에서 어셈블리를 빌드하기 위한 클래스를 컴파일합니다.  
  
-   CREATE ASSEMBLY 문을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 어셈블리를 등록합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 어셈블리에 대한 자세한 내용은 [어셈블리&#40;데이터베이스 엔진&#41;](../clr-integration/assemblies-database-engine.md)를 참조하세요.  
  
-   등록된 어셈블리를 참조하는 트리거를 만듭니다.  
  
> [!NOTE]  
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 에서 SQL Server 프로젝트를 배포하면 해당 프로젝트에 대해 지정된 데이터베이스에 어셈블리가 등록됩니다. 또한 프로젝트를 배포하면 모든 메서드에 대해 `SqlTrigger` 특성으로 주석 지정으로 지정하기 위해 데이터베이스에 CLR 트리거를 만듭니다. 자세한 내용은 [Deploying CLR Database Objects](../clr-integration/deploying-clr-database-objects.md)을(를) 참조하세요.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 CLR 코드 실행 기능은 기본적으로 해제되어 있습니다. 관리 코드 모듈을 참조하는 데이터베이스 개체를 만들고 변경하고 삭제할 수 있지만 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sp_configure(Transact-SQL) [을 사용하여](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md) clr enabled 옵션 [을 설정하지 않는 한 이러한 참조는](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)에서 실행되지 않습니다.  
  
 **어셈블리를 생성, 수정 또는 삭제하려면**  
  
-   [CREATE ASSEMBLY&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-assembly-transact-sql)  
  
-   [ALTER ASSEMBLY&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-assembly-transact-sql)  
  
-   [DROP ASSEMBLY&#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-assembly-transact-sql)  
  
 **CLR 트리거를 만들려면**  
  
-   [CREATE TRIGGER&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-trigger-transact-sql)  
  
## <a name="see-also"></a>관련 항목  
 [DML 트리거](dml-triggers.md)   
 [CLR&#40;공용 언어 런타임&#41; 통합 프로그래밍 개요](../clr-integration/common-language-runtime-clr-integration-programming-concepts.md)   
 [CLR 데이터베이스 개체에서 데이터 액세스](../clr-integration/data-access/data-access-from-clr-database-objects.md)  
  
  
