---
title: "보고서 작성기 제거 | Microsoft Docs"
ms.custom: 
ms.date: 05/30/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: install-windows
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 009538c6-4941-4393-b14b-9144cffdbdaf
caps.latest.revision: "10"
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 2ca635948940ec0a8921444d2b7928d53e16c70f
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/09/2018
---
# <a name="uninstall-report-builder"></a>보고서 작성기 제거

제어판 또는 명령줄에서 독립 실행형 버전의 보고서 작성기를 제거할 수 있습니다.

명령줄에서 보고서 작성기를 제거할 때 사용하는 구문은 보고서 작성기를 설치할 때 사용하는 구문과 동일하고 /i 옵션 대신 /x 옵션을 사용한다는 점만 다릅니다. 제거할 때 사용하는 명령줄에는 /quiet 옵션과 기타 표준 옵션도 포함될 수 있습니다. 보고서 작성기 Windows Installer 패키지(ReportBuilder3_x86.msi)가 이미 제거되었으면 명령줄을 사용하여 보고서 작성기를 제거하기 어렵습니다. 해당 GUID를 사용하여 보고서 작성기를 제거하는 방법은 [Command-Line Options](https://msdn.microsoft.com/library/windows/desktop/aa367988.aspx)(명령줄 옵션)에서 msiexec 프로그램에 대한 설명서를 참조하세요.  

보고서 작성기용 폴더에 사용자 지정 파일이 포함되어 있으면 보고서 작성기를 제거할 때 해당 폴더와 파일이 유지되고 보고서 작성기 파일만 제거됩니다.  

### <a name="to-uninstall-report-builder-from-the-control-panel"></a>제어판에서 보고서 작성기를 제거하려면

1.  **시작** 메뉴에서 **제어판**을 클릭합니다.  
  
2.  제어판에서 **프로그램 및 기능**을 클릭합니다.  
  
3.  **이름** 목록에서 [!INCLUDE[msCoName](../../includes/msconame-md.md)] SQL Server 2016 보고서 작성기를 찾아 클릭합니다.  
  
4.  **제거**를 클릭합니다.  
  
5.  보고서 작성기를 제거할지 묻는 메시지가 표시되면 **예**를 클릭합니다.  
  
### <a name="to-uninstall-report-builder-from-the-command-line"></a>명령줄에서 보고서 작성기를 제거하려면  
  
1.  **시작** 메뉴에서 **실행**을 클릭합니다.  
  
2.  **열기** 입력란에 **cmd.**을(를) 입력합니다.  
  
3.  명령 프롬프트 창에서 ReportBuilder3_x86.msi가 있는 폴더로 이동합니다.  
  
4.  다음과 같은 기본 명령줄을 입력합니다.  
  
 `msiexec /x ReportBuilder3_x86.msi /quiet /l*v install.log`  
  
 로깅을 포함할 수 있는 경우 다음과 같은 명령줄을 사용합니다.  
  
 `msiexec /x ReportBuilder3_x86.msi /quiet /l*v c:\junk\install.log`  
  
5.  **Enter**키를 누릅니다.  

## <a name="next-steps"></a>다음 단계

[보고서 작성기 설치](../../reporting-services/install-windows/install-report-builder.md)  

추가 질문이 있으신가요? [Reporting Services 포럼에서 질문하기](http://go.microsoft.com/fwlink/?LinkId=620231)
