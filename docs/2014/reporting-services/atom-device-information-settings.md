---
title: ATOM 디바이스 정보 설정 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: fe4a56a4-5552-423c-85c1-895e2e212fee
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: bdbac1500063accf868d4b538b82ba9f3b5aebb0
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66109976"
---
# <a name="atom-device-information-settings"></a>ATOM 디바이스 정보 설정
  Atom 렌더링 확장 프로그램의 디바이스 정보 설정은 사용할 문자 인코딩 및 Atom 피드 이름 전송을 지원합니다.  
  
 다음 표에서는 데이터 서비스 문서로 렌더링하기 위한 디바이스 정보 설정을 보여 줍니다.  
  
|설정|값|  
|-------------|-----------|  
|`DataFeed`|지정되면 이 설정에 제공된 피드 이름에 해당하는 Atom 피드를 렌더링하고, 지정되지 않으면 보고서의 Atom 서비스 문서를 렌더링합니다. 데이터 피드의 고유한 자동 생성 식별자입니다. 이 값은 내부적으로 사용되며 변경하면 안 됩니다.|  
|**인코딩**|.NET Framework에서 지원하는 문자 인코딩의 IANA(Internet Assigned Numbers Authority) 이름입니다. 기본값은 `UTF-8`입니다. 다른 값의 예로 ASCII, UTF-7 및 UTF-16을 들 수 있습니다.|  
  
## <a name="see-also"></a>관련 항목  
 <xref:ReportExecution2005.ReportExecutionService.Render%2A>   
 [디바이스 정보 설정을 렌더링 확장 프로그램에 전달](report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)   
 [RSReportServer.Config의 렌더링 확장 프로그램 매개 변수를 사용자 지정](customize-rendering-extension-parameters-in-rsreportserver-config.md)   
 [기술 참조&#40;SSRS&#41;](../../2014/reporting-services/technical-reference-ssrs.md)  
  
  
