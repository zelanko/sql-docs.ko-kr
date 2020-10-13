---
description: CLR 함수 만들기
title: CLR 함수 만들기 | Microsoft 문서
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- CLR functions [SQL Server]
- user-defined functions [SQL Server], CLR
ms.assetid: a82df075-2243-4e19-bfe1-ae6d65dabd0f
author: rothja
ms.author: jroth
ms.openlocfilehash: 4e7e7ba7e0e3f526c69026b9f759937d7329d50c
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2020
ms.locfileid: "91811077"
---
# <a name="create-clr-functions"></a>CLR 함수 만들기
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] CLR(공용 언어 런타임)에 만들어진 어셈블리에 프로그래밍된 데이터베이스 개체를 만들 수 있습니다. CLR에서 제공하는 풍부한 프로그래밍 모델을 활용할 수 있는 데이터베이스 개체에는 집계 함수, 함수, 저장 프로시저, 트리거 및 형식이 있습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 CLR 함수를 만드는 방법은 다음과 같습니다.  
  
-   [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]에서 지원하는 언어를 사용하여 클래스의 정적 메서드로 함수를 정의합니다. 공용 언어 런타임에서 함수를 프로그래밍하는 방법은 [CLR 사용자 정의 함수](../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-functions.md)를 참조하세요. 함수를 정의한 다음 적절한 언어 컴파일러를 사용하여 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 에서 어셈블리를 빌드하기 위한 클래스를 컴파일합니다.  
  
-   CREATE ASSEMBLY 문을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 어셈블리를 등록합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 어셈블리에 대한 자세한 내용은 [어셈블리&#40;데이터베이스 엔진&#41;](../../relational-databases/clr-integration/assemblies-database-engine.md)를 참조하세요.  
  
-   [CREATE FUNCTION](../../t-sql/statements/create-function-transact-sql.md) 문을 사용하여 등록된 어셈블리를 참조하는 함수를 만듭니다.  
  
> [!NOTE]
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 에서 SQL Server 프로젝트를 배포하면 해당 프로젝트에 대해 지정된 데이터베이스에 어셈블리가 등록됩니다. 또한 프로젝트를 배포하면 모든 메서드에 대해 **SqlFunction** 특성으로 주석 지정으로 지정하기 위해 데이터베이스에 CLR 함수를 만듭니다. 자세한 내용은 [Deploying CLR Database Objects](../../relational-databases/clr-integration/deploying-clr-database-objects.md)을 참조하세요.  
> 
> [!NOTE]
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 CLR 코드 실행 기능은 기본적으로 해제되어 있습니다. 관리 코드 모듈을 참조하는 데이터베이스 개체를 만들고 변경하고 삭제할 수 있지만 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sp_configure(Transact-SQL) [를 사용하여](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md) clr enabled 옵션 [을 설정하지 않는 한 이러한 참조는](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)에서 실행되지 않습니다.  
  
## <a name="accessing-external-resources"></a>외부 리소스 액세스  
 CLR 함수를 사용하여 파일, 네트워크 리소스, 웹 서비스, 기타 데이터베이스( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 원격 인스턴스 포함) 등의 외부 리소스에 액세스할 수 있습니다. [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)], `System.IO`, `System.WebServices`과 같은 `System.Sql`의 다양한 클래스를 사용하면 외부 리소스에 대한 액세스가 가능합니다. 액세스를 위해서는 이러한 함수를 포함하는 어셈블리를 최소한 EXTERNAL_ACCESS 권한 집합으로 구성해야 합니다. 자세한 내용은 [CREATE ASSEMBLY&#40;Transact-SQL&#41;](../../t-sql/statements/create-assembly-transact-sql.md)에서 지원하는 언어를 사용하여 클래스의 정적 메서드로 함수를 정의합니다. SQL 클라이언트 관리 공급자를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 원격 인스턴스를 액세스할 수 있습니다. 그러나 CLR 함수에서는 원본 서버에 대한 루프백 연결을 지원하지 않습니다.  
  
 **SQL Server에서 어셈블리를 만들거나 수정하거나 삭제하려면**  
  
-   [CREATE ASSEMBLY&#40;Transact-SQL&#41;](../../t-sql/statements/create-assembly-transact-sql.md)  
  
-   [ALTER ASSEMBLY&#40;Transact-SQL&#41;](../../t-sql/statements/alter-assembly-transact-sql.md)  
  
-   [DROP ASSEMBLY&#40;Transact-SQL&#41;](../../t-sql/statements/drop-assembly-transact-sql.md)  
  
 **CLR 함수를 만들려면**  
  
-   [CREATE FUNCTION&#40;Transact-SQL&#41;](../../t-sql/statements/create-function-transact-sql.md)  
  
## <a name="accessing-native-code"></a>네이티브 코드 액세스  
 CLR 함수를 사용하면 관리 코드에서 PInvoke를 사용하는 방법을 통해 C 또는 C++로 작성된 코드 등의 네이티브(비관리) 코드에 액세스할 수 있습니다. 자세한 내용은 [관리 코드에서 네이티브 함수 호출](/cpp/dotnet/calling-native-functions-from-managed-code) 을 참조하세요. 네이티브 코드에 액세스하면 레거시 코드를 CLR UDF로 다시 사용하거나 성능에 중요한 영향을 주는 UDF를 네이티브 코드로 작성할 수 있습니다. 이렇게 하려면 UNSAFE 어셈블리를 사용해야 합니다. UNSAFE 어셈블리 사용에 대한 주의 사항은 [CLR Integration Code Access Security](../../relational-databases/clr-integration/security/clr-integration-code-access-security.md) 을 참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [사용자 정의 함수 만들기&#40;데이터베이스 엔진&#41;](../../relational-databases/user-defined-functions/create-user-defined-functions-database-engine.md)   
 [사용자 정의 집계 만들기](../../relational-databases/user-defined-functions/create-user-defined-aggregates.md)   
 [사용자 정의 함수 실행](../../relational-databases/user-defined-functions/execute-user-defined-functions.md)   
 [사용자 정의 함수 보기](../../relational-databases/user-defined-functions/view-user-defined-functions.md)   
 [CLR&#40;공용 언어 런타임&#41; 통합 프로그래밍 개요](../../relational-databases/clr-integration/common-language-runtime-clr-integration-programming-concepts.md)  
  
