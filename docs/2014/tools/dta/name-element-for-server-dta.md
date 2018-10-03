---
title: Name 요소 (DTA) 서버용 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Name element
ms.assetid: 4c94754d-6d62-4357-8ce7-f107ebf90c71
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4c3c41cf90d15ee8c5342dd0274cd8fedbd30dee
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48171533"
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
  
|특징|Description|  
|--------------------|-----------------|  
|**데이터 형식 및 길이**|`string`, 1에서 255자 사이|  
|**기본값**|없음|  
|**발생 빈도**|**Server** 요소마다 한 번만 지정해야 함|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|--------------|  
|**부모 요소**|[Server 요소 &#40;DTA&#41;](server-element-dta.md)|  
|**자식 요소**|없음|  
  
## <a name="example"></a>예제  
 이 **Name** 요소의 사용 예는 [서버 요소&#40;DTA&#41;](server-element-dta.md)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [XML 입력 파일 참조&#40;데이터베이스 엔진 튜닝 관리자&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
