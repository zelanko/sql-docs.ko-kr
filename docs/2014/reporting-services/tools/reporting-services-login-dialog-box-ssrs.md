---
title: Reporting Services 로그인 대화 상자(SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.reportservicelogin.f1
ms.assetid: 2037d797-0b61-44c7-931f-6c689c3fc733
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 7f4753ba89da99753463a852ae38456e56cec3b3
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/22/2019
ms.locfileid: "59960749"
---
# <a name="reporting-services-login-dialog-box-ssrs"></a>Reporting Services 로그인 대화 상자(SSRS)
  **Reporting Services 로그인** 대화 상자를 사용하여 보고서 서버에 보고서를 게시하는 데 사용할 자격 증명을 제공할 수 있습니다.  
  
-   **참고** 프로젝트에 대한 **TargetServerURL** 배포 속성을 설정한 이후 보고서 서버에 보고서를 처음 게시한 경우에는 지정한 서버 이름이 `http://localhost/reportserver`가 아니라 `http://localhost/reports`와 비슷한 형태인지 확인하십시오. 로컬 서버에 `reports` 디렉터리 대신 `reportserver` 디렉터리를 지정할 경우 이 대화 상자가 열립니다. **TargetServerURL** 설정 방법에 대한 자세한 내용은 [배포 속성 설정&#40;Reporting Services&#41;](set-deployment-properties-reporting-services.md)을 참조하세요.  
  
## <a name="options"></a>변수  
 **Server**  
 보고서 서버의 이름을 표시합니다. `http://localhost/reportserver`)을 입력합니다. 기본 포트 80 이외의 다른 포트를 사용하는 보고서 서버의 경우 포트 번호를 포함해야 합니다. `http://localhost:81/reportserver`) 을 입력합니다.  
  
 **사용자 이름**  
 웹 서비스에 로그인할 사용자 이름을 입력합니다.  
  
 **암호**  
 웹 서비스에 로그인할 암호를 입력합니다.  
  
## <a name="see-also"></a>관련 항목  
 [데이터 연결, 데이터 원본 및 Reporting Services의 연결 문자열](../data-connections-data-sources-and-connection-strings-in-reporting-services.md)   
 [보고서 데이터 원본에 대 한 연결 정보와 자격 증명 지정](../report-data/specify-credential-and-connection-information-for-report-data-sources.md) [보고서 디자이너 F1 도움말](report-designer-f1-help.md)  
  
  
