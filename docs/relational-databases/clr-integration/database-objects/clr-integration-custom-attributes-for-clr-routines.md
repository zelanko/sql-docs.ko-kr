---
title: CLR 루틴용 사용자 지정 특성 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
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
caps.latest.revision: 82
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 865d305e5d85fd58ab85148f74cc5159323674bb
ms.sourcegitcommit: 022d67cfbc4fdadaa65b499aa7a6a8a942bc502d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37356125"
---
# <a name="clr-integration-custom-attributes-for-clr-routines"></a>CLR 루틴용 CLR 통합 사용자 지정 특성
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  공용 언어 런타임 (CLR) 루틴, 사용자 정의 형식에 등록 된 사용자 정의 집계를 나열 된 특성을 적용할 수 있습니다 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]합니다. 특성이 적용되지 않으면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]는 기본값을 사용합니다. 나열 된 특성에 정의 된 합니다 **Microsoft.SqlServer.Server** 네임 스페이스입니다.  
  
## <a name="the-sqluserdefinedaggregate-attribute"></a>SqlUserDefinedAggregate 특성  
 합니다 **SqlUserDefinedAggregate** 특성 메서드는 사용자 정의 집계로 등록 해야 함을 나타냅니다. 모든 사용자 정의 집계에는 이 특성이 주석으로 첨부되어야 합니다.  
  
 자세한 내용은 [SqlUserDefinedAggregateAttribute](http://go.microsoft.com/fwlink/?LinkId=124626)합니다.  
  
## <a name="the-sqlfunction-attribute"></a>SqlFunction 특성  
 합니다 **SqlFunction** 특성을 적절 한 함수 특성 집합을 사용 하 여 함수로 등록 해야 하는 메서드를 나타냅니다.  
  
 자세한 내용은 [SqlFunctionAttribute](http://go.microsoft.com/fwlink/?LinkId=128019)합니다.  
  
## <a name="the-sqlfacet-attribute"></a>SqlFacet 특성  
 합니다 **SqlFacet** 특성은 반환 형식의 사용자 정의 형식 (UDT) 식에 대 한 정보를 반환 하는 데 사용 됩니다.  
  
 자세한 내용은 [SqlFacetAttribute](http://go.microsoft.com/fwlink/?LinkId=128020)합니다.  
  
## <a name="the-sqlprocedure-attribute"></a>SqlProcedure 특성  
 합니다 **SqlProcedure** 특성 저장 프로시저로 등록 해야 하는 메서드를 나타냅니다. 이 특성은 Visual Studio에서 지정한 메서드를 저장 프로시저로 자동으로 등록하는 데만 사용되며 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서는 사용되지 않습니다.  
  
 자세한 내용은 [SqlProcedureAttribute](http://go.microsoft.com/fwlink/?LinkId=128021)합니다.  
  
## <a name="the-sqltrigger-attribute"></a>SqlTrigger 특성  
 합니다 **SqlTrigger** 특성 트리거로 등록 해야 하는 메서드를 나타냅니다.  
  
 자세한 내용은 [SqlTriggerContext](http://go.microsoft.com/fwlink/?LinkId=128022) 하 고 [SqlTriggerAttribute](http://go.microsoft.com/fwlink/?LinkId=203898)합니다.  
  
## <a name="the-sqluserdefinedtypeattribute"></a>SqlUserDefinedTypeAttribute  
 어셈블리의 클래스 정의에 SqlUserDefinedTypeAttribute를 적용할 수 있습니다. 이렇게 하면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 이 사용자 지정 특성을 가진 클래스 정의에 바인딩되는 사용자 정의 형식을 만듭니다.  
  
 자세한 내용은 [SqlUserDefinedTypeAttribute](http://go.microsoft.com/fwlink/?LinkId=128024)합니다.  
  
## <a name="the-sqlmethod-attribute"></a>SqlMethod 특성  
 합니다 **SqlMethod** 특성은 UDT의 속성 또는 메서드의 결정성 및 데이터 액세스 속성을 나타내는 데 사용 됩니다.  
  
 자세한 내용은 [SqlMethodAttribute](http://go.microsoft.com/fwlink/?LinkId=128025)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [CLR 사용자 정의 집계](../../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-aggregates.md)   
 [CLR 사용자 정의 함수](../../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-functions.md)   
 [CLR 사용자 정의 형식](../../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)   
 [CLR 저장 프로시저](http://msdn.microsoft.com/library/bbdd51b2-a9b4-4916-ba6f-7957ac6c3f33)   
 [CLR 트리거](http://msdn.microsoft.com/library/302a4e4a-3172-42b6-9cc0-4a971ab49c1c)  
  
  
