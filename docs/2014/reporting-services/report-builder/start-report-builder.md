---
title: 시작 보고서 작성기 (보고서 작성기) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Report Builder, launching
- launching Report Builder
- SharePoint integration [Reporting Services], starting Report Builder
- starting Report Builder
ms.assetid: 8c8c7d2e-b315-418d-bf65-90e7685e4259
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 6fc123be862320cd35ccf4aec76d8bc9cf7877af
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66107597"
---
# <a name="start-report-builder-report-builder"></a>보고서 작성기 시작(보고서 작성기)
  [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)]에는 독립 실행형 및 [!INCLUDE[ndptecclick](../../includes/ndptecclick-md.md)] 버전의 보고서 작성기 포함 되어 있습니다. 
  [!INCLUDE[ndptecclick](../../includes/ndptecclick-md.md)] 버전은 기본 모드 또는 SharePoint 통합 모드로 설치된 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에서 사용할 수 있습니다.  
  
> [!NOTE]  
>  보고서 작성기는 Itanium 64 기반 컴퓨터에 설치할 수 없습니다. 이는 보고서 작성기의 [!INCLUDE[ndptecclick](../../includes/ndptecclick-md.md)] 및 독립 실행형 버전에 적용됩니다.  
  
 이때 열리는 보고서 작성기 [!INCLUDE[ndptecclick](../../includes/ndptecclick-md.md)] 버전이 이전 버전의 보고서 작성기이면 보고서 작성기 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 버전을 사용하도록 보고서 관리자와 SharePoint 사이트를 업데이트해 줄 것을 관리자에게 요청하십시오.  
  
 보고서 작성기 [!INCLUDE[ndptecclick](../../includes/ndptecclick-md.md)] 버전을 사용하여 SharePoint에 게시된 [!INCLUDE[ssGeminiClient](../../includes/ssgeminiclient-md.md)] 통합 문서에 대한 보고서를 만들 수도 있습니다. 에서 보고서 작성기를 사용 하는 방법 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]에 대 한 자세한 내용은 Technet.microsoft.com에서 [PowerPivot 데이터를 사용 하 여 Reporting Services 보고서 만들기](https://go.microsoft.com/fwlink/?LinkId=185238) 를 참조 하세요.  
  
 로컬 컴퓨터의 **시작** 메뉴에서 독립 실행형 보고서 작성기를 시작 하려면 도구를 사용할 수 있도록 사용자 또는 관리자가 컴퓨터에 직접 보고서 작성기를 설치 해야 합니다. 독립 실행형 버전은 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]를 설치할 때 함께 설치되지 않습니다. 별도로 다운로드하여 설치해야 합니다. 보고서 작성기를 다운로드 하려면 [Microsoft® SQL Server® 2012 보고서 작성기](https://go.microsoft.com/fwlink/?LinkId=401502)을 참조 하세요.  
  
### <a name="to-start-report-builder-clickonce-from-report-manager"></a>보고서 관리자에서 보고서 작성기 ClickOnce를 시작하려면  
  
1.  웹 브라우저의 주소 표시줄에 보고서 서버의 URL을 입력합니다. 기본적으로 URL은 http://\<*servername*>/reports입니다. 보고서 관리자가 열립니다.  
  
2.  
  **보고서 작성기**를 클릭합니다.  
  
     보고서 작성기가 열립니다. 이제 보고서를 작성하거나 보고서 서버의 보고서를 열 수 있습니다.  
  
### <a name="to-start-report-builder-clickonce-using-a-url"></a>URL을 사용하여 보고서 작성기 ClickOnce를 시작하려면  
  
1.  웹 브라우저의 주소 표시줄에 다음 URL을 입력합니다.  
  
     http://\<servername>/reportserver/reportbuilder/ReportBuilder_3_0_0_0. 응용 프로그램  
  
2.  Enter 키를 누릅니다.  
  
     보고서 작성기가 열립니다. 이제 보고서를 작성하거나 보고서 서버의 보고서를 열 수 있습니다.  
  
### <a name="to-start-report-builder-clickonce-in-sharepoint-integrated-mode"></a>SharePoint 통합 모드에서 보고서 작성기 ClickOnce를 시작하려면  
  
1.  원하는 라이브러리가 있는 SharePoint 사이트로 이동합니다.  
  
2.  라이브러리를 엽니다.  
  
3.  
  **문서**를 클릭합니다.  
  
4.  
  **새 문서** 메뉴에서 **보고서 작성기 보고서**를 클릭합니다.  
  
     보고서 작성기가 열립니다. 이제 보고서를 작성하거나 보고서 서버의 보고서를 열 수 있습니다.  
  
     **참고** **새 문서** 메뉴에 **보고서 작성기 보고서**, **보고서 작성기 모델**및 **보고서 데이터 원본** 옵션이 나열 되지 않는 경우 해당 콘텐츠 형식을 SharePoint 라이브러리에 추가 해야 합니다. 자세한 내용은 msdn.microsoft.com의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [온라인 설명서](https://go.microsoft.com/fwlink/?LinkId=154888) 에서 [SharePoint 통합 모드&#41;Reporting Services &#40;라이브러리에 보고서 서버 콘텐츠 형식 추가](../add-reporting-services-content-types-to-a-sharepoint-library.md) 를 참조 하세요.  
  
### <a name="to-start-report-builder-stand-alone-from-the-start-menu"></a>시작 메뉴에서 보고서 작성기 독립 실행형 버전을 시작하려면  
  
1.  시작 메뉴에서 **모든 프로그램**을 클릭 한 다음 [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)] **보고서 작성기**를 클릭 합니다.  
  
2.  
  **보고서 작성기** 를 클릭합니다.  
  
     보고서 작성기가 열립니다. 이제 보고서를 작성하거나 열 수 있습니다.  
  
3.  새 보고서를 만들려면 보고서 작성기의 왼쪽 위 모서리에서 SQL Server 아이콘을 클릭한 다음 새로 만들기를 클릭합니다.  
  
4.  로컬 컴퓨터 또는 보고서 서버에 저장된 기존 보고서를 열려면 왼쪽 위 모서리에서 SQL Server 아이콘을 클릭한 다음 열기를 클릭합니다.  
  
     기존 서버 목록에 보고서 서버가 표시 되지 않는 경우 **보고서 열기** 대화 상자를 닫은 다음 보고서 작성기 아래쪽에 있는 **연결** 을 클릭 하 여 서버에 연결 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 2014의 보고서 작성기](report-builder-in-sql-server-2016.md)  
  
  
