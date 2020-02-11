---
title: 데이터 원본 속성 대화 상자, 자격 증명 | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.datasourceproperties.credentials.f1
- "10100"
ms.assetid: 14c3eeb6-d37b-4fda-967b-43afcdb48119
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: ed5b58aa9a4fe81a55e602fb61f673bf10059ee7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66109449"
---
# <a name="data-source-properties-dialog-box-credentials"></a>데이터 원본 속성 대화 상자, 자격 증명
  
  **데이터 원본 속성** 대화 상자의 **자격 증명** 을 선택하여 보고서의 데이터 원본에 연결하는 데 사용할 자격 증명을 표시하고 수정할 수 있습니다. 사용자가 제공하는 자격 증명은 데이터 원본에 액세스하고 보고서를 미리 보기 위해 데이터의 복사본을 캐시하는 데 사용됩니다. 미리 보기 데이터 캐시 방법에 대한 자세한 내용은 [보고서 미리 보기](reports/previewing-reports.md)를 참조하세요. 자격 증명에 대한 자세한 내용은 [보고서 데이터 원본에 대한 자격 증명 및 연결 정보 지정](report-data/specify-credential-and-connection-information-for-report-data-sources.md)을 참조하세요.  
  
## <a name="options"></a>옵션  
 **Windows 인증 사용(통합 보안)**  
 Windows 인증을 사용하려면 이 옵션을 선택합니다.  
  
 **이 사용자 이름 및 암호 사용**  
 특정 사용자 이름 및 암호를 제공하려면 이 옵션을 선택합니다. 공유 데이터 원본의 경우 보고서 서버 프로젝트를 대상 서버에 게시하면 사용자 이름과 암호가 데이터베이스에 대해 저장된 자격 증명으로 저장됩니다. 사용자 이름과 암호를 Windows 자격 증명으로 사용하려는 경우 대상 서버에서 게시된 공유 데이터 원본에 대한 속성을 편집할 수 있습니다. 자세한 내용은 [공유 데이터 원본 만들기, 삭제 또는 수정&#40;보고서 관리자&#41;](../../2014/reporting-services/create-delete-or-modify-a-shared-data-source-report-manager.md)을 참조하세요.  
  
 **사용자 이름**  
 데이터 원본에 로그인할 때 사용할 사용자 이름을 입력합니다.  
  
 **암호**  
 데이터 원본에 로그인할 때 사용할 암호를 입력합니다.  
  
 **자격 증명 확인**  
 보고서 실행 시 자격 증명을 요청하려면 이 옵션을 선택합니다.  
  
 **프롬프트 문자열 입력**  
 데이터 원본에 대한 로그인 자격 증명을 제공하도록 사용자에게 표시할 메시지를 입력합니다.  
  
 **자격 증명 사용 안 함**  
 데이터 원본에 대해 자격 증명을 사용하지 않으려면 이 옵션을 선택합니다. 이 옵션은 데이터 원본이 자격 증명을 허용하지 않거나 다른 방법으로 자격 증명을 전달하는 경우에만 작동합니다.  
  
## <a name="see-also"></a>참고 항목  
 [데이터 원본 속성 대화 상자, 일반](../../2014/reporting-services/data-source-properties-dialog-box-general.md)   
 [보고서 데이터 원본에 대 한 자격 증명 및 연결 정보 지정](report-data/specify-credential-and-connection-information-for-report-data-sources.md)   
 [Data Connections, Data Sources, and Connection Strings in Reporting Services](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-reporting-services.md)  
  
  
