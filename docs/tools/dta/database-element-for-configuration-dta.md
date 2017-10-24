---
title: "Database 요소 (DTA) 구성에 대 한 | Microsoft Docs"
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
- Database element
ms.assetid: e91ba243-6cc9-457a-8f5a-134f3c71ae69
caps.latest.revision: 12
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: ad4af22826a868e1860d5170fb156ba74d1b903c
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="database-element-for-configuration-dta"></a>Configuration의 Database 요소(DTA)
  데이터베이스 엔진 튜닝 관리자가 가상 구성( **Configuration** 요소에 의해 지정됨)을 평가하게 하려는 데이터베이스를 지정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
<Server>  
...code removed here...  
    <Database>...</Database>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|**데이터 형식 및 길이**|없음|  
|**기본값**|없음|  
|**발생 빈도**|**Server** 요소마다 한 번 이상 지정해야 합니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|--------------|  
|**부모 요소**|[서버 요소 구성 &#40; DTA &#41;](../../tools/dta/server-element-for-configuration-dta.md)|  
|**자식 요소**|[데이터베이스 &#40; DTA &#41;의 name 요소](../../tools/dta/name-element-for-database-dta.md)<br /><br /> [데이터베이스 &#40; DTA &#41;에 대 한 스키마 요소](../../tools/dta/schema-element-for-database-dta.md)<br /><br /> [Recommendation 요소 &#40; DTA &#41;](../../tools/dta/recommendation-element-dta.md)|  
  
## <a name="remarks"></a>주의  
 데이터베이스 엔진 튜닝 관리자 XML 스키마에서 이 요소의 이름은 **DatabaseTypecomplexType** 입니다. 이 **Database** 요소와 XML 입력 파일의 맨 위에서 발생하는 **Server** 요소가 루트 부모인 요소를 혼동하지 마십시오. 자세한 내용은 [Server의 Database 요소&#40;DTA&#41;](../../tools/dta/database-element-for-server-dta.md)를 참조하세요.  
  
## <a name="example"></a>예제  
 이 **Database** 요소의 사용 예를 보려면 [사용자 정의 구성이 포함된 XML 입력 파일 샘플&#40;DTA&#41;](../../tools/dta/xml-input-file-sample-with-user-specified-configuration-dta.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [XML 입력 파일 참조&#40;데이터베이스 엔진 튜닝 관리자&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  

