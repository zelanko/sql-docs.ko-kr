---
title: "Name 요소 (DTA) 스키마에 대 한 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- XML
helpviewer_keywords:
- Name element
ms.assetid: 014e4854-fed2-454b-8557-5f7c5bb6b17a
caps.latest.revision: 13
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 49e6040c8f3bbeb93a83bbd7b470940733a54de3
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="name-element-for-schema-dta"></a>Schema의 Name 요소(DTA)
  스키마의 이름을 포함합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
<Database>  
...code removed here  
    <Schema>  
        <Name>...</Name>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|**데이터 형식 및 길이**|**string**, 1에서 255자 사이|  
|**기본값**|없음|  
|**발생 빈도**|각 **Schema** 요소에 한 번만 지정해야 합니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|--------------|  
|**부모 요소**|[데이터베이스 &#40; DTA &#41;에 대 한 스키마 요소](../../tools/dta/schema-element-for-database-dta.md)|  
|**자식 요소**|없음|  
  
## <a name="example"></a>예제  
 이 요소의 사용 예는 [Server 요소&#40;DTA&#41;](../../tools/dta/server-element-dta.md)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [XML 입력 파일 참조&#40;데이터베이스 엔진 튜닝 관리자&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
