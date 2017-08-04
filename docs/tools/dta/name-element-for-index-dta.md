---
title: "Name 요소 (DTA) 인덱스에 대 한 | Microsoft Docs"
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
ms.assetid: 2300e9cf-f0a8-49e6-b1f5-45ffe03ccb5f
caps.latest.revision: 13
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: c2f20e695223c8ced900d82c79b646e3a4090101
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="name-element-for-index-dta"></a>Index의 Name 요소(DTA)
  사용자 지정 구성에서 인덱스의 이름을 지정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
<Create>  
    <Index>  
        <Name>...</Name>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|**데이터 형식 및 길이**|**string**, 길이 제한 없음|  
|**기본값**|없음|  
|**발생 빈도**|각 **Index** 요소에 한 번만 지정해야 합니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|--------------|  
|**부모 요소**|[Index 요소 &#40; DTA &#41;](../../tools/dta/index-element-dta.md)|  
|**자식 요소**|없음|  
  
## <a name="example"></a>예제  
 이 요소의 사용 예제를 보려면 [사용자 지정 구성이 포함된 XML 입력 파일 예제&#40;DTA&#41;](../../tools/dta/xml-input-file-sample-with-user-specified-configuration-dta.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [XML 입력 파일 참조&#40;데이터베이스 엔진 튜닝 관리자&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
