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
ms.openlocfilehash: 15f930695e13d824e70da748dad20cf574e9bc38
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34579145"
---
# <a name="xml-elements---methods"></a>XML 요소-메서드
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  두 메서드를 사용 하는 XML for Analysis (XMLA) 프로토콜 **Discover** 및 **Execute**, 응용 프로그램이 Analysis Services 인스턴스에 대 한 정보에 액세스 하기 위한 표준 방법을 제공 합니다. 이 두 메서드는 SOAP(Simple Object Access Protocol) 프로토콜을 통해 호출되므로 XML로 입력을 받고 출력을 전달합니다. Analysis Services에는 XML for Analysis 1.1 사양 준수 두 메서드를 구현 합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 다음 항목에는 Analysis Services에 의해 구현 되는 XMLA 메서드에 대해 설명 합니다.  
  
|메서드|Description|  
|------------|-----------------|  
|[Discover 메서드 &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-methods-discover.md)|Analysis Services의 인스턴스에서 특정 개체에 대 한 정보 또는 사용 가능한 데이터베이스 목록과 같은 정보를 검색합니다. **Discover** 메서드로 검색되는 데이터는 해당 메서드로 전달되는 매개 변수의 값에 따라 달라집니다.|  
|[Execute 메서드 &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-methods-execute.md)|Analysis Services의 인스턴스로 XMLA 명령을 보냅니다. 여기에는 서버의 데이터 검색 또는 업데이트와 같은 데이터 전송 관련 요청이 포함됩니다.|  
  
## <a name="see-also"></a>참고자료
 [XML 요소 &#40;XMLA&#41;](http://msdn.microsoft.com/library/40ab2360-efb6-4ba6-bf23-e84964e51008)   
 [XML 데이터 형식 &#40;XMLA&#41;](../../analysis-services/xmla/xml-data-types/xml-data-types-xmla.md)   
 [XML 요소 &#40;XMLA&#41;](http://msdn.microsoft.com/library/40ab2360-efb6-4ba6-bf23-e84964e51008)  
  
  
