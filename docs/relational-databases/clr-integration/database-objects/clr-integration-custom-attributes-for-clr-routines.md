---
title: CLR 루틴에 대 한 사용자 지정 특성 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: clr
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
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
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: f5672efbc82371c5447fc927b208e41efad20d2d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32924668"
---
# <a name="clr-integration-custom-attributes-for-clr-routines"></a>CLR 루틴에 대 한 CLR 통합 사용자 지정 특성
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  공용 언어 런타임 (CLR) 루틴, 사용자 정의 형식 및에 등록 된 사용자 정의 집계에 나열 된 특성을 적용할 수 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]합니다. 특성이 적용되지 않으면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]는 기본값을 사용합니다. 나열 된 특성에 정의 된는 **Microsoft.SqlServer.Server** 네임 스페이스입니다.  
  
## <a name="the-sqluserdefinedaggregate-attribute"></a>SqlUserDefinedAggregate 특성  
 **SqlUserDefinedAggregate** 특성을 사용자 정의 집계로 메서드를 등록 해야 함을 나타냅니다. 모든 사용자 정의 집계에는 이 특성이 주석으로 첨부되어야 합니다.  
  
 자세한 내용은 참조 [SqlUserDefinedAggregateAttribute](http://go.microsoft.com/fwlink/?LinkId=124626)합니다.  
  
## <a name="the-sqlfunction-attribute"></a>SqlFunction 특성  
 **SqlFunction** 특성 메서드 적절 한 함수 특성 집합으로 함수를 등록 해야 함을 나타냅니다.  
  
 자세한 내용은 참조 [SqlFunctionAttribute](http://go.microsoft.com/fwlink/?LinkId=128019)합니다.  
  
## <a name="the-sqlfacet-attribute"></a>SqlFacet 특성  
 **SqlFacet** 특성 사용자 정의 형식 (UDT) 식의 반환 형식에 대 한 정보를 반환 하는 데 사용 됩니다.  
  
 자세한 내용은 참조 [SqlFacetAttribute](http://go.microsoft.com/fwlink/?LinkId=128020)합니다.  
  
## <a name="the-sqlprocedure-attribute"></a>SqlProcedure 특성  
 **SqlProcedure** 특성 메서드 저장 프로시저로 등록 해야 함을 나타냅니다. 이 특성은 Visual Studio에서 지정한 메서드를 저장 프로시저로 자동으로 등록하는 데만 사용되며 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서는 사용되지 않습니다.  
  
 자세한 내용은 참조 [SqlProcedureAttribute](http://go.microsoft.com/fwlink/?LinkId=128021)합니다.  
  
## <a name="the-sqltrigger-attribute"></a>SqlTrigger 특성  
 **SqlTrigger** 특성 나타냅니다는 메서드를 트리거로 등록 해야 합니다.  
  
 자세한 내용은 참조 [SqlTriggerContext](http://go.microsoft.com/fwlink/?LinkId=128022) 및 [SqlTriggerAttribute](http://go.microsoft.com/fwlink/?LinkId=203898)합니다.  
  
## <a name="the-sqluserdefinedtypeattribute"></a>SqlUserDefinedTypeAttribute  
 어셈블리의 클래스 정의에 SqlUserDefinedTypeAttribute를 적용할 수 있습니다. 이렇게 하면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 이 사용자 지정 특성을 가진 클래스 정의에 바인딩되는 사용자 정의 형식을 만듭니다.  
  
 자세한 내용은 참조 [SqlUserDefinedTypeAttribute](http://go.microsoft.com/fwlink/?LinkId=128024)합니다.  
  
## <a name="the-sqlmethod-attribute"></a>SqlMethod 특성  
 **SqlMethod** 특성은 UDT의 속성 또는 메서드의 결정성 및 데이터 액세스 속성을 나타내는 데 사용 됩니다.  
  
 자세한 내용은 참조 [SqlMethodAttribute](http://go.microsoft.com/fwlink/?LinkId=128025)합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [CLR 사용자 정의 집계](../../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-aggregates.md)   
 [CLR 사용자 정의 함수](../../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-functions.md)   
 [CLR 사용자 정의 형식](../../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)   
 [CLR 저장 프로시저](http://msdn.microsoft.com/library/bbdd51b2-a9b4-4916-ba6f-7957ac6c3f33)   
 [CLR 트리거](http://msdn.microsoft.com/library/302a4e4a-3172-42b6-9cc0-4a971ab49c1c)  
  
  
