---
title: 스크립트 구성 요소에서 이벤트 발생 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- Script component [Integration Services], raising events
ms.assetid: bb389073-e1d0-4794-8d29-c8b293b6a5e3
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: fc66918159a880b68b76acd027f81458149cc351
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62895002"
---
# <a name="raising-events-in-the-script-component"></a>스크립트 구성 요소에서 이벤트 발생
  이벤트를 사용하면 포함하는 패키지에 오류 및 경고와 태스크 진행률 또는 상태 같은 기타 정보를 보고할 수 있습니다. 패키지에서는 이벤트 알림을 관리하기 위한 이벤트 처리기를 제공합니다. 스크립트 구성 요소에서는 `ScriptMain` 클래스의 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ComponentMetaData%2A> 속성에서 메서드를 호출하여 이벤트를 발생시킬 수 있습니다. [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 패키지 처리 이벤트에 대한 자세한 내용은 [Integration Services&#40;SSIS&#41; 이벤트 처리기](../../integration-services-ssis-event-handlers.md)를 참조하세요.  
  
 이벤트는 패키지에서 사용할 수 있도록 설정된 모든 로그 공급자에 로깅될 수 있습니다. 로그 공급자는 이벤트에 대한 정보를 데이터 원본에 저장합니다. 스크립트 구성 요소에서는 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.Log%2A> 메서드를 사용하여 이벤트를 발생시키지 않고 로그 공급자에 정보를 로깅할 수도 있습니다. <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.Log%2A> 메서드의 사용 방법은 다음 섹션을 참조하십시오.  
  
 이벤트를 발생시키기 위해 스크립트 태스크에서는 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100> 속성에 의해 제공된 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ComponentMetaData%2A> 인터페이스의 다음 메서드 중 하나를 호출합니다.  
  
|이벤트|Description|  
|-----------|-----------------|  
|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.FireCustomEvent%2A>|패키지에서 사용자가 정의한 사용자 지정 이벤트를 발생시킵니다.|  
|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.FireError%2A>|패키지에 오류 조건을 알립니다.|  
|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.FireInformation%2A>|사용자에게 정보를 제공합니다.|  
|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.FireProgress%2A>|패키지에 구성 요소 진행률을 알립니다.|  
|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.FireWarning%2A>|구성 요소가 사용자 알림이 발생할 수 있지만 오류 조건은 아닌 상태에 있음을 패키지에 알립니다.|  
  
 다음은 Error 이벤트를 발생시키는 간단한 예입니다.  
  
 `Dim myMetadata as IDTSComponentMetaData100`  
  
 `myMetaData = Me.ComponentMetaData`  
  
 `myMetaData.FireError(...)`  
  
![Integration Services 아이콘 (작은)](../../media/dts-16.gif "Integration Services 아이콘 (작은)")**Integration Services를 사용 하 여 날짜를 알림 설정**<br /> Microsoft의 최신 다운로드, 문서, 예제 및 비디오와 커뮤니티에서 선택된 솔루션을 보려면 MSDN의 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 페이지를 방문하세요.<br /><br /> [MSDN의 Integration Services 페이지 방문](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 이러한 업데이트에 대한 자동 알림을 받으려면 해당 페이지에서 제공하는 RSS 피드를 구독하세요.  
  
## <a name="see-also"></a>관련 항목  
 [Integration Services&#40;SSIS&#41; 이벤트 처리기](../../integration-services-ssis-event-handlers.md)   
 [패키지에 이벤트 처리기 추가](../../add-an-event-handler-to-a-package.md)  
  
  
