---
title: "Subscribe 요소 (XMLA) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: xmla
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- Subscribe Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Subscribe
- microsoft.xml.analysis.subscribe
- http://schemas.microsoft.com/analysisservices/2003/engine#Subscribe
helpviewer_keywords:
- Subscribe command
ms.assetid: aad50dd7-44d4-4d83-a973-187f9aed35ec
caps.latest.revision: 14
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d0af4762aec4d048f19ee47f8d07445aa5e7a8b3
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="subscribe-element-xmla"></a>Subscribe 요소(XMLA)
  추적에 구독 하 고 추적 이벤트를 포함 하는 행 집합을 반환 된 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Command>  
   <Subscribe>  
      <Object>...</Object>  
   </Subscribe>  
</Command>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|없음|  
|기본값|없음|  
|카디널리티|0-n: 두 번 이상 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[Command](../../../analysis-services/xmla/xml-elements-properties/command-element-xmla.md)|  
|자식 요소|[개체](../../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md)|  
  
## <a name="remarks"></a>주의  
 **Subscribe** 명령을 구독 하 고 스트림이 지정된 된 추적의 행 집합에서 다시는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스. 추적 이외의 개체가 **Object** 요소에 지정된 경우 오류가 발생합니다.  
  
 경우는 **개체** 요소가 지정 되지 않은, 세션 추적을 정의 하 고 구독 합니다는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스. 세션 추적은 현재 세션의 고정된 추적 이벤트 집합을 반환합니다.  
  
 클라이언트 응용 프로그램에 대 한 연결을 종료 하는 경우이 명령에서 반환 된 행 집합 스트림이 종료 됩니다는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스, 또는 세션을는 **가입** 명령을 실행 종료 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [명령 &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  

