---
title: 공유 데이터 원본 만들기, 수정 및 삭제(SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- modifying data source properties
- shared data sources [Reporting Services]
- removing shared data sources
- roles [Reporting Services], shared data sources
- data sources [Reporting Services], shared
- data sources [Reporting Services], modifying properties
- deleting shared data sources
ms.assetid: 1e58c1c2-5ecf-4ce6-9d04-0a8acfba17be
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 26bc12ce8c685c4aeb119f43ab594d920a6cef9f
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/22/2019
ms.locfileid: "59934749"
---
# <a name="create-modify-and-delete-shared-data-sources-ssrs"></a>공유 데이터 원본 만들기, 수정 및 삭제(SSRS)
  공유 데이터 원본은 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보고서 서버에서 실행되는 여러 보고서, 모델 및 데이터 기반 구독에서 참조할 수 있는 데이터 원본 연결 속성의 집합입니다. 공유 데이터 원본을 사용하면 시간이 지나면서 자주 변경되는 데이터 원본 속성을 쉽게 관리할 수 있습니다. 사용자 계정 또는 암호가 변경되거나 데이터베이스를 다른 서버로 이동하는 경우 한 위치에서 연결 정보를 업데이트할 수 있습니다.  
  
 공유 데이터 원본은 보고서 및 데이터 기반 구독에서는 선택 사항이지만 보고서 모델에서는 필수 사항입니다. 임시 보고를 위해 보고서 모델을 사용하려는 경우 공유 데이터 원본 항목을 만들고 유지 관리하여 모델에 연결 정보를 제공해야 합니다.  
  
 공유 데이터 원본은 다음과 같은 부분으로 구성됩니다.  
  
|부분|Description|  
|----------|-----------------|  
|이름|보고서 서버 폴더 계층 내에서 항목을 식별하는 이름입니다.|  
|Description|폴더 내용을 볼 때 보고서 관리자에 항목과 함께 표시되는 설명입니다.|  
|연결 형식|데이터 원본과 함께 사용되는 데이터 처리 확장 프로그램입니다. 보고서 서버에 배포된 데이터 처리 확장 프로그램만 사용할 수 있습니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에 포함된 데이터 처리 확장 프로그램에 대한 자세한 내용은 [Reporting Services&#40;SSRS&#41;에서 지원하는 데이터 원본](../create-deploy-and-manage-mobile-and-paginated-reports.md)을 참조하세요.|  
|연결 문자열|데이터베이스에 대한 연결 문자열입니다. 자세한 정보 및 자주 사용 되는 데이터 원본에 연결 문자열의 예를 보려면 [데이터 연결, 데이터 원본 및 Reporting Services의 연결 문자열](../data-connections-data-sources-and-connection-strings-in-reporting-services.md)합니다.|  
|자격 증명 유형|연결에 대한 자격 증명을 가져오는 방법 및 연결된 이후 자격 증명이 사용되는지 여부를 지정합니다. 자세한 내용은 [보고서 데이터 원본에 대한 자격 증명 및 연결 정보 지정](../../integration-services/connection-manager/data-sources.md)을 참조하세요.|  
  
 공유 데이터 원본에는 데이터를 검색하는 데 사용되는 쿼리 정보가 포함되지 않습니다. 쿼리는 항상 보고서 정의 안에 보관됩니다.  
  
## <a name="creating-and-modifying-a-shared-data-source"></a>공유 데이터 원본 만들기 및 수정  
 공유 데이터 원본을 만들거나 속성을 수정하려면 보고서 서버에서 **데이터 원본 관리** 권한이 있어야 합니다. 보고서 서버가 기본 모드로 실행되는 경우에는 보고서 관리자를 사용하여 공유 데이터 원본을 만들고 구성할 수 있으며 보고서 서버가 SharePoint 통합 모드로 실행되는 경우에는 SharePoint 사이트의 애플리케이션 페이지를 사용할 수 있습니다. 보고서 디자이너에서는 보고서 서버의 모드에 관계없이 공유 데이터 원본을 만든 다음 대상 서버에 게시할 수 있습니다.  
  
 공유 데이터 원본을 만드는 방법에 대한 자세한 내용은 다음을 참조하십시오.  
  
-   [포함된 데이터 원본 또는 공유 데이터 원본 만들기&#40;SSRS&#41;](../create-an-embedded-or-shared-data-source-ssrs.md)  
  
-   [공유 데이터 원본 만들기 및 관리&#40;SharePoint 통합 모드의 Reporting Services&#41;](../create-manage-shared-data-sources-reporting-services-sharepoint-integrated-mode.md)  
  
 보고서 서버에서 공유 데이터 원본을 만든 후 역할 할당을 만들어 공유 데이터 원본에 대한 액세스를 제어하거나, 다른 위치로 이동하거나, 이름을 바꾸거나, 외부 데이터 원본에서 유지 관리 작업이 수행되는 동안 보고서가 처리되지 않도록 오프라인 상태로 만들 수 있습니다. 공유 데이터 원본 항목의 이름을 변경하거나 보고서 서버 폴더 계층의 다른 위치로 이동하면 공유 데이터 원본을 참조하는 모든 보고서나 구독의 경로 정보도 함께 업데이트됩니다. 공유 데이터 원본을 오프라인 상태로 만들면 데이터 원본을 다시 활성화할 때까지 모든 보고서, 모델 및 구독이 실행되지 않습니다.  
  
 보고서 서버 폴더 계층 구조에서 공유 데이터 원본에 대한 액세스를 제어하는 방법에 대한 자세한 내용은 [공유 데이터 원본 항목 보안 설정](../security/secure-shared-data-source-items.md)을 참조하세요.  
  
## <a name="deleting-a-shared-data-source"></a>공유 데이터 원본 삭제  
 보고서 서버에서 다른 항목을 삭제하는 것과 동일한 방법으로 공유 데이터 원본을 삭제할 수 있습니다. 보고서 관리자에서 자세히 보기로 폴더를 열고, 항목을 선택를 클릭 **삭제**합니다. SharePoint 사이트에서 응용 프로그램 페이지를 열어서 SharePoint 라이브러리, 항목을 선택 고 클릭 **삭제**합니다.  
  
 공유 데이터 원본을 삭제하면 해당 원본을 사용하는 모든 보고서, 모델 또는 데이터 기반 구독이 비활성화됩니다. 데이터 원본 연결 정보가 없으므로 이러한 항목은 더 이상 실행되지 않습니다. 항목을 활성화하려면 각 항목을 열어 다음 작업을 수행해야 합니다.  
  
-   공유 데이터 원본을 참조하는 보고서 및 데이터 기반 구독에 대해서는 보고서 속성 또는 구독에서 데이터 원본 연결 정보를 지정하거나 사용할 값이 들어 있는 새 공유 데이터 원본을 선택할 수 있습니다.  
  
-   모델 및 해당 모델을 사용하는 보고서 작성기 보고서에 대해서는 새 공유 데이터 원본을 지정해야 합니다. 모델은 공유 데이터 원본을 통해서만 데이터 원본 연결 정보를 가져옵니다.  
  
 데이터 원본을 사용하는 보고서 및 모델 목록을 보려면 해당 공유 데이터 원본에 대한 종속 항목 페이지를 엽니다. 보고서 관리자 또는 SharePoint 애플리케이션 페이지에서 데이터 원본을 열면 이 페이지에 액세스할 수 있습니다. 종속 항목 페이지에는 데이터 기반 구독이 표시되지 않는다는 점에 주의하십시오. 구독에서 공유 데이터 원본을 사용하는 경우 해당 구독은 종속 항목 목록에 표시되지 않습니다.  
  
 공유 데이터 원본 삭제 작업은 실행 취소할 수 없습니다. 하지만 공유 데이터 원본을 실수로 삭제한 경우에는 삭제된 것과 동일한 속성 값을 사용하여 새 공유 데이터 원본을 만들 수 있습니다. 각 보고서, 모델 및 데이터 기반 구독을 열어 공유 데이터 원본을 이 원본을 사용하는 항목에 다시 바인딩해야 하지만 데이터 원본 속성이 이전과 동일하기만 하면 보고서, 모델 및 구독은 이전과 동일하게 작동하게 됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [공유 데이터 원본 만들기 및 관리&#40;SharePoint 통합 모드의 Reporting Services&#41;](../create-manage-shared-data-sources-reporting-services-sharepoint-integrated-mode.md)   
 [데이터 연결, 데이터 원본 및 Reporting Services의 연결 문자열](../data-connections-data-sources-and-connection-strings-in-reporting-services.md)   
 [보고서 데이터 원본 관리](manage-report-data-sources.md)   
 [보고서 관리자&#40;SSRS 기본 모드&#41;](../report-manager-ssrs-native-mode.md)   
 [포함된 데이터 연결 및 공유 데이터 연결 또는 데이터 원본&#40;보고서 작성기 및 SSRS&#41;](../embedded-and-shared-data-connections-or-data-sources-report-builder-and-ssrs.md)   
 [데이터 원본 속성 페이지&#40;보고서 관리자&#41;](../data-sources-properties-page-report-manager.md)   
 [공유 데이터 원본 만들기, 삭제 또는 수정&#40;보고서 관리자&#41;](../create-delete-or-modify-a-shared-data-source-report-manager.md)   
 [보고서의 데이터 원본 속성 구성&#40;보고서 관리자&#41;](configure-data-source-properties-for-a-report-report-manager.md)  
  
  
