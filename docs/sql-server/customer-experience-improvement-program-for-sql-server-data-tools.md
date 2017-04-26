---
title: "SQL Server Data Tools에 대한 사용자 환경 개선 프로그램 | Microsoft 문서"
ms.custom: 
ms.date: 10/21/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssdt
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: baf3a205-a6bb-4564-8b64-3a0475bb9273
caps.latest.revision: 11
author: stevestein
ms.author: sstein
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 7abf9d52d0e8fa4a4c6b16e479891db5f7e95529
ms.lasthandoff: 04/11/2017

---
# <a name="customer-experience-improvement-program-for-sql-server-data-tools"></a>SQL Server Data Tools에 대한 사용자 환경 개선 프로그램
  사용자 환경 개선 프로그램(CEIP)이 어떻게 Microsoft가 소프트웨어 개선 방법을 식별하는 데 도움이 되는지 알아 보세요.  언제든지 참여하거나 참여하지 않도록 도구를 구성할 수 있습니다.  
  
> [!NOTE]  
>  Microsoft SQL Server 2016 릴리스, 기타 제품 및 서비스에 대한 사용자 데이터 수집 및 사용 방법에 대한 설명은 이 [Microsoft 개인 정보 취급 방침](https://www.microsoft.com/privacystatement/en-us/SQLServer/Default.aspx)을 참조하세요.  
  
## <a name="opting-in-and-out-of-ceip-for-sql-server-data-tools"></a>SQL Server Data Tools에 대한 CEIP 참여 및 참여 거부  
 사용자 환경 개선 프로그램은 Microsoft가 시간에 따라 제품을 개선하는 데 도움이 되도록 설계된 프로그램입니다. 이 프로그램은 컴퓨터 하드웨어에 대한 정보는 물론, 컴퓨터 작업 수행 시 사용자를 방해하지 않고 사용자의 제품 사용 방식을 수집합니다. 수집된 정보를 통해 Microsoft는 개선할 기능을 식별할 수 있습니다. 이 문서에서는 Visual Studio 2015와 Visual Studio 2013 모두에 대한 SQL Server Data Tools(SSDT)의 CEIP에 참여 또는 참여 거부하는 방법을 다룰 것입니다.  
  
### <a name="choice-and-control-over--ceip-and-sql-server-data-tools-for-visual-studio-2015"></a>Visual Studio 2015용 SQL Server Data Tools와 CEIP에 대한 선택과 제어  
 Visual Studio 2015용 SSDT는 SQL Server 2016와 함께 제공되는 데이터 모델링 도구로서, Visual Studio 2015에 내장되어 있는 CEIP 옵션을 사용합니다. 이 [Visual Studio 도움말 문서](http://go.microsoft.com/fwlink/?LinkId=517102)에서 Visual Studio 2015의 CEIP를 통해 사용자 의견을 제출하는 방법에 대해 알 수 있습니다.  
  
 SQL Server 2016 미리 보기 버전의 경우 CEIP가 기본적으로 사용 설정되어 있습니다. 아래 지침에 따라 사용 해제하거나 다시 설정할 수 있습니다.  
  
 **Visual Studio(Visual Studio 2015의 전체 언어 설치에 해당)**  
  
 이미 Visual Studio가 있는 컴퓨터에서 SSDT 설치를 실행할 경우 SQL Server 및 비즈니스 인텔리전스 프로젝트 템플릿만 추가됩니다. 이 시나리오에서는 Visual Studio에서 제공하는 사용자 의견 옵션을 사용하여 CEIP에 참여 또는 참여하지 않을 수 있습니다.  
  
1.  Visual Studio를 시작합니다.  
  
2.  도움말 메뉴에서 **사용자 의견 보내기** > **설정**을 선택합니다.  
  
3.  CEIP를 해제하려면 **아니요, 참여하지 않습니다.**를 클릭한 후 **확인**을 클릭합니다.  
  
     CEIP를 설정하려면 **예, 참여하겠습니다.**를 클릭한 후 **확인**을 클릭합니다.  
  

  
 **레지스트리 기반 정책 또는 그룹 정책 사용**  
  
 Visual Studio 2015가 없는 컴퓨터에 SSDT 설치 프로그램을 실행하는 경우 Visual Studio Shell만 설치됩니다. 셸은 사용자 의견 옵션을 제공하지 않습니다. 이 경우에 레지스트리 업데이트는 CEIP를 구성하기 위한 유일한 옵션입니다.  
  
 기업 고객은 그룹 정책을 생성하여 SQL Server 2016에 대한 레지스트리 기반 정책을 설정함으로써 CEIP에 참여하거나 참여하지 않을 수 있습니다.  
  
 관련 레지스트리 키와 설정은 다음과 같습니다.  
  
 키 = HKEY_CURRENT_USER\Software\Microsoft\VSCommon\14.0\SQM  
  
 RegEntry name = OptIn  
  
 항목 종류 DWORD:  
  
-   0은 참여하지 않음  
  
-   1은 참여함  
  
> [!CAUTION]  
>  레지스트리를 잘못 편집하면 시스템이 심각하게 손상될 수 있습니다. 따라서 레지스트리를 변경하기 전에 컴퓨터의 중요한 데이터를 백업해 두어야 합니다. 변경 내용을 수동으로 적용한 후 문제가 발생할 경우 마지막으로 성공한 구성 시작 옵션을 사용할 수도 있습니다.  
  
 CEIP에서 수집, 처리 또는 전송되는 정보에 대한 자세한 내용은 [Microsoft 사용자 환경 개선 프로그램에 대한 개인 정보 취급 방침](http://go.microsoft.com/fwlink/?LinkId=52143)을 참조하세요.  
  
### <a name="choice-and-control-for-ceip-and-sql-server-data-tools---bi-ssdt-bi"></a>SQL Server Data Tools - BI(SSDT-BI) 및 CEIP에 대한 선택과 제어  
 SSDT-BI를 사용하고 있는 경우 설치 중 CEIP에 참여하도록 선택할 수 있습니다. 나중에 SSDT-BI에 대한 구성은 클라이언트 도구를 통해 또는 레지스트리 설정을 편집하여 변경할 수 있습니다.  
  
 **Visual studio 2013용 SSDT 및 SSDT-BI**  
  
1.  도구를 시작하고 Analysis Services 또는 Integration Services에 대한 새 또는 기존 프로젝트를 엽니다.  
  
2.  도움말 메뉴에서 **Microsoft SQL Server 사용자 의견 옵션**을 선택합니다.  
  
3.  CEIP를 해제하려면 **아니요, 참여하지 않겠습니다**를 클릭합니다.  
  
     CEIP를 설정하려면 **예, 참여하겠습니다**를 클릭합니다.  
  
4.  **확인**을 클릭합니다.  
  
 **레지스트리 기반 정책 또는 그룹 정책 사용**  
  
 기업 고객은 그룹 정책을 생성하여 SQL Server 2014에 대한 레지스트리 기반 정책을 설정함으로써 참여하거나 참여하지 않을 수 있습니다.  
  
 관련 레지스트리 키와 설정은 다음과 같습니다.  
  
 키 = HKEY_CURRENT_USER\Software\Microsoft\Microsoft SQL Server\120  
  
 레지스트리 항목 이름 = CustomerFeedback  
  
 항목 종류 DWORD:  
  
-   0은 참여하지 않음  
  
-   1은 참여함  
  
  

