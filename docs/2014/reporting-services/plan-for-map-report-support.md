---
title: 지도 보고서 지원 계획 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 5ddc97a7-7ee5-475d-bc49-3b814dce7e19
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 2236103c76c6af8f81b0d4004962c23adedc2eaa
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/22/2019
ms.locfileid: "59946899"
---
# <a name="plan-for-map-report-support"></a>지도 보고서 지원 계획
  [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)] 공간 데이터 원본을 사용 하는 지도 보고서를 지원 합니다. 공간 데이터는 SQL Server 데이터베이스, ESRI 셰이프 파일 또는 Reporting Services나 보고서 작성기에 설치된 지도 갤러리에서 가져올 수 있습니다. 지도에 Bing 지도 타일 배경을 표시할 수도 있습니다. 보고서 작성자는 공간 데이터나 Bing 지도 타일을 런타임에 검색되는 동적 스타일 또는 보고서 정의에 포함된 정적 스타일로 지정하는 보고서를 만들 수 있습니다.  
  
## <a name="support-for-bing-maps"></a>Bing Maps 지원  
 지도는 Bing 지도 타일을 표시하는 배경 계층을 포함할 수 있습니다. 지도 타일 계층을 포함하는 게시된 보고서를 보려면 보고서 서버가 Bing Maps 웹 서비스에서 타일을 검색하도록 구성되어 있어야 합니다. 자세한 내용은 [RSReportServer Configuration File](report-server/rsreportserver-config-configuration-file.md)을 참조하세요.  
  
 보고서 작성자는 각 보고서에서 SSL(Secure Sockets Layer) 연결을 사용하여 타일 서버에서 타일을 검색할지 여부를 지정할 수 있습니다. 이렇게 하려면, 타일 계층에 대 한 속성 창에서 UseSecureConnection 부울 속성을 설정 해야 이러한를 `true`입니다.  
  
> [!NOTE]  
>  보고서에서 Bing 지도 타일을 사용하는 방법은 [추가 사용 조건(Additional Terms of Use)](https://go.microsoft.com/fwlink/?LinkId=151371) 및 [개인 정보 취급 방침](https://go.microsoft.com/fwlink/?LinkId=151372)을 참조하십시오.  
  
## <a name="report-design-recommendations"></a>보고서 디자인 권장 구성  
 지도 보고서를 효과적으로 디자인하려면 보고서 작성자가 정적 공간 데이터와 동적 공간 데이터의 장단점을 평가하고 보고서 사용자를 위해 균형점을 찾아야 합니다. 포함된 지도 요소를 사용하면 보고서 정의의 크기가 매우 증가할 수 있지만 지도 보고서를 보는 데 필요한 시간을 줄일 수 있습니다. 동적 지도 요소를 사용하면 보고서 정의의 크기는 줄일 수 있지만 지도를 처리하고 보는 데 필요한 시간이 늘어날 수 있습니다. 보고서 작성자는 이렇게 서로 반대되는 문제점을 고려하여 적절한 균형점을 찾아야 합니다.  
  
 보고서 서버 관리자로서 보고서 정의 크기가 문제가 되면 보고서 정의의 공간 데이터 양을 줄이도록 보고서 디자이너에게 요청할 수 있습니다.  
  
 다음과 같은 경우 지도 요소가 보고서 정의에 포함됩니다.  
  
-   보고서를 만들 때 공간 데이터 원본이 로컬 파일 시스템에 있습니다. 여기에는 로컬에 설치된 ESRI 셰이프 파일 또는 지도 갤러리의 공간 데이터가 포함됩니다. 기본적으로 지도 마법사와 지도 계층 마법사는 로컬 파일 시스템에 있는 데이터 원본의 공간 데이터를 포함합니다.  
  
-   보고서 작성자가 공간 데이터를 수동으로 보고서에 포함하는 옵션을 선택합니다.  
  
 지도를 포함하는 보고서 정의의 크기를 줄이기 위해 보고서 작성자는 다음과 같은 옵션을 하나 이상 사용할 수 있습니다.  
  
-   [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]의 보고서 디자이너에서 공간 데이터 원본, 즉 ESRI 셰이프 파일을 보고서 서버 프로젝트에 추가합니다. 프로젝트를 배포하면 보고서와 함께 ESRI 셰이프 파일이 보고서 서버에 게시됩니다. 보고서 작성자가 지도 마법사를 실행하면 보고서 서버 프로젝트에서 공간 데이터 원본을 지정할 수 있으며 기본적으로 지도 요소는 보고서 정의에 포함되지 않습니다.  
  
-   보고서 작성기를 실행한 후 보고서 서버에서 셰이프 파일을 선택하여 공간 데이터 원본, 즉 ESRI 셰이프 파일을 추가합니다. 보고서 작성자가 지도 마법사를 실행하면 보고서 서버에서 공간 데이터 원본을 찾아 선택할 수 있으며 기본적으로 지도 요소는 보고서 정의에 포함되지 않습니다.  
  
-   지도 데이터가 포함되어 있어야 할 경우에는 보고서에 필요한 지도 데이터만 포함되도록 뷰포트 중심 및 확대/축소 수준을 조정합니다.  
  
 자세한 내용은 [Maps &#40;보고서 작성기 및 SSRS&#41;](report-design/maps-report-builder-and-ssrs.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [보고서 문제 해결: 맵 보고서&#40;보고서 작성기 및 SSRS&#41;](report-design/troubleshoot-reports-map-reports-report-builder-and-ssrs.md)  
  
  
