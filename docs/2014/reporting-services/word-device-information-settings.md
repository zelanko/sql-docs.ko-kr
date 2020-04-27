---
title: Word 디바이스 정보 설정 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Word [Reporting Services]
- device information settings [Reporting Services], Word
ms.assetid: 28146498-fae7-4b13-b47f-6ec05aa8e057
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: ddd145c5073003a8dc189e3ed9b1bbb25dc11d09
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66096924"
---
# <a name="word-device-information-settings"></a>Word 디바이스 정보 설정
  다음 표는 [!INCLUDE[ofprword](../includes/ofprword-md.md)] 형식으로 렌더링하기 위한 디바이스 정보 설정을 나열합니다.  
  
|설정|값|  
|-------------|-----------|  
|`AutoFit`|`False`. 자동 맞춤이 임의의 Word 테이블에서 `false`로 설정됩니다.<br /><br /> `True`. 자동 맞춤이 모든 Word 테이블에서 `true`로 설정됩니다.<br /><br /> `Never`. 자동 맞춤 값이 Word 테이블에서 설정되지 않으며 Word 기본값으로 되돌아갑니다.<br /><br /> `Default`. 자동 맞춤이 논리 페이지당 실제 그리기 영역(여백을 제외한 실제 페이지 너비)보다 좁은 테이블에서 설정됩니다.|  
|`ExpandToggles`|표시하거나 숨길 수 있는 모든 항목이 전체 확장 상태로 렌더링되어야 하는지 여부를 나타냅니다. 기본값은 `false`입니다.|  
|`FixedPageWidth`|DOC 파일에 적용되는 페이지 너비가 보고서 본문의 가장 큰 페이지 너비에 맞게 늘어나는지 여부를 나타냅니다. 기본값은 `false`입니다.|  
|**OmitHyperlinks**|하이퍼링크 동작이 설정된 모든 항목에 대한 하이퍼링크 동작을 생략할지 여부를 나타냅니다. 기본값은 `false`입니다.|  
|`OmitDrillthroughs`|드릴스루 동작이 설정된 모든 항목에 대한 드릴스루 동작을 생략할지 여부를 나타냅니다. 기본값은 `false`입니다.|  
  
## <a name="see-also"></a>참고 항목  
 [장치 정보 설정을 렌더링 확장 프로그램에 전달](report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)   
 [Rsreportserver.config의 렌더링 확장 프로그램 매개 변수 사용자 지정](customize-rendering-extension-parameters-in-rsreportserver-config.md)   
 [기술 참조&#40;SSRS&#41;](../../2014/reporting-services/technical-reference-ssrs.md)  
  
  
