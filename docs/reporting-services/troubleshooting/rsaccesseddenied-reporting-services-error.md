---
title: rsAccessedDenied - Reporting Services 오류 | Microsoft Docs
ms.date: 05/22/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: troubleshooting
ms.topic: conceptual
helpviewer_keywords:
- rsAccessDenied error
ms.assetid: 2f76b1bf-96a2-4755-b76b-84e933220efc
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 0063256e371585fe6d63a1a635aa286fca5a7d39
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "66270234"
---
# <a name="rsaccesseddenied---reporting-services-error"></a>rsAccessedDenied - Reporting Services 오류
  사용자가 작업을 수행할 수 있는 권한이 없는 경우 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 오류 **rsAccessedDenied** 가 발생합니다. 예를 들어 보고서를 열 수 있는 역할 할당이 없거나 필요한 사용 권한으로 브라우저를 열지 않았습니다.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]** [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 기본 모드 &#124; SharePoint 모드|  
  
- URL을 통해 보고서 서버에 직접 액세스하는 동안 오류가 발생한 경우 예외가 HTTP 401 오류에 매핑됩니다.  
  
- 웹 포털을 사용하는 동안 오류가 발생하는 경우 예외는 일반적으로 HTTP 401 오류 또는 정의된 다른 HTML 오류 페이지에 매핑됩니다.  
  
- 예약된 작업, 구독 또는 배달을 하는 동안 오류가 발생한 경우 오류가 보고서 서버 로그 파일에만 나타납니다.  
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|**제품 이름**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|**이벤트 ID**|rsAccessedDenied|  
|**이벤트 원본**|Microsoft.ReportingServices.Diagnostics.Utilities.ErrorStrings|  
|**구성 요소**|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|  
|**메시지 텍스트**|'mydomain\myAccount' 사용자에게 부여된 권한으로는 이 작업을 수행할 수 없습니다. (rsAccessDenied) (ReportingServicesLibrary)|  
  
## <a name="user-action"></a>사용자 조치  
 보고서 서버 내용 및 작업에 액세스하는 사용 권한은 역할 할당을 통해 부여됩니다. 새로 설치하는 경우 로컬 관리자만 보고서 서버에 액세스할 수 있습니다. 다른 사용자에게 액세스 권한을 부여하려면 로컬 관리자는 도메인 사용자나 그룹 계정을 지정하는 역할 할당, 사용자가 수행할 수 있는 태스크를 정의하는 하나 이상의 역할 그리고 범위(일반적으로 홈 폴더나 보고서 서버 폴더 계층의 루트 노드)를 만들어야 합니다. 웹 포털을 사용하여 역할 할당을 만들 수 있습니다. 자세한 내용은 [역할 할당](../../reporting-services/security/role-assignments.md)을 참조하세요.  
  
 또한 이 오류는 보고서 서버의 로컬 관리로 인해서도 발생합니다. 자세한 내용은 [로컬 관리에 대해 기본 모드 보고서 서버 구성&#40;SSRS&#41;](../../reporting-services/report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [역할 할당](../../reporting-services/security/role-assignments.md)  
 [기본 모드 보고서 서버에 대한 사용 권한 부여](../../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md)  
 [역할 및 권한&#40;Reporting Services&#41;](../../reporting-services/security/roles-and-permissions-reporting-services.md)  
  