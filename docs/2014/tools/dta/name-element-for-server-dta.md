---
title: Server의 Name 요소 (DTA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Name element
ms.assetid: 4c94754d-6d62-4357-8ce7-f107ebf90c71
author: stevestein
ms.author: sstein
ms.openlocfilehash: 5f2537dcae126252f75cb90aa41a85ea55674d4e
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85011490"
---
# <a name="name-element-for-server-dta"></a>Server의 Name 요소(DTA)
  튜닝할 데이터베이스가 상주하는 서버의 이름을 포함합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
...code removed here...  
<Server>  
    <Name>...</Name>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특성|Description|  
|--------------------|-----------------|  
|**데이터 형식 및 길이**|`string`, 1에서 255자 사이|  
|**기본값**|없음|  
|**발생 빈도**|**Server** 요소마다 한 번만 지정해야 함|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|--------------|  
|**부모 요소**|[Server 요소&#40;DTA&#41;](server-element-dta.md)|  
|**자식 요소**|없음|  
  
## <a name="example"></a>예제  
 이 **Name** 요소의 사용 예는 [Server 요소&#40;DTA&#41;](server-element-dta.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [XML 입력 파일 참조&#40;데이터베이스 엔진 튜닝 관리자&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
