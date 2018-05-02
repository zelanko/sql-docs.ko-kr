---
title: Schema 요소 (DTA) 데이터베이스에 대 한 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: dta
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- XML
helpviewer_keywords:
- Schema element
ms.assetid: d932e59c-953f-4ab4-934d-b6baf344835c
caps.latest.revision: 14
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c2b4da3d22c91ad05ba53736eb17a2210b0c0b5d
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/17/2018
---
# <a name="schema-element-for-database-dta"></a>Database의 Schema 요소(DTA)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 튜닝할 데이터베이스의 스키마를 지정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
<Database>  
...code removed here...  
    <Schema>...</Schema>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|**데이터 형식 및 길이**|없음|  
|**기본값**|없음|  
|**발생 빈도**|**Server** 요소 아래 지정된 **Database** 요소에 한 번만 지정해야 합니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|--------------|  
|**부모 요소**|[Server의 Database 요소&#40;DTA&#41;](../../tools/dta/database-element-for-server-dta.md)|  
|**자식 요소**|[Schema의 Name 요소&#40;DTA&#41;](../../tools/dta/name-element-for-schema-dta.md)<br /><br /> [Schema의 Table 요소&#40;DTA&#41;](../../tools/dta/table-element-for-schema-dta.md)|  
  
## <a name="example"></a>예제  
 이 요소의 사용 예는 [Server 요소&#40;DTA&#41;](../../tools/dta/server-element-dta.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [XML 입력 파일 참조&#40;데이터베이스 엔진 튜닝 관리자&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
