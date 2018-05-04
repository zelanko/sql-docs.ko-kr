---
title: Unlock 요소 (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- Unlock Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Unlock
- urn:schemas-microsoft-com:xml-analysis#Unlock
- microsoft.xml.analysis.unlock
helpviewer_keywords:
- Unlock command
ms.assetid: 46425b33-baa2-41ad-803a-34d2fb4b2cab
caps.latest.revision: 14
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 37fb814e22796dd807207015d6927ff9e4dc7498
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="unlock-element-xmla"></a>Unlock 요소(XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  에 지정된 된 잠금을 해제 한 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Command>  
   <Unlock>  
      <ID>...</ID>  
   </Unlock>  
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
|자식 요소|[ID](../../../analysis-services/xmla/xml-elements-properties/id-element-xmla.md)|  
  
## <a name="remarks"></a>주의  
 **Unlock** 명령은 현재 활성 트랜잭션 컨텍스트 내에서 설정된 잠금을 해제합니다. 데이터베이스 관리자 또는 서버 관리자만 명시적으로 **Unlock** 명령을 실행할 수 있습니다.  
  
 모든 잠금은 현재 트랜잭션의 컨텍스트에 유지됩니다. 현재 트랜잭션이 커밋 또는 롤백되면 해당 트랜잭션 내에 정의된 모든 잠금이 자동으로 해제됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [요소를 잠급니다 &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-commands/lock-element-xmla.md)   
 [명령 & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  
