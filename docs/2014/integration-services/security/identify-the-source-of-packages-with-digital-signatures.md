---
title: 디지털 서명을 사용하여 패키지 원본 확인 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- signing packages [Integration Services]
- certificates [Integration Services]
- packages [Integration Services], security
- security [Integration Services], certificates
- signing policies [Integration Services]
ms.assetid: a433fbef-1853-4740-9d5e-8a32bc4ffbb2
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 714ede33a89a3ab4e44dae682887ee0c21c9f363
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/22/2019
ms.locfileid: "58375671"
---
# <a name="identify-the-source-of-packages-with-digital-signatures"></a>디지털 서명을 사용하여 패키지 원본 확인
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지에 해당 원본을 식별하는 디지털 인증서를 사용하여 서명할 수 있습니다. 디지털 인증서를 사용하여 패키지에 서명하면 패키지를 로드하기 전에 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에서 디지털 서명을 확인하도록 할 수 있습니다. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에서 서명을 확인하도록 하려면 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 또는 **dtexec** 유틸리티(dtexec.exe)에서 옵션을 설정하거나 선택적 레지스트리 값을 설정합니다.  
  
## <a name="signing-a-package-with-a-digital-certificate"></a>디지털 인증서를 사용하여 패키지 서명  
 디지털 인증서를 사용하여 패키지에 서명하려면 먼저 인증서를 만들거나 가져와야 합니다. 인증서가 있으면 이 인증서를 사용하여 패키지에 서명할 수 있습니다. 인증서를 가져오고 해당 인증서를 사용하여 패키지에 서명하는 방법에 대한 자세한 내용은 [디지털 인증서를 사용하여 패키지 서명](../sign-a-package-by-using-a-digital-certificate.md)을 참조하세요.  
  
## <a name="setting-an-option-to-check-the-package-signature"></a>패키지 서명을 확인하는 옵션 설정  
 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 및 **dtexec** 유틸리티 모두에는 서명된 패키지의 디지털 서명을 확인하도록 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 를 구성하는 옵션이 있습니다. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 또는 **dtexec** 유틸리티 중 무엇을 사용할지는 다음과 같이 모든 패키지를 확인할지 또는 특정 패키지만 확인할지에 따라 결정합니다.  
  
-   디자인 타임에 패키지를 로드하기 전에 모든 패키지의 디지털 서명을 확인하려면 **에서** 패키지 로드 시 디지털 서명 확인 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]옵션을 설정합니다. 이 옵션은 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]의 모든 패키지에 대한 전역 설정입니다. 자세한 내용은 [General Page](../general-page-of-integration-services-designers-options.md)을 참조하세요.  
  
-   개별 패키지의 디지털 서명을 확인 하려면 지정 합니다 `/VerifyS[igned]` 옵션을 사용 하는 경우는 **dtexec** 패키지를 실행 하는 유틸리티입니다. 자세한 내용은 [dtexec Utility](../packages/dtexec-utility.md)를 참조하세요.  
  
## <a name="setting-a-registry-value-to-check-the-package-signature"></a>패키지 서명을 확인하는 레지스트리 값 설정  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에서는 서명되거나 서명되지 않은 패키지에 대한 조직의 정책을 관리하는 데 사용할 수 있는 선택적 레지스트리 값인 **BlockedSignatureStates**도 지원합니다. 이 레지스트리 값을 사용하면 패키지에 서명이 없거나 패키지의 서명이 잘못되거나 신뢰할 수 없는 경우 패키지를 로드하지 못하게 할 수 있습니다. 이 레지스트리 값을 설정하는 방법에 대한 자세한 내용은 [레지스트리 값을 설정하여 서명 정책 구현](../implement-a-signing-policy-by-setting-a-registry-value.md)을 참조하세요.  
  
> [!NOTE]  
>  선택적 **BlockedSignatureStates** 레지스트리 값은 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 또는 **dtexec** 명령줄에서 설정한 디지털 서명 옵션보다 더 제한적인 설정을 지정할 수 있습니다. 이 경우 더 제한적인 설정이 다른 설정보다 우선합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Integration Services&#40;SSIS&#41; 패키지](../integration-services-ssis-packages.md)   
 [보안 개요&#40;Integration Services&#41;](security-overview-integration-services.md)  
  
  
