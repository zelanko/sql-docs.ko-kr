---
title: 개체 (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
topic_type:
- apiref
- apinav
helpviewer_keywords:
- objects [XML for Analysis]
- XML for Analysis, objects
- XMLA, objects
ms.assetid: 768188ef-85d4-432a-9390-be05c835137f
caps.latest.revision: 13
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 98ff50749cc45b5ffe4343acc19668f4dd0db126
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36082343"
---
# <a name="objects-xmla"></a>개체(XMLA)
  XMLA(XML for Analysis) 프로토콜은 `Discover` 및 `Execute`와 같은 두 메서드를 사용하여 응용 프로그램이 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스의 정보에 액세스할 수 있는 표준 방법을 제공합니다. 이 두 메서드는 SOAP(Simple Object Access Protocol) 프로토콜을 통해 호출되므로 XML로 입력을 받고 출력을 전달합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 다음 항목에서는 [!INCLUDE[ssAS](../../includes/ssas-md.md)]에서 구현하는 XMLA 개체에 대해 설명합니다.  
  
|메서드|Description|  
|------------|-----------------|  
|[DiscoverResponse 요소 &#40;XMLA&#41;](xml-elements-objects-discoverresponse.md)|인스턴스에서 반환한 정보를 포함 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에 대 한 응답에는 [Discover](xml-elements-methods-discover.md) 메서드를 호출 합니다.|  
|[ExecuteResponse 요소 &#40;XMLA&#41;](xml-elements-objects-executeresponse.md)|인스턴스에서 반환한 정보를 포함 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에 대 한 응답에는 [Execute](xml-elements-methods-execute.md) 메서드를 호출 합니다.|  
  
## <a name="see-also"></a>관련 항목  
 [XML 요소 &#40;XMLA&#41;](../dev-guide/xml-elements-xmla.md)   
 [XML 데이터 형식 &#40;XMLA&#41;](xml-data-types/xml-data-types-xmla.md)   
 [XML 요소 &#40;XMLA&#41;](../dev-guide/xml-elements-xmla.md)  
  
  