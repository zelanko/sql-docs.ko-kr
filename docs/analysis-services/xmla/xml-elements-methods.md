---
title: 메서드 (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f42c986f8ebb3be2126335663a0716049e908ab0
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="xml-elements---methods"></a>XML 요소-메서드
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  두 메서드를 사용 하는 XML for Analysis (XMLA) 프로토콜 **Discover** 및 **Execute**, 응용 프로그램이 인스턴스의 정보에 액세스 하기 위한 표준 방법을 제공 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. 이 두 메서드는 SOAP(Simple Object Access Protocol) 프로토콜을 통해 호출되므로 XML로 입력을 받고 출력을 전달합니다. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]는 이 두 메서드를 구현할 때 XMLA(XML for Analysis) 1.1 사양을 준수합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 다음 항목에서는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서 구현되는 XMLA 메서드에 대해 설명합니다.  
  
|메서드|Description|  
|------------|-----------------|  
|[Discover 메서드 &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-methods-discover.md)|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스에서 사용 가능한 데이터베이스 목록 또는 특정 개체에 대한 세부 정보와 같은 정보를 검색합니다. **Discover** 메서드로 검색되는 데이터는 해당 메서드로 전달되는 매개 변수의 값에 따라 달라집니다.|  
|[Execute 메서드 &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-methods-execute.md)|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스로 XMLA(XML for Analysis) 명령을 보냅니다. 여기에는 서버의 데이터 검색 또는 업데이트와 같은 데이터 전송 관련 요청이 포함됩니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [XML 요소 & #40; XMLA & #41;](http://msdn.microsoft.com/library/40ab2360-efb6-4ba6-bf23-e84964e51008)   
 [XML 데이터 형식 & #40; XMLA & #41;](../../analysis-services/xmla/xml-data-types/xml-data-types-xmla.md)   
 [XML 요소 & #40; XMLA & #41;](http://msdn.microsoft.com/library/40ab2360-efb6-4ba6-bf23-e84964e51008)  
  
  
