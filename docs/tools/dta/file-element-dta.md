---
title: "파일 요소 (DTA) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
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
helpviewer_keywords: File element
ms.assetid: 73dce835-9a80-4aef-8e0f-9dcf07dd5b80
caps.latest.revision: "15"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 65d4f2334b180c7307d95bea0cb13a2c6ce33a5a
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/17/2018
---
# <a name="file-element-dta"></a>File 요소(DTA)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]작업 파일을 지정합니다. 작업은 튜닝하려는 데이터베이스에 대해 실행되는 일련의 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문입니다. 작업 파일은 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트(.sql) 또는 추적 파일(.trc)이 될 수 있습니다. 자세한 내용은[Start and Use the Database Engine Tuning Advisor](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md)을 참조하세요.  
  
## <a name="syntax"></a>구문  
  
```  
  
<DTAInput>  
  <Server>...</Server>  
  <Workload>  
    <File>...</File>  
  </Workload>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|**데이터 형식 및 길이**|**string** 데이터 형식을 사용하여 작업 파일의 디렉터리 경로를 지정할 수 있습니다. 예를 들어<br /><br /> `<File>C:\Tuning\tun.sql</File>`<br /><br /> 서버에서 지정하는 길이 제한이 적용됩니다.|  
|**기본값**|없음|  
|**발생 빈도**|다른 작업 유형이 지정되지 않은 경우 한 번만 지정해야 합니다. **Workload**부모에 대해 **EventString**, **File** 또는 **Database** 자식 요소를 지정해야 하지만 한 유형만 사용할 수 있습니다. 예를 들어 **File** 요소로 작업을 지정할 경우 동일한 XML 입력 파일에서 **Database** 요소로 작업을 지정할 수 없습니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|--------------|  
|**부모 요소**|[Workload 요소 &#40; DTA &#41;](../../tools/dta/workload-element-dta.md)|  
|**자식 요소**|없음|  
  
## <a name="example"></a>예제  
 이 요소의 사용 예제를 보려면 [단순 XML 입력 파일 예제&#40;DTA&#41;](../../tools/dta/simple-xml-input-file-sample-dta.md)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [XML 입력 파일 참조&#40;데이터베이스 엔진 튜닝 관리자&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
