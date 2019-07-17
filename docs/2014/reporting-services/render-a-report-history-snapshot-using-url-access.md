---
title: URL 액세스를 사용하여 보고서 기록 스냅샷 렌더링 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- URL access [Reporting Services], report history
- history snapshots [Reporting Services]
- historical data [Reporting Services]
- snapshots [Reporting Services], URL access
- snapshots [Reporting Services], rendering report history
ms.assetid: 3f87f82d-0e61-4492-9c4b-f5238c39e8cd
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 67854a39ab7e38289627d03ac00cc4b2a6dca6f2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66107976"
---
# <a name="render-a-report-history-snapshot-using-url-access"></a>URL 액세스를 사용하여 보고서 기록 스냅샷 렌더링
  *rs:Snapshot* 매개 변수를 제공하고 이 값을 유효한 스냅숏 ID로 설정하여 보고서 기록 스냅숏을 기반으로 한 보고서를 렌더링할 수 있습니다. 매개 변수 값은 ISO(국제 표준화 기구) 8601 표준을 기반으로 하여 YYYY-MM-DDTHH:MM:SS 형식으로 사용합니다.  
  
 이 매개 변수를 생략할 경우 보고서는 보고서 서버의 보고서 실행 및 캐시 관리 옵션 설정에 따라 렌더링됩니다. 보고서 실행에 대한 자세한 내용은 [보고서 처리 속성 설정](report-server/set-report-processing-properties.md)을 참조하세요.  
  
## <a name="example"></a>예제  
 다음 예는 보고서 기록 스냅샷을 검색하는 URL을 보여 줍니다.  
  
```  
http://myrshost/reportserver?/SampleReports/Company Sales&rs:Snapshot=2003-04-07T13:40:02  
```  
  
## <a name="see-also"></a>관련 항목  
 [URL 액세스&#40;SSRS&#41;](url-access-ssrs.md)   
 [URL 액세스 매개 변수 참조](url-access-parameter-reference.md)  
  
  
