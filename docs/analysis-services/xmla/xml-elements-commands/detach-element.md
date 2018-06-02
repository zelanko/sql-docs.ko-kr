---
title: Detach 요소 | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b92798e16b701bb7073b26823fffc4f34a570f1c
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/02/2018
ms.locfileid: "34577755"
---
# <a name="detach-element"></a>Detach 요소
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  현재 서버 인스턴스에서 Analysis Services 데이터베이스를 분리합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Command>  
   <Detach>  
      <Object>...</Object>  
      <Password>...</Password>  
   </Detach>  
</Command>  
  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|InclusionThresholdSetting|  
|기본값|InclusionThresholdSetting|  
|카디널리티|0-n: 두 번 이상 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[Command](../../../analysis-services/xmla/xml-elements-properties/command-element-xmla.md)|  
|자식 요소|[개체](../../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md)<br /><br /> [암호](../../../analysis-services/xmla/xml-elements-properties/password-element-xmla.md)|  
  
## <a name="see-also"></a>참고자료
 <xref:Microsoft.AnalysisServices.Database.Detach%2A>   
 [Attach 요소](../../../analysis-services/xmla/xml-elements-commands/attach-element.md)   
 [Analysis Services 데이터베이스 연결 및 분리](../../../analysis-services/multidimensional-models/attach-and-detach-analysis-services-databases.md)   
 [Analysis Services 데이터베이스 이동](../../../analysis-services/multidimensional-models/move-an-analysis-services-database.md)   
 [Readwritemode 데이터베이스](../../../analysis-services/multidimensional-models/database-readwritemodes.md)   
 [ReadOnly 및 ReadWrite 모드 간 Analysis Services 데이터베이스 전환](../../../analysis-services/multidimensional-models/switch-an-analysis-services-database-between-readonly-and-readwrite-modes.md)  
  
  
