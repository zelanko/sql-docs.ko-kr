---
title: "저장 프로시저의 쿼리 컨텍스트 액세스 | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- execution context [Analysis Services]
- stored procedures [Analysis Services], query context
- Context object
- query context [Analysis Services]
ms.assetid: bdc7dad8-2f22-4265-aba4-a3a451527840
caps.latest.revision: "22"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 5b7a0c3e57a5249a26bf13a2cf9709e58df85da8
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="accessing-query-context-in-stored-procedures"></a>저장 프로시저의 쿼리 컨텍스트 액세스
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]저장된 프로시저의 실행 컨텍스트는 저장된 프로시저 코드 내에서 사용할 수는 **컨텍스트** ADOMD.NET 서버 개체 모델의 개체입니다. 이것은 읽기 전용 컨텍스트이며 저장 프로시저로 수정할 수 없습니다. 이 개체에 다음 속성을 사용할 수 있습니다.  
  
|속성|형식|Description|  
|--------------|----------|-----------------|  
|**CurrentCube**|Cube|현재 쿼리 컨텍스트에 대한 큐브입니다.|  
|**CurrentDatabaseName**|String|현재 데이터베이스의 식별자입니다.|  
|**CurrentConnection**|연결|현재 컨텍스트의 연결 개체에 대한 참조입니다.|  
|**전달**|정수|현재 컨텍스트의 패스 번호입니다.|  
  
 **컨텍스트** 개체가 저장된 프로시저에서 MDX (Multidimensional Expressions) 개체 모델을 사용할 때 존재 합니다. 그러나 클라이언트에서 MDX 개체 모델을 사용할 경우에는 이 개체를 사용할 수 없습니다. **컨텍스트** 개체가 명시적으로 전달 또는 저장된 프로시저에서 반환 합니다. 이 개체는 저장 프로시저 실행 중에만 사용할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [다차원 모델 어셈블리 관리](../../analysis-services/multidimensional-models/multidimensional-model-assemblies-management.md)   
 [저장 프로시저 정의](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/defining-stored-procedures.md)  
  
  
