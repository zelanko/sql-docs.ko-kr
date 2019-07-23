---
title: Integration Services 디자이너 옵션의 일반 페이지 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.Business_Intelligence_Designers.Data_Transformation_Designers.General
ms.assetid: d695690a-923b-4036-945e-7621e8651deb
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 4a403e63ef164db151eed148dd6b6fa6719d6649
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68102756"
---
# <a name="general-page-of-integration-services-designers-options"></a>Integration Services 디자이너 옵션의 일반 페이지

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  **옵션** 대화 상자에 있는 **Integration Services 디자이너** 페이지의 **일반** 페이지를 사용하여 패키지 로드, 표시 및 업그레이드 옵션을 지정할 수 있습니다.  
  
 **에서** 일반 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]페이지를 열려면 **도구** 메뉴에서 **옵션**을 클릭한 다음 **Business Intelligence 디자이너**를 확장하여 **Integration Services 디자이너**를 엽니다.  
  
## <a name="options"></a>옵션  
 **패키지 로드 시 디지털 서명 확인**  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 에서 패키지 로드 시 디지털 서명을 확인하도록 하려면 선택합니다. [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 에서는 디지털 서명이 있는지, 유효한지 신뢰할 수 있는 원본에서 가져온 것인지 여부만 확인합니다. [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 에서는 패키지가 서명된 이후 변경되었는지 여부는 확인하지 않습니다.  
  
 **BlockedSignatureStates** 레지스트리 값을 설정하면 이 레지스트리 값으로 인해 **패키지 로드 시 디지털 서명 확인** 옵션이 무시됩니다. 자세한 내용은 [레지스트리 값을 설정하여 서명 정책 구현](../integration-services/packages/implement-a-signing-policy-by-setting-a-registry-value.md)을 참조하세요.  
  
 디지털 인증서 및 패키지에 대한 자세한 내용은 [디지털 서명을 사용하여 패키지 원본 확인](../integration-services/security/identify-the-source-of-packages-with-digital-signatures.md)을 참조하세요.  
  
 **패키지가 서명되어 있지 않으면 경고 표시**  
 서명되어 있지 않은 패키지를 로드할 때 경고를 표시하려면 선택합니다.  
  
 **선행 제약 조건 레이블 표시**  
 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]에서 패키지를 확인할 때 선행 제약 조건에 표시할 레이블을 성공, 실패, 완료 중에서 선택합니다.  
  
 **스크립트 언어**  
 새 스크립트 태스크 및 스크립트 구성 요소에 대한 기본 스크립트 언어를 선택합니다.  
  
 **새 공급자 이름을 사용하도록 연결 문자열 업데이트**  
 [!INCLUDE[ssISversion2005](../includes/ssisversion2005-md.md)] 패키지를 열거나 업그레이드할 때 현재 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]버전에 대해 다음 공급자의 이름을 사용하도록 연결 문자열을 업데이트합니다.  
  
-   [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] OLE DB 공급자  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Native Client  
  
 [!INCLUDE[ssIS](../includes/ssis-md.md)] 패키지 업그레이드 마법사는 연결 관리자에 저장된 연결 문자열만 업데이트하며 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 식 언어 또는 스크립트 태스크의 코드를 사용하여 동적으로 생성된 연결 문자열은 업데이트하지 않습니다.  
  
 **새 패키지 ID 만들기**  
 [!INCLUDE[ssISversion2005](../includes/ssisversion2005-md.md)] 패키지를 업그레이드할 때 업그레이드된 버전의 패키지에 대해 새 패키지 ID를 만듭니다.  
  
## <a name="see-also"></a>참고 항목  
 [보안 개요&#40;Integration Services&#41;](../integration-services/security/security-overview-integration-services.md)   
 [스크립팅을 사용한 패키지 확장](../integration-services/extending-packages-scripting/extending-packages-with-scripting.md)  
  
  
