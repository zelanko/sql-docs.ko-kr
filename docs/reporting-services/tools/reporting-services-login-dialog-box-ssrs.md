---
title: Reporting Services 로그인 대화 상자 | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: tools
ms.topic: reference
f1_keywords:
- sql13.rtp.rptdesigner.reportservicelogin.f1
ms.assetid: 2037d797-0b61-44c7-931f-6c689c3fc733
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 3d60450f0f4c7feb7d6a00f66fcedeb89c764bf5
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "77082168"
---
# <a name="reporting-services-login-dialog-box-ssrs"></a>Reporting Services 로그인 대화 상자(SSRS)
  **Reporting Services 로그인** 대화 상자를 사용하여 보고서 서버에 보고서를 게시하는 데 사용할 자격 증명을 제공할 수 있습니다.  
  
-   **참고** 프로젝트에 대한 **TargetServerURL** 배포 속성을 설정한 이후 보고서 서버에 보고서를 처음 게시한 것이면 서버 이름에 **reports** 가 아니라 **server**가 포함되어 있는지 확인합니다. 예를 들어 `https://localhost/reportserver`가 아니라 `https://localhost/reports`여야 합니다. 로컬 서버에 `reports` 디렉터리 대신 `reportserver` 디렉터리를 지정할 경우 이 대화 상자가 열립니다. **TargetServerURL** 설정 방법에 대한 자세한 내용은 [배포 속성 설정&#40;Reporting Services&#41;](../../reporting-services/tools/set-deployment-properties-reporting-services.md)을 참조하세요.  
  
## <a name="options"></a>옵션  
 **Server**  
 보고서 서버의 이름을 표시합니다. `https://localhost/reportserver`)을 입력합니다. 기본 포트 80 이외의 다른 포트를 사용하는 보고서 서버의 경우 포트 번호를 포함해야 합니다. `https://localhost:81/reportserver`)을 입력합니다.  
  
 **사용자 이름**  
 웹 서비스에 로그인할 사용자 이름을 입력합니다.  
  
 **암호**  
 웹 서비스에 로그인할 암호를 입력합니다.  
  
## <a name="see-also"></a>참고 항목  
 [데이터 연결 문자열 만들기 - 보고서 작성기 및 SSRS](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)   
 [보고서 데이터 원본에 대한 자격 증명 및 연결 정보 지정](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md)   
 [보고서 디자이너 F1 도움말](../../reporting-services/tools/report-designer-f1-help.md)  
  
  
