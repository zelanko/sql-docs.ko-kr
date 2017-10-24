---
title: "Database 요소 (DTA) 서버에 대 한 | Microsoft Docs"
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
ms.assetid: 5cd9a87a-af4b-45f3-8c18-f7fd7e7d3064
caps.latest.revision: 16
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 3b24e80cb9f0686e3f6eac488488d001e1076ae3
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="database-element-for-server-dta"></a>Server의 Database 요소(DTA)
  특정 서버에서 튜닝할 데이터베이스를 지정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
<Server>  
...code removed here...  
    <Database>...</Database>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|없음|  
|기본값|없음|  
|발생 빈도|**Server** 요소마다 한 번 이상 지정해야 합니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|--------------|  
|부모 요소|[Server 요소&#40;DTA&#41;](../../tools/dta/server-element-dta.md)|  
|자식 요소|[Database의 Name 요소&#40;DTA&#41;](../../tools/dta/name-element-for-database-dta.md)<br /><br /> [Database의 Schema 요소&#40;DTA&#41;](../../tools/dta/schema-element-for-database-dta.md)|  
  
## <a name="remarks"></a>주의  
 데이터베이스 엔진 튜닝 관리자 XML 스키마에서 이 요소의 이름은 **DatabaseDetailsTypecomplexType** 입니다. 이 **Database** 요소와 **Configuration** 요소가 루트 부모인 요소를 혼동하지 마십시오. 자세한 내용은 [Configuration의 Database 요소&#40;DTA&#41;](../../tools/dta/database-element-for-configuration-dta.md)를 참조하세요.  
  
## <a name="example"></a>예제  
 사용 예는 **데이터베이스** 요소 참조 [서버 요소 &#40; DTA &#41;](../../tools/dta/server-element-dta.md)합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [XML 입력 파일 참조&#40;데이터베이스 엔진 튜닝 관리자&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  

