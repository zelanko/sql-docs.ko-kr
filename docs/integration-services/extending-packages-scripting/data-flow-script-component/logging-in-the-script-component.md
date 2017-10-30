---
title: "스크립트 구성 요소에서 로깅 | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- Script component [Integration Services], logging
ms.assetid: 17c19787-379e-43fe-9107-e36e17ecda53
caps.latest.revision: 14
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 410a2472399574753d67a44b93437b1698c8b086
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="logging-in-the-script-component"></a>스크립트 구성 요소의 로깅
  [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 패키지의 로깅 기능을 사용하면 나중에 분석할 수 있도록 미리 정의된 이벤트나 사용자 정의 메시지를 기록하여 실행 진행률, 결과 및 문제에 대한 세부 정보를 저장할 수 있습니다. 스크립트 구성 요소에서 사용할 수는 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.Log%2A> 의 메서드는 **ScriptMain** 사용자 정의 데이터를 기록 하는 클래스입니다. 로깅이 설정 된 경우와 **ScriptComponentLogEntry** 이벤트가 로깅 대상으로 선택 되어는 **세부 정보** 탭은 **SSIS 로그 구성** 대화 상자, 한 번 호출 하는 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.Log%2A> 메서드는 데이터 흐름 태스크에 대해 구성 된 모든 로그 공급자에 이벤트 정보를 저장 합니다.  
  
 다음은 간단한 로깅 예입니다.  
  
 `Dim bt(0) As Byte`  
  
 `Me.Log("Test Log Event", _`  
  
 `0, _`  
  
 `bt)`  
  
> [!NOTE]  
>  스크립트 구성 요소에서 직접 로깅을 수행할 수도 있지만 로깅보다는 이벤트를 구현하는 것이 좋습니다. 이벤트를 사용하면 이벤트 메시지의 로깅 기능을 사용할 수 있을 뿐 아니라 기본 또는 사용자 정의 이벤트 처리기를 사용하여 이벤트에 응답할 수도 있습니다.  
  
 로깅에 대 한 자세한 내용은 참조 [Integration services&#40; Ssis&#41; 로깅](../../../integration-services/performance/integration-services-ssis-logging.md)합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Integration Services &#40; Ssis&#41; 로깅](../../../integration-services/performance/integration-services-ssis-logging.md)  
  
  

