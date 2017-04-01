---
title: "Banner 요소(ssbdiagnose) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "banner 요소"
  - "XML 출력 파일 형식 [ssbdiagnose], banner 요소"
  - "ssbdiagnose"
ms.assetid: cc6cd49a-acf0-4cfb-8c6a-554692b89de2
caps.latest.revision: 15
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 15
---
# Banner 요소(ssbdiagnose)
  **ssbdiagnose** 출력 XML 파일을 생성한 유틸리티를 식별합니다.  
  
## 구문  
  
```  
  
<Banner  
    title="..."   
    product="..."   
    version="..." />  
```  
  
## 요소 특성  
  
|Attribute|설명|  
|---------------|-----------------|  
|**title**|**ssbdiagnose** XML 출력 파일을 생성한 유틸리티를 식별합니다.|  
|**product**|**ssbdiagnose** XML 출력 파일을 생성한 제품을 식별합니다.|  
|**version**|XML 출력 파일을 생성한 유틸리티의 버전을 식별합니다.|  
  
## 요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|**데이터 형식 및 길이**|없음|  
|**기본값**|없음|  
|**발생 빈도**|**ssbdiagnose** 출력 XML 파일당 한 번|  
  
## 요소 관계  
  
|관계|요소|  
|------------------|--------------|  
|**부모 요소**|[DiagnosticInformation 요소&#40;ssbdiagnose&#41;](../../tools/ssbdiagnose/diagnosticinformation-element-ssbdiagnose.md)|  
|**자식 요소**|없음|  
  
## 예제  
 다음은 Banner 요소의 예입니다.  
  
```  
<Banner title="Service Broker Diagnostics Utility" product="Microsoft SQL Server" version="10.0.1073.0" />  
```  
  
## 참고 항목  
 [ssbdiagnose 유틸리티&#40;Service Broker&#41;](../../tools/ssbdiagnose/ssbdiagnose-utility-service-broker.md)  
  
  