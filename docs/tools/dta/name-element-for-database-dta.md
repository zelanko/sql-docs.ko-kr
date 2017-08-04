---
title: "Name 요소 (DTA) 데이터베이스에 대 한 | Microsoft Docs"
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
ms.assetid: e871c4fa-3b57-46cf-b4f8-e3be86f92dc4
caps.latest.revision: 15
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: f05671f43981849c81d6fb77958bd7a19f10e603
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="name-element-for-database-dta"></a>Database의 Name 요소(DTA)
  튜닝할 데이터베이스의 이름을 지정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
<Server>  
    <Database>  
        <Name>...</Name>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|**데이터 형식 및 길이**|**string**, 길이 제한 없음|  
|**기본값**|없음|  
|**발생 빈도**|각 **Database** 요소 당 한 번씩만 필요합니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|--------------|  
|**부모 요소**|[서버 &#40; DTA &#41;의 database 요소](../../tools/dta/database-element-for-server-dta.md)|  
|**자식 요소**|없음|  
  
## <a name="example"></a>예제  
 이 요소의 사용 예는 [Server 요소&#40;DTA&#41;](../../tools/dta/server-element-dta.md)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [XML 입력 파일 참조&#40;데이터베이스 엔진 튜닝 관리자&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
