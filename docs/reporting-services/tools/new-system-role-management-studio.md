---
title: 새 시스템 역할(Management Studio) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: tools
ms.topic: conceptual
f1_keywords:
- sql13.swb.reportserver.newsystemrole.f1
ms.assetid: 7b4a0b98-975b-478a-8359-7db39ccbb347
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 4bb010a6f3b9c21661cfa840e6975cec51f90c84
ms.sourcegitcommit: dda9a1a7682ade466b8d4f0ca56f3a9ecc1ef44e
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 05/14/2019
ms.locfileid: "65582187"
---
# <a name="new-system-role-management-studio"></a>새 시스템 역할(Management Studio)
  이 페이지를 사용하여 시스템 수준의 역할 정의를 만들 수 있습니다. 시스템 역할 정의는 보고서 서버 전체에 적용되는 시스템 수준 태스크 집합을 지정합니다.  
  
> [!NOTE]  
>  역할 정의는 기본 모드로 실행되는 보고서 서버에만 사용되며 보고서 서버가 SharePoint 통합 모드로 구성된 경우 이 페이지를 사용할 수 없습니다.  
  
## <a name="options"></a>옵션  
 **이름**  
 역할 정의의 이름을 입력합니다. 역할 정의 이름은 보고서 서버 네임스페이스 내에서 고유해야 합니다. 이름은 하나 이상의 영숫자 문자를 포함해야 합니다. 공백과 특정 기호도 포함할 수 있습니다. 이름 지정 시에는 다음 문자를 사용하지 마십시오.  
  
 ; ? : \@ & = + , $ / * < >  
  
 " /  
  
 **설명**  
 역할 사용 방법을 설명하고 역할에서 지원하는 작업을 나열하는 설명을 제공합니다.  
  
 **태스크**  
 이 역할을 통해 수행할 수 있는 시스템 수준의 태스크를 선택합니다. 새 태스크를 만들거나 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에서 지원하는 기존 작업을 수정할 수 없습니다. 또한 시스템 역할 정의에 대해 항목 수준의 태스크를 선택할 수 없습니다.  
  
 **태스크 설명**  
 작업에서 지원하는 작업 또는 사용 권한을 열거하는 태스크에 대한 설명을 표시합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Management Studio의 보고서 서버 F1 도움말](../../reporting-services/tools/report-server-in-management-studio-f1-help.md)   
 [역할 정의](../../reporting-services/security/role-definitions.md)  
  
  
