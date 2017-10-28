---
title: "등록된 서버 F1 도움말 | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- SQL Server Management Studio [SQL Server], Help
- Registered Servers [SQL Server], help
- SQL Server Management Studio Help [SQL Server], registered servers
ms.assetid: 59f76b28-ba78-4a1a-b5d5-8b581f30114d
caps.latest.revision: 23
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 5db067d5a2fe5bbf9953484c9a999ed7b1fcddae
ms.openlocfilehash: df1eb91bc84f39d0e2277731d5329d79b8c43e78
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="registered-servers-f1-help"></a>등록된 서버 F1 도움말
  이 섹션에서는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]의 등록된 서버 구성 요소에 대한 F1 도움말을 제공합니다. 다양한 옵션에 대해 설명합니다.
  
 등록된 서버에 대해 알아보고 서버에서 수행할 작업에 대한 링크를 확인하려면 [서버 등록](../../tools/sql-server-management-studio/register-servers.md) 항목으로 이동합니다. 
 

 등록된 서버 설정을 저장하려면 클릭합니다. 
 
 ## <a name="reporting-services-new-or-edit-server-registration-general-tab"></a>Reporting Services 새 서버 등록 또는 서버 등록 편집(일반 탭) 
  이 탭을 사용하여 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]인스턴스의 등록 옵션을 지정할 수 있습니다.  
  
 이 페이지에 액세스하려면 등록된 서버에서 **등록된 서버** 도구 모음의 **Reporting Services** 를 클릭하고 **Reporting Services**와 같은 등록된 서버 그룹을 마우스 오른쪽 단추로 클릭한 다음 **새로 만들기**를 가리키고 **서버 등록**을 클릭합니다.  
  
### <a name="options"></a>옵션  
 **서버 유형**  
 등록된 서버에서 서버를 등록하는 경우 **서버 유형** 상자는 읽기 전용이며 **등록된 서버** 창에 표시된 서버 유형과 일치합니다. 다른 유형의 서버를 등록하려면 새 서버를 등록하기 전에 **등록된 서버** 도구 모음에서 원하는 서버를 클릭합니다.  
  
 **서버 이름**  
 연결할 보고서 서버 인스턴스를 지정합니다. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에서는 해당 인스턴스 이름을 통해 보고서 서버에 액세스할 수 있습니다. 설치하는 각 SQL Server 인스턴스에 대해 하나의 보고서 서버 인스턴스를 만들 수 있습니다. 기본 인스턴스를 사용하는 경우에는 SQL Server 인스턴스의 이름을 입력합니다. 명명된 인스턴스를 사용하는 경우에는 MSSQL$InstanceName 형식으로 보고서 서버에 연결할 명명된 인스턴스를 지정합니다.  
  
 **인증**  
 보고서 서버에 대한 인증은 인터넷 정보 서비스(IIS)를 통해 수행됩니다. Reporting Services에 연결할 때는 다음 인증 모드 중 하나를 선택합니다.  
  
 **Windows 인증 모드(Windows 인증)**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 자격 증명을 사용하여 보고서 서버 인스턴스에 연결합니다.  
  
 **기본 인증**  
 Reporting Services 설치에서 기본 인증을 사용하도록 구성되어 있는 경우 **기본 인증** 을 사용하여 연결합니다.  
  
 **폼 인증**  
 Reporting Services 설치에서 사용자 지정 인증 확장 프로그램을 사용하도록 구성되어 있는 경우 **폼 인증** 을 사용하여 연결합니다.  
  
 **사용자 이름**  
 연결에 사용할 로그인 이름을 입력합니다. 이 옵션은 **기본 인증** 또는 **폼 인증**을 선택한 경우에만 사용할 수 있습니다.  
  
 **암호**  
 사용자 이름에 대한 암호를 입력합니다. 이 옵션은 **기본 인증** 또는 **폼 인증**을 선택한 경우에만 편집할 수 있습니다.  
  
 **암호 저장**  
 입력한 암호를 저장합니다. 이 옵션은 **기본 인증** 또는 **폼 인증**을 클릭한 경우에만 사용할 수 있습니다.  
  
