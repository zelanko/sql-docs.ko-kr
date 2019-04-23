---
title: 제거 된 독립 실행형 버전의 보고서 작성기 (보고서 작성기) | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 009538c6-4941-4393-b14b-9144cffdbdaf
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 10d6d79587051b78f212c5fbe4a9d866ee0c75e0
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/22/2019
ms.locfileid: "59960159"
---
# <a name="uninstall-the-stand-alone-version-of-report-builder-report-builder"></a>독립 실행형 버전의 보고서 작성기 제거(보고서 작성기)
  제어판 또는 명령줄에서 독립 실행형 버전의 보고서 작성기를 제거할 수 있습니다. [!INCLUDE[ndptecclick](../../includes/ndptecclick-md.md)] 버전 보고서 작성기는 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)]를 제거해야만 제거할 수 있습니다.  
  
 명령줄에서 보고서 작성기를 제거할 때 사용하는 구문은 보고서 작성기를 설치할 때 사용하는 구문과 동일하고 /i 옵션 대신 /x 옵션을 사용한다는 점만 다릅니다. 제거할 때 사용하는 명령줄에는 /quiet 옵션과 기타 표준 옵션도 포함될 수 있습니다. 보고서 작성기 Windows Installer 패키지(ReportBuilder3_x86.msi)가 이미 제거되었으면 명령줄을 사용하여 보고서 작성기를 제거하기 어렵습니다. 해당 GUID를 사용하여 보고서 작성기를 제거하는 방법에 대한 자세한 내용은 MSDN 라이브러리에서 msiexec 프로그램에 대한 설명서를 참조하십시오.  
  
 보고서 작성기용 폴더에 사용자 지정 파일이 포함되어 있으면 보고서 작성기를 제거할 때 해당 폴더와 파일이 유지되고 보고서 작성기 파일만 제거됩니다.  
  
### <a name="to-uninstall-report-builder-from-the-control-panel"></a>제어판에서 보고서 작성기를 제거하려면  
  
1.  **시작** 메뉴에서 **제어판**을 클릭합니다.  
  
2.  제어판에서 **프로그램 및 기능**을 클릭합니다.  
  
3.  **이름** 목록에서 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 보고서 작성기를 찾아 클릭합니다.  
  
4.  **제거**를 클릭합니다.  
  
5.  보고서 작성기를 제거할지 묻는 메시지가 표시되면 **예**를 클릭합니다.  
  
### <a name="to-uninstall-report-builder-from-the-command-line"></a>명령줄에서 보고서 작성기를 제거하려면  
  
1.  **시작** 메뉴에서 **실행**을 클릭합니다.  
  
2.  에 **열고** 텍스트 상자 `cmd.`  
  
3.  명령 프롬프트 창에서 ReportBuilder3_x86.msi가 있는 폴더로 이동합니다.  
  
4.  다음과 같은 기본 명령줄을 입력합니다.  
  
 `msiexec /x ReportBuilder3_x86.msi /quiet /l*v install.log`  
  
 로깅을 포함할 수 있는 경우 다음과 같은 명령줄을 사용합니다.  
  
 `msiexec /x ReportBuilder3_x86.msi /quiet /l*v c:\junk\install.log`  
  
1.  **Enter**키를 누릅니다.  
  
## <a name="see-also"></a>관련 항목  
 [설치, 제거 및 보고서 작성기 지원](../install-uninstall-and-report-builder-support.md)   
 [보고서 작성기의 독립 실행형 버전을 설치 &#40;보고서 작성기&#41;](install-report-builder.md)  
  
  
