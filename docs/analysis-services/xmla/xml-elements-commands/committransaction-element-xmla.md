---
title: CommitTransaction 요소 (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5ade8d12812212193a082afddf1504eebadb270e
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/02/2018
ms.locfileid: "34575055"
---
# <a name="committransaction-element-xmla"></a>CommitTransaction 요소(XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Analysis Services 인스턴스로 현재 세션에서 트랜잭션을 커밋합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Command>  
   <CommitTransaction />  
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
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 **CommitTransaction** 명령은 현재 세션에서 **BeginTransaction** 요소를 사용하여 명시적으로 정의된 활성 트랜잭션을 커밋합니다. 활성 트랜잭션이 없으면 오류가 발생합니다. 이미 활성 트랜잭션이 있는 경우 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스는 현재 세션에 대한 트랜잭션의 참조 수를 줄입니다. 명시적으로 정의된 활성 트랜잭션의 참조 수가 0이 되면 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스가 트랜잭션을 커밋합니다.  
  
## <a name="see-also"></a>참고자료
 [BeginTransaction 요소 &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-commands/begintransaction-element-xmla.md)   
 [Cancel 요소 &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-commands/cancel-element-xmla.md)   
 [RollbackTransaction 요소 &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-commands/rollbacktransaction-element-xmla.md)   
 [명령 &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  
