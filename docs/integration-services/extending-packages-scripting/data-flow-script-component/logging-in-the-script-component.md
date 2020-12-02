---
description: 스크립트 구성 요소의 로깅
title: 스크립트 구성 요소의 로깅 | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- Script component [Integration Services], logging
ms.assetid: 17c19787-379e-43fe-9107-e36e17ecda53
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 9d761fd4bd949f066a7dc0c59a69efa4a46edfff
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/26/2020
ms.locfileid: "88430295"
---
# <a name="logging-in-the-script-component"></a>스크립트 구성 요소의 로깅

[!INCLUDE[sqlserver-ssis](../../../includes/applies-to-version/sqlserver-ssis.md)]


  [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 패키지의 로깅 기능을 사용하면 나중에 분석할 수 있도록 미리 정의된 이벤트나 사용자 정의 메시지를 기록하여 실행 진행률, 결과 및 문제에 대한 세부 정보를 저장할 수 있습니다. 스크립트 구성 요소에서는 **ScriptMain** 클래스의 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.Log%2A> 메서드를 사용하여 사용자 정의 데이터를 로깅할 수 있습니다. 로깅을 사용하도록 설정하고 **SSIS 로그 구성** 대화 상자의 **자세히** 탭에서 **ScriptComponentLogEntry** 이벤트를 로깅하도록 선택할 경우 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.Log%2A> 메서드를 한 번만 호출하면 데이터 흐름 태스크에 대해 구성된 모든 로그 공급자에 해당 이벤트 정보가 저장됩니다.  
  
 다음은 간단한 로깅 예입니다.  
  
 `Dim bt(0) As Byte`  
  
 `Me.Log("Test Log Event", _`  
  
 `0, _`  
  
 `bt)`  
  
> [!NOTE]  
>  스크립트 구성 요소에서 직접 로깅을 수행할 수도 있지만 로깅보다는 이벤트를 구현하는 것이 좋습니다. 이벤트를 사용하면 이벤트 메시지의 로깅 기능을 사용할 수 있을 뿐 아니라 기본 또는 사용자 정의 이벤트 처리기를 사용하여 이벤트에 응답할 수도 있습니다.  
  
 로깅에 대한 자세한 내용은 [Integration Services&#40;SSIS&#41; 로깅](../../../integration-services/performance/integration-services-ssis-logging.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [Integration Services&#40;SSIS&#41; 로깅](../../../integration-services/performance/integration-services-ssis-logging.md)  
  
  
