---
title: CLR 루틴에 대 한 사용자 지정 특성 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
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
caps.latest.revision: 82
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 21bb0d5bd6ea5dfe672b47ee9095416da6267dbf
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36088865"
---
# <a name="custom-attributes-for-clr-routines"></a>CLR 루틴용 사용자 지정 특성
  공용 언어 런타임 (CLR) 루틴, 사용자 정의 형식 및에 등록 된 사용자 정의 집계에 나열 된 특성을 적용할 수 [!INCLUDE[msCoName](../../../includes/ssnoversion-md.md)]합니다. 특성이 적용되지 않으면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]는 기본값을 사용합니다. 나열된 특성은 `Microsoft.SqlServer.Server` 네임스페이스에 정의됩니다.  
  
## <a name="the-sqluserdefinedaggregate-attribute"></a>SqlUserDefinedAggregate 특성  
 `SqlUserDefinedAggregate` 특성은 메서드를 사용자 정의 집계로 등록해야 함을 나타냅니다. 모든 사용자 정의 집계에는 이 특성이 주석으로 첨부되어야 합니다.  
  
 자세한 내용은 참조 [SqlUserDefinedAggregateAttribute](http://go.microsoft.com/fwlink/?LinkId=124626)합니다.  
  
## <a name="the-sqlfunction-attribute"></a>SqlFunction 특성  
 `SqlFunction` 특성은 적절한 함수 특성 집합을 사용하여 메서드를 함수로 등록해야 함을 나타냅니다.  
  
 자세한 내용은 참조 [SqlFunctionAttribute](http://go.microsoft.com/fwlink/?LinkId=128019)합니다.  
  
## <a name="the-sqlfacet-attribute"></a>SqlFacet 특성  
 `SqlFacet` 특성은 UDT(사용자 정의 형식) 식의 반환 형식에 대한 정보를 반환하는 데 사용됩니다.  
  
 자세한 내용은 참조 [SqlFacetAttribute](http://go.microsoft.com/fwlink/?LinkId=128020)합니다.  
  
## <a name="the-sqlprocedure-attribute"></a>SqlProcedure 특성  
 `SqlProcedure` 특성은 메서드를 저장 프로시저로 등록해야 함을 나타냅니다. 이 특성은 Visual Studio에서 지정한 메서드를 저장 프로시저로 자동으로 등록하는 데만 사용되며 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서는 사용되지 않습니다.  
  
 자세한 내용은 참조 [SqlProcedureAttribute](http://go.microsoft.com/fwlink/?LinkId=128021)합니다.  
  
## <a name="the-sqltrigger-attribute"></a>SqlTrigger 특성  
 `SqlTrigger` 특성은 메서드를 트리거로 등록해야 함을 나타냅니다.  
  
 자세한 내용은 참조 [SqlTriggerContext](http://go.microsoft.com/fwlink/?LinkId=128022) 및 [SqlTriggerAttribute](http://go.microsoft.com/fwlink/?LinkId=203898)합니다.  
  
## <a name="the-sqluserdefinedtypeattribute"></a>SqlUserDefinedTypeAttribute  
 어셈블리의 클래스 정의에 SqlUserDefinedTypeAttribute를 적용할 수 있습니다. 이렇게 하면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 이 사용자 지정 특성을 가진 클래스 정의에 바인딩되는 사용자 정의 형식을 만듭니다.  
  
 자세한 내용은 참조 [SqlUserDefinedTypeAttribute](http://go.microsoft.com/fwlink/?LinkId=128024)합니다.  
  
## <a name="the-sqlmethod-attribute"></a>SqlMethod 특성  
 `SqlMethod` 특성은 UDT의 속성 또는 메서드의 결정성 및 데이터 액세스 속성을 나타내는 데 사용됩니다.  
  
 자세한 내용은 참조 [SqlMethodAttribute](http://go.microsoft.com/fwlink/?LinkId=128025)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [CLR 사용자 정의 집계](../../clr-integration-database-objects-user-defined-functions/clr-user-defined-aggregates.md)   
 [CLR 사용자 정의 함수](../../clr-integration-database-objects-user-defined-functions/clr-user-defined-functions.md)   
 [CLR 사용자 정의 형식](../../clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)   
 [CLR 저장 프로시저](../../../database-engine/dev-guide/clr-stored-procedures.md)   
 [CLR 트리거](../../../database-engine/dev-guide/clr-triggers.md)  
  
  