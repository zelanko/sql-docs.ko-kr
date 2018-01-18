---
title: "Database 요소 (DTA) 작업에 대 한 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: dta
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: XML
helpviewer_keywords: Database element
ms.assetid: 112fca2a-37e5-4162-b2e7-b56eb8ab0c6f
caps.latest.revision: "12"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 02bf075186f8bc9c8efc6fb05b9288f636494a7c
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/17/2018
---
# <a name="database-element-for-workload-dta"></a>Workload의 Database 요소(DTA)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]작업 추적 테이블이 있는 데이터베이스를 지정 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
<Workload>  
  <Database>  
   ...code removed here...  
  </Database>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|**데이터 형식 및 길이**|없음|  
|**기본값**|없음|  
|**발생 빈도**|다른 작업 유형이 지정되지 않은 경우 한 번만 지정해야 합니다. **Workload**부모에 대해 **EventString**, **File** 또는 **Database** 자식 요소를 지정해야 하지만 한 유형만 사용할 수 있습니다. 예를 들어 **Database** 요소로 작업을 지정할 경우 동일한 XML 입력 파일에서 **File** 요소로 작업을 지정할 수 없습니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|--------------|  
|**부모 요소**|[Workload 요소 &#40; DTA &#41;](../../tools/dta/workload-element-dta.md)|  
|**자식 요소**|[데이터베이스 &#40; DTA &#41;의 name 요소](../../tools/dta/name-element-for-database-dta.md)<br /><br /> [데이터베이스 &#40; DTA &#41;에 대 한 스키마 요소](../../tools/dta/schema-element-for-database-dta.md)|  
  
## <a name="remarks"></a>주의  
 데이터베이스 엔진 튜닝 관리자 XML 스키마에서 이 요소의 이름은 **DatabaseDetailsTypecomplexType** 입니다. 이 **Database** 요소와 **Configuration** 요소가 루트 부모인 요소를 혼동하지 마십시오. [Configuration의 Database 요소&#40;DTA&#41;](../../tools/dta/database-element-for-configuration-dta.md)를 참조하세요.  
  
## <a name="example"></a>예제  
 이 **Database** 요소의 사용 예는 [Workload 요소&#40;DTA&#41;](../../tools/dta/workload-element-dta.md)에서 코드 예제를 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [XML 입력 파일 참조&#40;데이터베이스 엔진 튜닝 관리자&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
