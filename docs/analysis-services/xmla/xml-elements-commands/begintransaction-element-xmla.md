---
title: "BeginTransaction 요소 (XMLA) | Microsoft Docs"
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
- BeginTransaction Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#BeginTransaction
- microsoft.xml.analysis.begintransaction
- http://schemas.microsoft.com/analysisservices/2003/engine#BeginTransaction
helpviewer_keywords:
- BeginTransaction command
ms.assetid: fca122fc-b57c-4ba6-849b-ca8c93cf64e9
caps.latest.revision: 14
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 677ad07e9ce6206bbc4e7946ec111f8865bcfcce
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="begintransaction-element-xmla"></a>BeginTransaction 요소(XMLA)
  인스턴스로 현재 세션에서 트랜잭션을 시작 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Command>  
   <BeginTransaction />  
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
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 **BeginTransaction** 명령은 현재 세션에서 활성 트랜잭션을 시작합니다. 활성 트랜잭션이 이미 있는 경우에는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스가 현재 세션의 트랜잭션 참조 수를 늘립니다. 그렇지 않으면 인스턴스가 새로운 트랜잭션을 시작하고 현재 세션의 참조 수를 1로 설정합니다. 활성 트랜잭션이 **BeginTransaction** 명령을 통해 명시적으로 지정된 경우 이후 모든 명령은 명시적으로 지정된 트랜잭션 내에서 실행됩니다.  
  
 현재 세션이 종료되고 트랜잭션의 참조 수가 0보다 크면 모든 활성 트랜잭션이 롤백됩니다.  
  
 현재 세션에 명시적으로 지정된 활성 트랜잭션이 없으면 현재 세션에서 실행된 모든 명령이 암시적으로 정의된 트랜잭션 내에서 실행됩니다. 명령이 성공하면 암시적 트랜잭션이 커밋되고 명령이 실패하면 롤백됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Cancel 요소 &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/cancel-element-xmla.md)   
 [CommitTransaction 요소 &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/committransaction-element-xmla.md)   
 [RollbackTransaction 요소 &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/rollbacktransaction-element-xmla.md)   
 [명령 &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  

