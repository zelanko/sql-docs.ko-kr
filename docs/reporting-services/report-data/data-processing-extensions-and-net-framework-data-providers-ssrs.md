---
title: 데이터 처리 확장 프로그램과 .NET Framework 데이터 공급자 | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: conceptual
helpviewer_keywords:
- reports [Reporting Services], data
- data processing extensions [Reporting Services]
- data providers [Reporting Services]
- data retrieval [Reporting Services]
- Reporting Services, data sources
- report data [Report Builder], accessing
ms.assetid: 42a5afb5-f4c8-4957-b1fd-77bf39afa5be
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 1be86b9522f0386fff2d1014c3d94c652411f029
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "77082574"
---
# <a name="data-processing-extensions-and-net-framework-data-providers-ssrs"></a>데이터 처리 확장 프로그램과 .NET Framework 데이터 공급자(SSRS)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 데이터 처리 확장 프로그램은 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]와 함께 설치되는 구성 요소로, 특정 유형의 데이터 원본에서 데이터를 검색하고 보고서 디자인 및 보고서 처리를 지원하기 위한 추가 기능을 제공하도록 디자인되었습니다. 먼저 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 데이터 공급자는 특정 유형의 데이터 원본에서 데이터를 검색하고 수정할 수 있는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] System.Data <xref:System.Data> 또는 타사 제공 구성 요소입니다.  
  
## <a name="understanding-a-data-processing-extension"></a>데이터 처리 확장 프로그램 이해  
 먼저 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 데이터 처리 확장 프로그램은 <xref:System.Data> 인터페이스의 하위 집합을 지원합니다. 데이터 처리 확장 프로그램에는 데이터 원본에 대한 읽기 전용 액세스 권한만 필요하므로 쓰기 및 업데이트용 인터페이스는 구현되지 않습니다. 각 데이터 처리 확장 프로그램은 보고서 처리를 지원하는 사용자 지정 기능을 제공할 수 있습니다. 예를 들어 데이터 처리 확장 프로그램은 다음과 같은 유형의 기능을 지원할 수 있습니다.  
  
-   연결 문자열과 별도로 자격 증명 관리  
  
-   다중값 매개 변수 지원  
  
-   데이터 원본에서 계산된 서버 집계 검색  
  
-   데이터 원본에서 데이터 속성 및 데이터 값 검색  
  
## <a name="understanding-a-data-provider"></a>데이터 공급자 이해  
 먼저 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 데이터 공급자(드라이버)는 데이터 원본의 데이터를 읽고, 쓰고, 업데이트하기 위한 표준 <xref:System.Data> 인터페이스 집합을 지원합니다. 데이터 공급자는 특정 유형의 데이터 원본에 사용 가능한 데이터 처리 확장 프로그램이 없는 경우 사용할 수 있습니다. 많은 타사 표준 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 데이터 공급자를 사용할 수 있습니다.  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 에는 확장 가능한 데이터 공급자 아키텍처가 있으므로 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 데이터 처리 확장 프로그램에서 제공하는 추가 기능을 포함하는 사용자 지정 데이터 처리 확장 프로그램을 빌드할 수 있습니다. 자세한 내용은 [Implementing a Data Processing Extension](../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md)을 참조하세요. 타사 데이터 처리 확장 프로그램의 경우 타사 데이터 처리 확장 프로그램과 함께 제공되는 설명서를 참조하십시오.  
  
> [!NOTE]  
>  먼저 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 데이터 공급자나 사용자 지정 데이터 처리 확장 프로그램을 설치하고 등록해야만 데이터 원본의 데이터에 액세스하는 데 사용할 수 있습니다. 데이터 처리 확장 프로그램은 보고서를 작성하기 위한 보고 클라이언트와 게시된 보고서를 보기 위한 보고서 서버에 모두 설치 및 등록해야 합니다. 모든 데이터 공급자가 서버 환경에서 작동하는 것은 아닙니다. 자세한 내용은 [표준 .NET Framework 데이터 공급자 등록&#40;SSRS&#41;](../../reporting-services/report-data/register-a-standard-net-framework-data-provider-ssrs.md) 및 [데이터 처리 확장 프로그램 배포](../../reporting-services/extensions/data-processing/deploying-a-data-processing-extension.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [데이터 처리 확장 프로그램 개요](../../reporting-services/extensions/data-processing/data-processing-extensions-overview.md)   
 [보고서 포함된 데이터 세트 및 공유 데이터 세트&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
  
  
