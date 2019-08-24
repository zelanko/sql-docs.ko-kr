---
title: 확장 프로그램에 대한 보안 고려 사항 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- security [Reporting Services], extensions
- extensions [Reporting Services], security
- permissions [Reporting Services], extensions
ms.assetid: 58cbdfeb-1105-4a7d-a3b8-b897ff95f367
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 128da8d5bb3b956b5b5661ce47ca6e4b741f0bc5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63282423"
---
# <a name="security-considerations-for-extensions"></a>확장 프로그램에 대한 보안 고려 사항
  CLR(공용 언어 런타임) 기능이 있는 모든 애플리케이션은 CLR 보안 시스템과 상호 작용해야 합니다. 이러한 애플리케이션은 실행되면 CLR에 의해 자동으로 평가되어 권한 집합이 부여됩니다. 부여받은 권한에 따라 애플리케이션이 계속 실행될 수도 있고 보안 예외가 생성될 수도 있습니다. 특정 보고서 서버에 대한 보안 정책 구성 파일의 로컬 보안 설정 및 정책은 어셈블리에서 수신하는 코드 권한을 정의합니다.  
  
 권한을 요청하기 전에 확장 프로그램 코드에서 사용할 리소스 및 보호된 작업에 대해 알고 있어야 하며 이러한 리소스 및 작업을 보호하고 있는 권한도 알고 있어야 합니다. 또한 확장 프로그램 구성 요소가 호출하는 클래스 라이브러리 메서드에서 액세스하는 리소스도 추적해야 합니다. 자세한 내용은 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 개발자 가이드의 "Requesting Permissions(권한 요청)"를 참조하십시오.  
  
 보고서 서버에 배포된 확장 프로그램은 완전히 신뢰할 수 있는 상태로 실행되어야 합니다. 즉, 확장 프로그램은 **FullTrust** 권한 집합이 부여된 코드 그룹에 속해야 합니다. 또한 특정 보고서에 대해 인증되는 사용자에 따라 확장 프로그램이 CLR을 통해 사용할 수 있는 특정 서버 리소스 및 작업에 대한 액세스 권한을 가질 수 있음을 의미합니다. 코드 그룹 및 확장에 관한 자세한 내용은 [Reporting Services의 코드 액세스 보안](secure-development/code-access-security-in-reporting-services.md)을 참조하세요.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에서는 모든 확장 프로그램에 대해 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 보안을 적용합니다.  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에서 데이터 처리, 배달, 렌더링 및 보안 확장 프로그램의 배포에 다음 조건이 적용됩니다.  
  
-   로컬 관리자만 확장 프로그램을 배포할 수 있는 권한을 가집니다.  
  
-   적절한 읽기/쓰기 권한을 가진 사용자만 확장할 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 요소에 대한 구성 파일을 변경할 수 있습니다.  
  
-   권한이 있는 사용자만 보안 정책 파일을 편집하고 확장 프로그램에 대한 코드 액세스 보안을 사용할 수 있는 권한을 가집니다.  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]의 코드 액세스 보안에 대한 자세한 내용은 [보안 개발 & #40; Reporting Services& #41;](secure-development/secure-development-reporting-services.md)를 참조하세요.  
  
 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 보안에 대한 자세한 내용은 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 개발자 가이드의 ".NET Framework Security(.NET Framework 보안)"를 참조하십시오.  
  
## <a name="initialization-of-extension-assemblies"></a>확장 프로그램 어셈블리 초기화  
 일부 확장 프로그램 어셈블리에서 시스템 리소스 액세스, 구성 파일 읽기 및 다른 종속 어셈블리 로드 작업을 수행하려면 특정 권한이 필요하므로 보고서 서버에서 확장 프로그램이 메모리로 처음 로드될 때 서비스 계정 자격 증명이 사용됩니다. 하지만 어셈블리가 로드되고 초기화된 후 확장 프로그램 어셈블리에 대한 이후의 모든 호출에서는 현재 로그온한 사용자 계정의 자격 증명을 사용합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Reporting Services 확장 프로그램](reporting-services-extensions.md)   
 [Reporting Services 확장 라이브러리](reporting-services-extension-library.md)  
  
  
