---
description: 보안 개체 항목
title: 보안 개체 항목 | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- securable items [Reporting Services]
- roles [Reporting Services], securable items
- security [Reporting Services], securable items listed
- role-based security [Reporting Services], securable items
ms.assetid: 27f58d4c-5c7b-4947-af5b-0f1fa60faf5f
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 9fd4b92dcacf94e2a0196f210050954a84c1ac3d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88498016"
---
# <a name="securable-items"></a>보안 개체 항목
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 에서는 역할 기반 보안을 사용하여 보고서 서버에 저장되어 있는 항목에 대한 액세스를 제어합니다. 사용자에게 보고서 서버 액세스 권한을 부여할 때는 일반적으로 다음과 같이 역할 할당 쌍을 만듭니다.  
  
-   사이트 수준에서 만들기  
  
-   보고서 서버 폴더 계층의 루트 노드인 홈에서 만들기  
  
 보안은 보고서 서버 폴더 계층에서 상속됩니다. 사이트 수준 또는 홈 폴더에서 역할 할당을 만들면 보고서 서버의 모든 항목 및 작업으로 확장되는 사용 권한 상속이 설정됩니다.  
  
 개별 항목에 대해 보안을 정의하여 사용 권한 상속을 재정의할 수 있습니다. 개별적으로 보안을 설정할 수 있는 항목은 다음과 같습니다.  
  
-   폴더  
  
-   보고서  
  
-   보고서 모델  
  
-   리소스  
  
-   공유 데이터 원본  
  
-   공유 데이터 세트  
  
 일정 및 구독과 같은 기타 생성자는 보안이 명시적으로 설정되지 않습니다. 일정과 구독은 보고서의 보안 내에서 작동합니다.  
  
## <a name="item-descriptions"></a>항목 설명  
 다음 표에서는 보안 개체 항목을 표시하고 각각의 특징에 대해 설명합니다.  
  
|항목|특징|  
|----------|---------------------|  
|폴더|폴더 보안은 폴더 자체 및 폴더에 포함된 항목에 적용됩니다. 홈 폴더는 폴더 계층의 루트 노드입니다. 이 폴더에 대해 설정한 보안은 폴더 계층의 모든 종속 폴더, 보고서, 리소스 및 공유 데이터 원본에 대한 초기 보안 설정이 됩니다. 자세한 내용은 [폴더 보안](../../reporting-services/security/secure-folders.md)을 참조하세요.<br /><br /> 내 보고서는 전용 역할을 기반으로 암시된 역할 할당을 통해 보안되는 특수한 용도의 폴더입니다. 자세한 내용은 [내 보고서 보안 설정](../../reporting-services/security/secure-my-reports.md)을 참조하세요.|  
|보고서|보고서 및 링크된 보고서는 해당 보고서의 속성 변경 등 사용자가 수행할 수 있는 동작의 범위를 제어하여 보안을 설정할 수 있습니다.<br /><br /> 보고서 기록은 기록을 포함하는 보고서를 통해 보안 유지됩니다. 보고서 기록 내에서는 스냅샷을 개별적으로 보안 유지할 수 없습니다.<br /><br /> 보고서 보안에 대한 자세한 내용은 [보고서 및 리소스 보안](../../reporting-services/security/secure-reports-and-resources.md)을 참조하세요.|  
|보고서 모델|보고서 모델의 전체 또는 일부에 대해 역할 할당을 지정할 수 있습니다. 보고서 모델은 광범위할 수 있으므로 기밀 데이터로 매핑되는 모델 항목의 보안을 설정하는 것이 좋습니다.|  
|리소스|리소스는 리소스 자체 및 해당 속성에 대한 액세스를 제어하도록 보안을 설정할 수 있습니다.<br /><br /> 독립 실행형 리소스만 개별 항목으로 보안을 설정할 수 있습니다. 보고서에 포함된 리소스는 해당 보고서와 별도로 보안을 설정할 수 없습니다.<br /><br /> 리소스 보안에 대한 자세한 내용은 [보고서 및 리소스 보안](../../reporting-services/security/secure-reports-and-resources.md)을 참조하세요.|  
|공유 데이터 원본|공유 데이터 원본의 보안을 설정하여 항목과 해당 속성 페이지에 대한 액세스를 제한할 수 있습니다. 자세한 내용은 [공유 데이터 원본 항목 보안 설정](../../reporting-services/security/secure-shared-data-source-items.md)을 참조하세요.|  
|공유 데이터 세트|공유 데이터 세트는 해당 공유 데이터 세트의 정의 보기 또는 변경, 속성 변경 등 사용자가 수행할 수 있는 동작의 범위를 제어하여 보안을 설정할 수 있습니다.<br /><br /> 자세한 내용은 [공유 데이터 세트 항목 보안 설정](../../reporting-services/security/secure-shared-dataset-items.md)을 참조하세요.|  
  
## <a name="see-also"></a>참고 항목  
 [기본 모드 보고서 서버에 대한 사용 권한 부여](../../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md)   
 [역할 만들기, 삭제 또는 수정&#40;Management Studio&#41;](../../reporting-services/security/role-definitions-create-delete-or-modify.md)   
 [사용자에게 보고서 서버에 대한 액세스 권한 부여&#40;보고서 관리자&#41;](../../reporting-services/security/grant-user-access-to-a-report-server-report-manager.md)   
 [역할 할당 수정 또는 삭제&#40;보고서 관리자&#41;](../../reporting-services/security/role-assignments-modify-or-delete.md)  
  
  
