---
title: CLR 루틴에 대 한 사용자 지정 특성 | Microsoft Docs
description: 사용자 지정 특성은 Microsoft SQL Server에 등록 된 CLR 루틴, 사용자 정의 형식 및 사용자 정의 집계에 적용 될 수 있습니다.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- routines [CLR integration]
- SqlFacet attribute
- SqlTrigger attribute
- SqlProcedure attribute
- custom attributes [CLR integration]
- SqlUserDefinedAggregate attribute
- attributes [CLR integration]
- SqlMethod attribute
- SqlFunction attribute
- common language runtime [SQL Server], attributes
- SqlUserDefinedTypeAttribute attribute
ms.assetid: 95069d22-b05d-4670-b053-15ee2a664e33
author: rothja
ms.author: jroth
ms.openlocfilehash: bad209c4ddb516167b8048ae73680bc9ea59cc05
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2020
ms.locfileid: "91810811"
---
# <a name="clr-integration-custom-attributes-for-clr-routines"></a>CLR 루틴용 CLR 통합 사용자 지정 특성
[!INCLUDE[sql-asdbmi](../../../includes/applies-to-version/sql-asdbmi.md)]
  에 등록 된 CLR (공용 언어 런타임) 루틴, 사용자 정의 형식 및 사용자 정의 집계에 나열 된 특성을 적용할 수 있습니다 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . 특성이 적용되지 않으면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]는 기본값을 사용합니다. 나열 된 특성은 **Microsoft 서버** 네임 스페이스에 정의 되어 있습니다.  
  
## <a name="the-sqluserdefinedaggregate-attribute"></a>SqlUserDefinedAggregate 특성  
 **SqlUserDefinedAggregate** 특성은 메서드를 사용자 정의 집계로 등록 해야 함을 나타냅니다. 모든 사용자 정의 집계에는 이 특성이 주석으로 첨부되어야 합니다.  
  
 자세한 내용은 [SqlUserDefinedAggregateAttribute](/dotnet/api/microsoft.sqlserver.server.sqluserdefinedaggregateattribute)를 참조 하세요.  
  
## <a name="the-sqlfunction-attribute"></a>SqlFunction 특성  
 **Sqlfunction** 특성은 적절 한 함수 특성을 설정 하 여 메서드를 함수로 등록 해야 함을 나타냅니다.  
  
 자세한 내용은 [SqlFunctionAttribute](/dotnet/api/microsoft.sqlserver.server.sqlfunctionattribute)를 참조 하세요.  
  
## <a name="the-sqlfacet-attribute"></a>SqlFacet 특성  
 **Sqlfacet** 특성은 UDT (사용자 정의 형식) 식의 반환 형식에 대 한 정보를 반환 하는 데 사용 됩니다.  
  
 자세한 내용은 [SqlFacetAttribute](/dotnet/api/microsoft.sqlserver.server.sqlfacetattribute)를 참조 하세요.  
  
## <a name="the-sqlprocedure-attribute"></a>SqlProcedure 특성  
 **Sqlprocedure** 특성은 메서드를 저장 프로시저로 등록 해야 함을 나타냅니다. 이 특성은 Visual Studio에서 지정한 메서드를 저장 프로시저로 자동으로 등록하는 데만 사용되며 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서는 사용되지 않습니다.  
  
 자세한 내용은 [SqlProcedureAttribute](/dotnet/api/microsoft.sqlserver.server.sqlprocedureattribute)를 참조 하세요.  
  
## <a name="the-sqltrigger-attribute"></a>SqlTrigger 특성  
 **Sqltrigger** 특성은 메서드를 트리거로 등록 해야 함을 나타냅니다.  
  
 자세한 내용은 [Sqltriggercontext](/dotnet/api/microsoft.sqlserver.server.sqltriggercontext) 및 [sqltriggercontext](/dotnet/api/microsoft.sqlserver.server.sqltriggerattribute)를 참조 하십시오.  
  
## <a name="the-sqluserdefinedtypeattribute"></a>SqlUserDefinedTypeAttribute  
 어셈블리의 클래스 정의에 SqlUserDefinedTypeAttribute를 적용할 수 있습니다. 이렇게 하면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 이 사용자 지정 특성을 가진 클래스 정의에 바인딩되는 사용자 정의 형식을 만듭니다.  
  
 자세한 내용은 [SqlUserDefinedTypeAttribute](/dotnet/api/microsoft.sqlserver.server.sqluserdefinedtypeattribute)를 참조 하세요.  
  
## <a name="the-sqlmethod-attribute"></a>SqlMethod 특성  
 **Sqlmethod** 특성은 UDT의 메서드 또는 속성의 명확성 및 데이터 액세스 속성을 나타내는 데 사용 됩니다.  
  
 자세한 내용은 [SqlMethodAttribute](/dotnet/api/microsoft.sqlserver.server.sqlmethodattribute)를 참조 하세요.  
  
## <a name="see-also"></a>참고 항목  
 [CLR 사용자 정의 집계](../../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-aggregates.md)   
 [CLR 사용자 정의 함수](../../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-functions.md)   
 [CLR 사용자 정의 형식](../../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)   
 [CLR 저장 프로시저](/dotnet/framework/data/adonet/sql/clr-stored-procedures)   
 [CLR 트리거](/dotnet/framework/data/adonet/sql/clr-triggers)  
  
