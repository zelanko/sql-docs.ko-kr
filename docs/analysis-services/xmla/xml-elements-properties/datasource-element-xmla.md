---
title: DataSource 요소 (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 2660cb47f492b74001e6ba0ce0b4fdc9da44f7d9
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="datasource-element-xmla"></a>DataSource 요소(XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  부모에 대 한 아웃오브 라인 데이터 원본 바인딩을 포함 [일괄 처리](../../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md) 또는 [프로세스](../../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Batch> <!-- or Process>  
...  
   <DataSource>  
      <DatabaseID>...</DatabaseID>  
      <DataSourceID>...</DataSourceID>  
   </DataSource>  
...  
</Batch>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|없음|  
|기본값|없음|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[Batch](../../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md), [Process](../../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md)|  
|자식 요소|[DatabaseID](../../../analysis-services/xmla/xml-elements-properties/databaseid-element-xmla.md), [DataSourceID](../../../analysis-services/xmla/xml-elements-properties/datasourceid-element-xmla.md)|  
  
## <a name="remarks"></a>주의  
 **DataSource** 요소에 사용 되는 데이터 원본에 대 한 아웃오브 라인 바인딩을 나타냅니다는 **일괄 처리** 또는 **프로세스** 명령에 대 한 데이터 원본 바인딩을 임시로 재정의 하려면 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 명령으로 처리 하는 개체입니다.  
  
 아웃오브 라인 바인딩에 대 한 자세한 내용은 참조 하십시오. [데이터 원본 및 바인딩 & #40; SSAS 다차원 & #41; ](../../../analysis-services/multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).  
  
## <a name="see-also"></a>관련 항목:  
 [속성 & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
