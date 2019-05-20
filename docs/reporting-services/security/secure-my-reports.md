---
title: 내 보고서 보안 설정 | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- denying My Reports folder access
- private folders [Reporting Services]
- user workspace [Reporting Services]
- security [Reporting Services], My Reports folder
- My Reports folder [Reporting Services]
ms.assetid: 3b23a382-13b8-4196-9a93-7fe62d03a63c
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 7973c4ad5483193aa4ed2116b714f6d404c4da1c
ms.sourcegitcommit: dda9a1a7682ade466b8d4f0ca56f3a9ecc1ef44e
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 05/14/2019
ms.locfileid: "65570694"
---
# <a name="secure-my-reports"></a>내 보고서 보안 설정
  내 보고서 기능은 보고서 작업을 위한 사용자 관리 작업 영역을 제공합니다. 원래 용도대로 사용하려면 내 보고서 폴더는 여러 사용자가 사용할 수 있는 다른 폴더보다 권한 제한이 적어야 합니다. 다른 폴더의 보고서를 보고 실행할 수 있는 권한만 있는 사용자가 내 보고서 폴더와 자신이 소유한 내용을 관리하려면 확장된 권한이 있어야 합니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 는 이 용도에 맞는 특별한 역할 할당과 역할 정의를 제공합니다.  
  
> [!NOTE]
>  내 보고서는 보고서 관리자에서만 사용할 수 있으며 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에서는 사용할 수 없습니다.  
  
## <a name="role-assignment-for-my-reports"></a>내 보고서에 대한 역할 할당  
 내 보고서에 대한 역할 할당에는 미리 설정된 요소가 있으며 내 보고서 폴더를 활성화하는 각 사용자에 대해 자동으로 생성됩니다. 보고서 서버가 자동으로 보안을 할당하도록 하면 관리자가 각각의 내 보고서 사용자에 대해 액세스할 수 있도록 설정하지 않아도 되므로 내 보고서를 광범위하게 사용하는 조직에 특히 유용합니다.  
  
 **내 보고서** 역할 할당은 다음과 같은 요소로 구성됩니다.  
  
-   사용자 폴더\\*\<username>* \내 보고서 폴더에 있는 사용자의 내 보고서 폴더  
  
-   내 보고서 폴더 활성화 시 결정되는 사용자 계정. 사용자가 보고서 관리자에서 내 보고서 폴더를 클릭하거나 보고서 디자이너에서 내 보고서 폴더에 보고서를 게시할 때 폴더가 활성화됩니다. 이 폴더는 사용자가 내 보고서 링크에 대한 속성을 요청할 때도 활성화됩니다.  
  
-   내 보고서에 대해 미리 정의된 역할 정의  
  
## <a name="role-definition-for-my-reports"></a>내 보고서에 대한 역할 정의  
 **내 보고서** 역할 정의에는 내 보고서 폴더의 내용 관리를 지원하는 태스크가 포함됩니다. **내 보고서** 역할은 한 가지 용도의 역할로 생성되었습니다. 모든 항목 수준의 보안 정책으로 이 역할을 선택할 수는 있지만 다른 폴더 요구 사항에 맞게 수정하는 작업을 최소화하려면 그렇게 하지 않는 것이 좋습니다. 내 보고서 기능에 대해 **내 보고서** 역할을 예약하면 여러 사용자에 대해 일관된 역할을 유지할 수 있습니다.  
  
 기본적으로 보고서 서버 관리자만 **내 보고서** 역할을 수정합니다. 포함된 태스크를 변경하여 **내 보고서** 역할을 사용자 지정할 수 있습니다. 다른 역할로 대체할 수도 있습니다.  
  
## <a name="denying-access-to-my-reports"></a>내 보고서에 대한 액세스 거부  
 다음과 같은 방법으로 다른 사용자가 내 보고서에 액세스하지 못하도록 할 수 있습니다.  
  
-   사이트 설정 페이지에서 내 보고서 해제. 자세한 내용은 [내 보고서 설정 및 해제](../../reporting-services/report-server/enable-and-disable-my-reports.md)를 참조하세요.  
  
-   **내 보고서** 역할에서 모든 태스크 제거  
  
 내 보고서를 해제하면 내 보고서 폴더에 대한 링크가 보고서 관리자에서 제거됩니다. 내 보고서를 지원하는 기본 폴더 구조, 즉 사용자 폴더 폴더와 하위 폴더는 계속 사용할 수 있으며 사용자가 폴더 경로를 알고 있으면 액세스할 수 있습니다. **내 보고서** 역할에서 태스크를 제거하면 액세스할 수 없게 됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [보고서 및 리소스 보안](../../reporting-services/security/secure-reports-and-resources.md)   
 [보안 폴더](../../reporting-services/security/secure-folders.md)   
 [기본 모드 보고서 서버에 대한 사용 권한 부여](../../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md)  
  
  
