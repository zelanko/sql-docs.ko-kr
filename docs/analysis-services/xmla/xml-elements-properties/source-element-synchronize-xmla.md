---
title: Source 요소 (Synchronize) (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: dc3767c1253cdfa613f7f5866963348bd90ad179
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="source-element-synchronize-xmla"></a>Source 요소(Synchronize)(XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  동기화 중에 대상 데이터베이스를 원본 데이터베이스 나타냅니다는 [동기화](../../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md) 명령입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Synchronize>  
   <Source>  
      <Object>...</Object>  
      <ConnectionString>...</ConnectionString>  
   </Source>  
</Synchronize>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|없음|  
|기본값|없음|  
|카디널리티|1-1: 한 번만 나타나는 필수 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[동기화](../../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md)|  
|자식 요소|[ConnectionString](../../../analysis-services/xmla/xml-elements-properties/connectionstring-element-xmla.md), [개체](../../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md)|  
  
## <a name="remarks"></a>주의  
 **동기화** 명령을 사용 하 여는 **소스** 요소에 대 한 연결을 설정 하 고의 인스턴스에서 데이터베이스를 식별 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 에 동기화 할 대상 데이터베이스입니다.  
  
## <a name="see-also"></a>관련 항목:  
 [속성 & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
