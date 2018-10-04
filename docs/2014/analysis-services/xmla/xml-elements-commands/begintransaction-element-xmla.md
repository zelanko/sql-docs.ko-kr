---
title: BeginTransaction 요소 (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- BeginTransaction Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#BeginTransaction
- microsoft.xml.analysis.begintransaction
- http://schemas.microsoft.com/analysisservices/2003/engine#BeginTransaction
helpviewer_keywords:
- BeginTransaction command
ms.assetid: fca122fc-b57c-4ba6-849b-ca8c93cf64e9
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 5e8b1954836a7c5b079d629602d03ba4b45d8620
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48083473"
---
# <a name="begintransaction-element-xmla"></a>BeginTransaction 요소(XMLA)
  인스턴스로 현재 세션에서 트랜잭션을 시작 합니다 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Command>  
   <BeginTransaction />  
</Command>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|없음|  
|기본값|없음|  
|카디널리티|0-n: 두 번 이상 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[Command](../xml-elements-properties/command-element-xmla.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>Remarks  
 `BeginTransaction` 명령은 현재 세션에서 활성 트랜잭션을 시작합니다. 활성 트랜잭션이 이미 있는 경우에는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스가 현재 세션의 트랜잭션 참조 수를 늘립니다. 그렇지 않으면 인스턴스가 새로운 트랜잭션을 시작하고 현재 세션의 참조 수를 1로 설정합니다. 활성 트랜잭션이 `BeginTransaction` 명령을 통해 명시적으로 지정된 경우 이후 모든 명령은 명시적으로 지정된 트랜잭션 내에서 실행됩니다.  
  
 현재 세션이 종료되고 트랜잭션의 참조 수가 0보다 크면 모든 활성 트랜잭션이 롤백됩니다.  
  
 현재 세션에 명시적으로 지정된 활성 트랜잭션이 없으면 현재 세션에서 실행된 모든 명령이 암시적으로 정의된 트랜잭션 내에서 실행됩니다. 명령이 성공하면 암시적 트랜잭션이 커밋되고 명령이 실패하면 롤백됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [Cancel 요소 &#40;XMLA&#41;](cancel-element-xmla.md)   
 [CommitTransaction 요소 &#40;XMLA&#41;](committransaction-element-xmla.md)   
 [RollbackTransaction 요소 &#40;XMLA&#41;](rollbacktransaction-element-xmla.md)   
 [명령 &#40;XMLA&#41;](xml-elements-commands.md)  
  
  
