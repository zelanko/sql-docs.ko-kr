---
title: URL 액세스를 사용하여 보고서 검색 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- searching reports
- text searches [Reporting Services]
- URL access [Reporting Services], report searches
ms.assetid: 6f3410c4-7944-448f-bae8-bab3e8152d46
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 79c1a291781c5d58b83b05f77ce5ccb952765277
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/22/2019
ms.locfileid: "59970519"
---
# <a name="search-a-report-using-url-access"></a>URL 액세스를 사용하여 보고서 검색
  URL 액세스를 사용하여 특정 텍스트 집합에 대한 보고서를 검색할 수 있습니다. 보고서를 검색하려면 URL의 *rc:FindString* 매개 변수 값을 검색할 텍스트에 해당하는 값으로 설정합니다. 아울러 *rc:StartFind* 및 *rc:EndFind* 매개 변수를 사용하여 보고서 내의 특정 페이지로 검색 범위를 좁힐 수 있습니다.  
  
## <a name="example"></a>예제  
 다음 URL 액세스 예제는 Product Catalog 예제 보고서에서 1~5페이지 중 처음 나타나는 "Mountain-400" 텍스트를 검색합니다.  
  
```  
http://server/Reportserver?/SampleReports/Product Catalog&rs:Command=Render&rc:StartFind=1&rc:EndFind=5&rc:FindString=Mountain-400  
```  
  
## <a name="see-also"></a>관련 항목  
 [URL 액세스&#40;SSRS&#41;](url-access-ssrs.md)   
 [URL 액세스 매개 변수 참조](url-access-parameter-reference.md)  
  
  
