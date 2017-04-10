---
title: "URL 액세스를 사용하여 보고서 검색 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "보고서 검색"
  - "텍스트 검색 [Reporting Services]"
  - "URL 액세스 [Reporting Services], 보고서 검색"
ms.assetid: 6f3410c4-7944-448f-bae8-bab3e8152d46
caps.latest.revision: 34
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 34
---
# URL 액세스를 사용하여 보고서 검색
  URL 액세스를 사용하여 특정 텍스트 집합에 대한 보고서를 검색할 수 있습니다. 보고서를 검색하려면 URL의 *rc:FindString* 매개 변수 값을 검색할 텍스트에 해당하는 값으로 설정합니다. 아울러 *rc:StartFind* 및 *rc:EndFind* 매개 변수를 사용하여 보고서 내의 특정 페이지로 검색 범위를 좁힐 수 있습니다.  
  
## 예제  
 다음 URL 액세스 예제는 Product Catalog 예제 보고서에서 1~5페이지 중 처음 나타나는 "Mountain-400" 텍스트를 검색합니다.  
  
```  
http://server/Reportserver?/SampleReports/Product Catalog&rs:Command=Render&rc:StartFind=1&rc:EndFind=5&rc:FindString=Mountain-400  
```  
  
## 관련 항목:  
 [URL 액세스&#40;SSRS&#41;](../reporting-services/url-access-ssrs.md)   
 [URL 액세스 매개 변수 참조](../reporting-services/url-access-parameter-reference.md)  
  
  