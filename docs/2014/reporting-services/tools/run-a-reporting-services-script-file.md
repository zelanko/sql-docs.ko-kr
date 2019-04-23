---
title: Reporting Services 스크립트 파일 실행 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- scripts [Reporting Services], running
ms.assetid: 0de4995c-85ec-4d4c-aaef-fbd30edfb20f
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 8d4023d5fb434f58fd031e6512f3fa84fa551fec
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/22/2019
ms.locfileid: "59958859"
---
# <a name="run-a-reporting-services-script-file"></a>Reporting Services 스크립트 파일 실행
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 스크립트 파일은 명령 프롬프트에서 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 스크립트 환경(RS.exe)을 사용하여 실행합니다. RS.exe에는 사용할 수 있는 많은 명령 프롬프트 인수가 있습니다. 명령 프롬프트 옵션에 대한 자세한 내용은 [RS.exe 유틸리티&#40;SSRS&#41;](rs-exe-utility-ssrs.md)를 참조하세요. 추가 스크립트 예제는 [SQL Server Reporting Services 제품 예제(SQL Server Reporting Services Product Samples)](https://go.microsoft.com/fwlink/?LinkId=177889)를 참조하십시오.  
  
## <a name="sample-command-lines"></a>예제 명령줄  
  
-   대상 보고서 서버를 지정하여 스크립트 환경에서 Script.rss를 실행합니다. 기본적으로 Windows 인증이 적용됩니다.  
  
    ```  
    rs -i Script.rss -s http://servername/reportserver  
    ```  
  
-   웹 서비스 호출을 인증하기 위한 사용자 이름과 암호를 지정하여 스크립트 환경에서 Script.rss를 실행합니다.  
  
    ```  
    rs -i Script.rss -s http://servername/reportserver -u myusername -p mypassword  
    ```  
  
-   서버 제한 시간을 30초로 지정하여 스크립트 환경에서 Script.rss를 실행합니다.  
  
    ```  
    rs -i Script.rss -s http://servername/reportserver -l 30  
    ```  
  
-   *report*라는 전역 스크립트 변수를 지정하여 스크립트 환경에서 Script.rss를 실행합니다.  
  
    ```  
    rs -i Script.rss -s http://servername/reportserver -v report="Company Sales"  
    ```  
  
-   스크립트 파일의 웹 서비스 작업이 일괄 처리로 실행되도록 지정하여 스크립트 환경에서 Script.rss를 실행합니다.  
  
    ```  
    rs -i Script.rss -s http://servername/reportserver -b  
    ```  
  
## <a name="see-also"></a>관련 항목  
 [기술 참조&#40;SSRS&#41;](../technical-reference-ssrs.md)  
  
  
