---
title: ATOM 디바이스 정보 설정 | Microsoft Docs
description: Atom 피드 이름 및 사용할 문자 인코딩 전송을 지원하는 Atom 렌더링 확장 프로그램에 대한 디바이스 정보 설정을 알아봅니다.
ms.date: 03/16/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: fe4a56a4-5552-423c-85c1-895e2e212fee
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 274815c98aa15aead103e33de761b8b496212242
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87242503"
---
# <a name="atom-device-information-settings"></a>ATOM 디바이스 정보 설정
  Atom 렌더링 확장 프로그램의 디바이스 정보 설정은 사용할 문자 인코딩 및 Atom 피드 이름 전송을 지원합니다.  
  
 다음 표에서는 데이터 서비스 문서로 렌더링하기 위한 디바이스 정보 설정을 보여 줍니다.  
  
|설정|값|  
|-------------|-----------|  
|**DataFeed**|지정되면 이 설정에 제공된 피드 이름에 해당하는 Atom 피드를 렌더링하고, 지정되지 않으면 보고서의 Atom 서비스 문서를 렌더링합니다. 데이터 피드의 고유한 자동 생성 식별자입니다. 이 값은 내부적으로 사용되며 변경하면 안 됩니다.|  
|**인코딩**|.NET Framework에서 지원하는 문자 인코딩의 IANA(Internet Assigned Numbers Authority) 이름입니다. 기본값은 **UTF-8**입니다. 다른 값의 예로 ASCII, UTF-7 및 UTF-16을 들 수 있습니다.|  
  
## <a name="see-also"></a>참고 항목  
 <xref:ReportExecution2005.ReportExecutionService.Render%2A>   
 [디바이스 정보 설정을 렌더링 확장 프로그램에 전달](../reporting-services/report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)   
 [RSReportServer.Config의 렌더링 확장 프로그램 매개 변수를 사용자 지정](../reporting-services/customize-rendering-extension-parameters-in-rsreportserver-config.md)   
 [기술 참조&#40;SSRS&#41;](../reporting-services/technical-reference-ssrs.md)  
  
  