> **참고:** 저장한 암호를 더 이상 저장하지 않으려면 이 확인란의 선택을 취소하고 **저장**을 클릭합니다.  
  
 **등록된 서버 이름**  
 등록된 서버에 표시할 이름입니다. 이 이름은 **서버 이름** 상자에 있는 이름과 일치할 필요가 없습니다.  
  
 **등록된 서버 설명**  
 서버에 대한 선택적 설명을 입력합니다.  
  
 **테스트**  
 **서버 이름**에서 선택한 서버 연결을 테스트하려면 클릭합니다.  
  
 
 ## <a name="analysis-services---multidimensional-data-new-or-edit-server-registration-general-tab"></a>Analysis Services - 다차원 데이터 새 서버 등록 또는 서버 등록 편집(일반 탭)
 
  이 탭을 사용하여 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]인스턴스의 등록 옵션을 지정할 수 있습니다.  
  
 이 페이지에 액세스하려면 등록된 서버 도구 모음에서 **Analysis Services** 를 클릭하고 **Analysis Services**와 같은 등록된 서버 그룹을 마우스 오른쪽 단추로 클릭한 다음 **새로 만들기**를 가리키고 **서버 등록**을 클릭합니다.  
  
### <a name="options"></a>옵션  
 **서버 유형**  
 등록된 서버에서 서버를 등록하는 경우 **서버 유형** 상자는 읽기 전용이며 등록된 서버 창에 표시된 서버 유형과 일치합니다. 다른 유형의 서버를 등록하려면 새 서버를 등록하기 전에 **등록된 서버** 도구 모음에서 원하는 서버를 클릭합니다.  
  
 **서버 이름**  
 연결할 서버 인스턴스를 선택합니다. 마지막으로 연결한 서버 인스턴스가 기본적으로 표시됩니다.  
  
 **인증**  
 Windows 인증을 사용하는 경우 사용자가 자신의 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 자격 증명을 사용하거나 Windows 사용자 또는 Windows 그룹의 멤버로 연결할 수 있습니다.  
  
 **User name**  
 이 릴리스에서는 이 옵션을 사용할 수 없습니다.  
  
 **암호**  
 이 릴리스에서는 이 옵션을 사용할 수 없습니다.  
  
 **암호 저장**  
 이 릴리스에서는 이 옵션을 사용할 수 없습니다.  
  
 **등록된 서버 이름**  
 등록된 서버에 표시할 이름입니다. 이 이름은 **서버 이름** 상자와 일치할 필요가 없습니다.  
  
 **등록된 서버 설명**  
 서버에 대한 선택적 설명을 입력합니다.  
  
 **테스트**  
 **서버 이름**에서 선택한 서버 연결을 테스트하려면 클릭합니다. 
 
 ## <a name="ssis-new-or-edit-server-registration-general-tab"></a>SSIS 새 서버 등록 또는 서버 등록 편집(일반 탭) 
 
 이 탭을 사용하여 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]등록 옵션을 지정할 수 있습니다.  
  
 이 페이지에 액세스하려면 등록된 서버의 **등록된 서버** 도구 모음에서 **Integration Services** 를 클릭하고 등록된 서버 그룹을 마우스 오른쪽 단추로 클릭한 다음 **새로 만들기**를 가리키고 **서버 등록**을 클릭합니다.  
  
### <a name="options"></a>옵션  
 **서버 유형**  
 등록된 서버에서 서버를 등록하는 경우 **서버 유형** 상자는 읽기 전용이며 등록된 서버에 표시된 서버 유형과 일치합니다. 다른 유형의 서버를 등록하려면 새 서버를 등록하기 전에 **등록된 서버**, **데이터베이스 엔진**, **데이터베이스 엔진**, **Analysis Server** **SQL Server Compact** **등록된 서버** 도구 모음에서 **Integration Services** 를 클릭합니다.  
  
 **서버 이름**  
 연결할 서버를 선택합니다. 기본적으로 마지막으로 연결한 서버가 표시됩니다.  
  
 **인증**  
 Windows 인증 모드를 사용하면 사용자는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 사용자 계정을 통해 연결할 수 있습니다.  
  
 **User name**  
 이 릴리스에서는 이 옵션을 사용할 수 없습니다.  
  
 **암호**  
 이 릴리스에서는 이 옵션을 사용할 수 없습니다.  
  
 **암호 저장**  
 이 릴리스에서는 이 옵션을 사용할 수 없습니다.  
  
 **등록된 서버 이름**  
 **등록된 서버**에 표시할 이름입니다. 이 이름은 **서버 이름** 상자와 일치할 필요가 없습니다.  
  
 **등록된 서버 설명**  
 서버에 대한 선택적 설명을 입력합니다.  
  
 **테스트**  
 **서버 이름**에서 선택한 서버 연결을 테스트하려면 클릭합니다. 
  

 
 
  

