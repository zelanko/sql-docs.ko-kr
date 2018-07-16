---
title: 메서드 (XMLA) | Microsoft Docs
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
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#
helpviewer_keywords:
- methods [XML for Analysis]
- XML for Analysis, methods
- XMLA, methods
ms.assetid: c6768dd4-ca06-4a85-93b7-5fd5700886ad
caps.latest.revision: 30
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1baf254e9965153394a3a7b1367ced21c009a7f4
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37171424"
---
# <a name="methods-xmla"></a>메서드(XMLA)
  XMLA(XML for Analysis) 프로토콜은 `Discover` 및 `Execute`와 같은 두 메서드를 사용하여 응용 프로그램이 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스의 정보에 액세스할 수 있는 표준 방법을 제공합니다. 이 두 메서드는 SOAP(Simple Object Access Protocol) 프로토콜을 통해 호출되므로 XML로 입력을 받고 출력을 전달합니다. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]는 이 두 메서드를 구현할 때 XMLA(XML for Analysis) 1.1 사양을 준수합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 다음 항목에서는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서 구현되는 XMLA 메서드에 대해 설명합니다.  
  
|메서드|Description|  
|------------|-----------------|  
|[Discover 메서드 &#40;XMLA&#41;](xml-elements-methods-discover.md)|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스에서 사용 가능한 데이터베이스 목록 또는 특정 개체에 대한 세부 정보와 같은 정보를 검색합니다. `Discover` 메서드로 검색된 데이터는 해당 메서드에 전달된 매개 변수 값에 따라 달라집니다.|  
|[메서드를 실행 &#40;XMLA&#41;](xml-elements-methods-execute.md)|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스로 XMLA(XML for Analysis) 명령을 보냅니다. 여기에는 서버의 데이터 검색 또는 업데이트와 같은 데이터 전송 관련 요청이 포함됩니다.|  
  
## <a name="see-also"></a>관련 항목  
 [XML 요소 &#40;XMLA&#41;](../dev-guide/xml-elements-xmla.md)   
 [XML 데이터 형식 &#40;XMLA&#41;](xml-data-types/xml-data-types-xmla.md)   
 [XML 요소 &#40;XMLA&#41;](../dev-guide/xml-elements-xmla.md)  
  
  
