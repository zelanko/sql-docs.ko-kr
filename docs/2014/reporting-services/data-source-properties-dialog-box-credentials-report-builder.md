---
title: 데이터 원본 속성 대화 상자, 자격 증명 (보고서 작성기) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- "10017"
ms.assetid: 4531f09f-d653-4c05-a120-d7788838bc99
caps.latest.revision: 11
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 237e1c9ef26c5dba838fa8071b2dce7293f2077a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36186917"
---
# <a name="data-source-properties-dialog-box-credentials-report-builder"></a>데이터 원본 속성 대화 상자, 자격 증명(보고서 작성기)
  **데이터 원본 속성** 대화 상자에서 **자격 증명** 을 선택하여 보고서의 포함된 데이터 원본에 연결하는 데 사용할 자격 증명을 표시하고 수정할 수 있습니다. 사용자가 제공하는 자격 증명은 데이터 원본에 액세스하여 보고서를 미리 보는 데 사용됩니다. 자격 증명에 대한 자세한 내용은 [보고서 작성기에 자격 증명 지정](../../2014/reporting-services/specify-credentials-in-report-builder.md)을 참조하세요.  
  
## <a name="options"></a>변수  
 **Windows 인증 (통합된 보안)를 사용 하 여**  
 Windows 인증을 사용하려면 이 옵션을 선택합니다.  
  
 **이 사용자 이름 및 암호 사용**  
 특정 사용자 이름 및 암호를 제공하려면 이 옵션을 선택합니다. 포함된 데이터 원본의 경우 보고서 서버 프로젝트를 대상 서버에 게시하면 사용자 이름과 암호가 데이터베이스에 대해 저장된 자격 증명으로 저장됩니다. 사용자 이름과 암호를 Windows 자격 증명으로 사용하려는 경우 대상 서버에서 게시된 공유 데이터 원본에 대한 속성을 변경할 수 있습니다. 자세한 내용은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [온라인 설명서](http://go.microsoft.com/fwlink/?linkid=121312)의 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 설명서에서 [공유 데이터 원본 만들기, 삭제 또는 수정&#40;보고서 관리자&#41;](../../2014/reporting-services/create-delete-or-modify-a-shared-data-source-report-manager.md)을 참조하세요.  
  
 **사용자 이름**  
 데이터 원본에 로그온할 때 사용할 사용자 이름을 입력합니다.  
  
 **암호**  
 데이터 원본에 로그온할 때 사용할 암호를 입력합니다.  
  
 **자격 증명 확인**  
 보고서 실행 시 자격 증명을 요청하려면 이 옵션을 선택합니다.  
  
 **프롬프트 문자열 입력**  
 데이터 원본에 대한 로그인 자격 증명을 제공하도록 사용자에게 표시할 메시지를 입력합니다.  
  
 **자격 증명 없음**  
 데이터 원본에 대해 자격 증명을 사용하지 않으려면 이 옵션을 선택합니다. 이 옵션은 데이터 원본이 자격 증명을 허용하지 않거나 다른 방법으로 자격 증명을 전달하는 경우에만 작동합니다.  
  
 일부 데이터 확장 프로그램의 경우 보고서 서버에 무인 실행 계정을 구성해야 합니다.  
  
 자세한 내용은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [온라인 설명서](http://go.microsoft.com/fwlink/?linkid=121312)의 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 설명서에서 [외부 데이터 원본의 데이터 추가&#40;SSRS&#41;](report-data/add-data-from-external-data-sources-ssrs.md) 및 [무인 실행 계정 구성&#40;SSRS 구성 관리자&#41;](install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md)의 해당하는 데이터 원본 유형에 대한 항목을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [대화 상자, 창 및 마법사에 대한 보고서 작성기 도움말](../../2014/reporting-services/report-builder-help-for-dialog-boxes-panes-and-wizards.md)   
 [데이터 원본 속성 대화 상자, 일반&#40;보고서 작성기&#41;](../../2014/reporting-services/data-source-properties-dialog-box-general-report-builder.md)   
 [데이터 연결이 나 데이터 원본 추가 및 확인 &#40;보고서 작성기 및 SSRS&#41;](report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)   
 [보고서에 데이터 추가 &#40;보고서 작성기 및 SSRS&#41;](report-data/report-datasets-ssrs.md)  
  
  