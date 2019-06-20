---
title: 독립 실행형 버전의 보고서 작성기 (보고서 작성기) | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 6b2291bb-1d20-4d08-81cb-a16dd8e01faf
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: c60455bf38fc0cb8efb3ce44e4121adfe099a393
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66108787"
---
# <a name="install-the-stand-alone-version-of-report-builder-report-builder"></a>독립 실행형 버전의 보고서 작성기 설치(보고서 작성기)
  보고서 작성기를 설치할 수는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 기능 팩에는 [Microsoft 다운로드 센터](https://go.microsoft.com/fwlink/?LinkID=168472) 또는 보고서 작성기는 Windows Installer 패키지인 ReportBuilder3_x86.msi를가지고 있는 공용 폴더와 같은 위치 다운로드 되었습니다.  
  
 보고서 작성기의 명령줄 설치를 수행하고 인수를 제공하여 설치를 사용자 지정할 수도 있습니다. 표준 MSI 내장 매개 변수 외에도 보고서 작성기를 제공 하는 사용자 지정 매개 변수를 사용할 수 있습니다. RBINSTALLDIR과 REPORTSERVERURL입니다. RBINSTALLDIR은 보고서 작성기의 루트 설치 폴더를 지정합니다. REPORTSERVERURL은 보고서 작성기에서 보고서를 서버에 저장하기 위해 사용하는 기본 보고서 서버를 지정합니다.  
  
 사용자 인터페이스의 상호 작용이 필요 없는 완전 자동 설치를 수행하려면 **/quiet** 옵션을 지정합니다. 기본적으로 quiet 옵션 플래그를 사용하면 설치 오류가 표시되지 않습니다. 따라서 quite 옵션을 사용할 때는 로깅을 지정하는 **/l** 옵션을 함께 사용하는 것이 좋습니다.  
  
> [!IMPORTANT]  
>  Windows Vista 및 Windows 7의 경우 보안 기능으로 인해 명령줄 작업을 실행하려면 높은 권한이 필요합니다. 따라서 명령줄을 실행할 경우 사용 권한을 요청하는 메시지가 표시되므로 자동 설치를 수행할 수 없습니다. 자동 설치를 수행하려면 관리자 권한으로 명령줄을 실행해야 합니다.  
  
### <a name="to-install-report-builder-from-the-download-site"></a>다운로드 사이트에서 보고서 작성기를 설치하려면  
  
1.  로 이동 [Microsoft SQL Server 2012 보고서 작성기](https://go.microsoft.com/fwlink/?LinkID=219138) 웹 페이지의 보고서 작성기 섹션을 찾습니다.  
  
2.  클릭 **X86 패키지**합니다.  
  
3.  에 **파일 다운로드** 대화 상자, 클릭 **실행**합니다.  
  
    > [!IMPORTANT]  
    >  신뢰할 수 있는 출처에서 제공하는 파일만 다운로드합니다.  
  
4.  Internet Explorer 대화 상자에서 클릭 **실행**합니다.  
  
    > [!IMPORTANT]  
    >  신뢰할 수 있는 출처에서 제공하는 파일만 실행합니다.  
  
5.  Microsoft SQL Server 보고서 작성기 마법사가 시작됩니다.  
  
6.  에 **설치 마법사 시작** 페이지에서 클릭 **다음**합니다.  
  
7.  에 **사용권 계약** 페이지에서 계약 내용을 읽고 하 고 다음을 선택 합니다 **사용권 계약에 동의** 옵션. **다음**을 클릭합니다.  
  
8.  사용자 이름과 회사 이름을 입력합니다. **다음**을 클릭합니다.  
  
9. 에 **기능 선택** 페이지에서 필요에 따라 **찾아보기** 하거나 **디스크 공간**입니다. **다음**을 클릭합니다.  
  
    -   클릭 **찾아보기** 에 보고서 작성기의 기본 위치를 확인 하 고 업데이트 합니다.  
  
        > [!NOTE]  
        >  보고서 작성기의 기본 설치 폴더는 \<드라이브 > Program Files\Microsoft SQL Server입니다.  
  
    -   클릭 **디스크 공간** 자세한 디스크 공간 보고서 작성기를 사용 합니다.  
  
        > [!NOTE]  
        >  볼륨에 디스크 여유 공간이 충분하지 않은 경우 해당 볼륨이 강조 표시됩니다.  
  
10. **기본 대상 서버** 페이지에서 필요 시 대상 보고서 서버의 URL을 제공합니다(기본값과 다른 경우). **다음**을 클릭합니다.  
  
    > [!NOTE]  
    >  보고서 서버에 연결되었을 때 보고서 작성기로 작업할 계획이라면 이 단계에서 서버의 URL을 제공하는 것이 좋습니다. 그러나 또한 가능에서이 **옵션** 보고서 작성기에서 작업할 때 대화 상자.  
  
11. 클릭 **설치** 의 보고서 작성기 설치를 완료 합니다.  
  
### <a name="to-install-report-builder-from-a-share"></a>공유에서 보고서 작성기를 설치하려면  
  
1.  로컬 컴퓨터에 보고서 작성기를 설치하기 위해 실행하는 ReportBuilder3_x86.msi.msi의 위치는 관리자에게 문의하십시오.  
  
2.  보고서 작성기의 Windows Installer 패키지(MSI)인 ReportBuilder3_x86.msi.msi를 찾아서 클릭합니다.  
  
     Microsoft SQL Server 보고서 작성기 마법사가 시작됩니다.  
  
3.  에 **설치 마법사 시작** 페이지에서 클릭 **다음**합니다.  
  
4.  에 **사용권 계약** 페이지에서 계약 내용을 읽고 하 고 다음을 선택 합니다 **사용권 계약에 동의** 옵션. **다음**을 클릭합니다.  
  
5.  사용자 이름과 회사 이름을 입력합니다. **다음**을 클릭합니다.  
  
6.  에 **기능 선택** 페이지에서 필요에 따라 **찾아보기** 하거나 **디스크 공간**입니다. **다음**을 클릭합니다.  
  
    -   클릭 **찾아보기** 에 보고서 작성기의 기본 위치를 확인 하 고 업데이트 합니다.  
  
        > [!NOTE]  
        >  보고서 작성기의 기본 설치 폴더는 \<드라이브 > Program Files\Microsoft SQL Server입니다.  
  
    -   클릭 **디스크 공간** 자세한 디스크 공간 보고서 작성기를 사용 합니다.  
  
        > [!NOTE]  
        >  볼륨에 디스크 여유 공간이 충분하지 않은 경우 해당 볼륨이 강조 표시됩니다.  
  
7.  **기본 대상 서버** 페이지에서 필요 시 대상 보고서 서버의 URL을 제공합니다(기본값과 다른 경우). **다음**을 클릭합니다.  
  
    > [!NOTE]  
    >  보고서 서버에 연결되었을 때 보고서 작성기로 작업할 계획이라면 이 단계에서 서버의 URL을 제공하는 것이 좋습니다. 그러나 또한 가능에서이 **옵션** 보고서 작성기에서 작업할 때 대화 상자.  
  
8.  클릭 **설치** 의 보고서 작성기 설치를 완료 합니다.  
  
### <a name="to-install-report-builder-from-the-command-line"></a>명령줄에서 보고서 작성기를 설치하려면  
  
1.  로 이동 [Microsoft SQL Server 2012 보고서 작성기](https://go.microsoft.com/fwlink/?LinkID=219138) 보고서 작성기 섹션을 찾습니다.  
  
2.  클릭 **X86 패키지**합니다.  
  
3.  저장을 클릭합니다.  
  
4.  필요에 따라 확인 하려면 저장 위치로 이동 합니다 **다른 이름으로 저장** 옵션은 **Windows Installer 패키지**, 클릭 하 고 **저장**.  
  
5.  **시작** 메뉴에서 **실행**을 클릭합니다.  
  
6.  열려 있는 텍스트 상자에 입력 `cmd.`  
  
7.  명령 프롬프트 창에서 ReportBuilder3_x86.msi를 저장한 폴더로 이동합니다.  
  
8.  다음 형식으로 명령을 입력합니다.  
  
     `msiexec/i ReportBuilder3_.msi /option [value] [/option [value]]`  
  
     보고서 작성기를 설치할 때 특정 두 옵션은 RBINSTALLDIR과 REPORTSERVERURL입니다. 이러한 인수는 명령줄에 포함하지 않아도 됩니다. 기본 명령은 다음과 같습니다.  
  
     `msiexec /i ReportBuilder3_x86.msi /quiet`  
  
9. 명령을 실행하려면 Enter 키를 누릅니다.  
  
## <a name="see-also"></a>관련 항목  
 [설치, 제거 및 보고서 작성기 지원](../install-uninstall-and-report-builder-support.md)   
 [보고서 작성기의 독립 실행형 버전을 제거 &#40;보고서 작성기&#41;](install-report-builder.md)  
  
  
