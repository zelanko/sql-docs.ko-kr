---
title: 설치, 제거 및 보고서 작성기 지원 | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- administering Report Builder
ms.assetid: 2c9a5814-17bf-4947-8fb3-6269e7caa416
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 8d3f7e5829c19b79ca19783d36885f6bfd3761f7
ms.sourcegitcommit: baa40306cada09e480b4c5ddb44ee8524307a2ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/06/2019
ms.locfileid: "73637882"
---
# <a name="install-uninstall-and-report-builder-support"></a>설치, 제거 및 보고서 작성기 지원
  보고서 작성기는 보고서, 보고서 파트 및 공유 데이터 세트를 만들고 업데이트하고 공유하는 데 사용하는 보고서 작성 도구입니다. 보고서 작성기는 독립 실행형 버전 및 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]버전으로 사용할 수 있습니다. 독립 실행형 버전은 사용자나 관리자가 컴퓨터에 설치합니다. [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 버전은 자동으로 [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)] 와 함께 설치되고 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]와 통합된 SharePoint 사이트나 보고서 관리자에서 컴퓨터로 다운로드됩니다.  
  
 보고서 작성기의 독립 실행형 버전은 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]와 함께 설치되지 않습니다. [Microsoft® SQL Server® 2012 보고서 작성기](https://go.microsoft.com/fwlink/?LinkId=401502)에서 별도로 다운로드하고 설치해야 합니다.  
  
> [!NOTE]  
>  보고서 작성기는 Itanium 기반 컴퓨터에 설치할 수 없습니다. 이는 보고서 작성기의 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 및 독립 실행형 버전에 적용됩니다.  
  
 일반적으로 관리자는 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]를 설치 및 구성하고 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 버전의 보고서 작성기를 사용할 수 있는 권한을 부여하며 보고서 서버에 저장된 보고서, 보고서 파트 및 공유 데이터 세트에 대한 폴더와 사용 권한을 관리합니다. [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 관리에 대 한 자세한 내용은 msdn.microsoft.com의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [온라인 설명서](https://go.microsoft.com/fwlink/?LinkId=154888) 에서 [보고서 서버 &#40;&#41; 기본 모드 Reporting Services](report-server/reporting-services-report-server-native-mode.md) 를 참조 하세요.  
  
##  <a name="Installing"></a>보고서 작성기 설치  
 보고서 작성기는 독립 실행형 버전 및 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 버전으로 사용할 수 있습니다. 독립 실행형 버전은 사용자나 관리자가 컴퓨터에 다운로드하여 설치하지만 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 버전은 [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)]와 함께 설치됩니다. [Microsoft 다운로드 센터](https://www.microsoft.com/download/details.aspx?id=53613)에서 보고서 작성기를 다운로드할 수 있습니다.  
  
> [!NOTE]  
>  보고서 작성기는 Itanium 64 기반 컴퓨터에 설치할 수 없습니다. 이는 보고서 작성기의 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 및 독립 실행형 버전에 적용됩니다.  
  
 두 버전 중 하나의 보고서 작성기를 설치하기 전에 시스템 요구 사항을 확인하고 모든 필수 구성 요소를 설치합니다.  
  
### <a name="system-requirements"></a>시스템 요구 사항  
 보고서 작성기를 설치하려면 로컬 컴퓨터에 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 버전 3.5가 설치되어 있어야 합니다. 보고서 작성기를 설치하려고 할 때 로컬 컴퓨터에 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 가 설치되어 있지 않은 경우 설치를 계속하여 완료하기 전에 이를 설치하라는 메시지가 표시됩니다.  
  
 .NET Framework 3.5는 [Microsoft 다운로드 센터](https://www.microsoft.com/download/details.aspx?id=21)에서 .NET Framework 3.5를 다운로드할 수 있습니다.  
  
 보고서 작성기는 [!INCLUDE[msCoName](../includes/msconame-md.md)] 3.5를 지원하는 모든 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] Windows 운영 체제에 설치할 수 있습니다. 예를 들어 Windows Vista 또는 Windows 7에 보고서 작성기를 설치할 수 있습니다.  
  
 보고서 작성기를 실행할 컴퓨터에는 512MB 이상의 RAM이 권장됩니다. 하지만 실행하는 보고서의 복잡성에 따라 더 많거나 적은 RAM이 필요할 수 있습니다.  
  
### <a name="installing-the-stand-alone-version-of-report-builder-directly-on-your-computer"></a>컴퓨터에 보고서 작성기의 독립 실행형 버전을 직접 설치  
 사용자가 다운로드 사이트인 [Microsoft 다운로드 센터](https://www.microsoft.com/download/details.aspx?id=53613)에서 보고서 작성기를 설치하거나 관리자가 사용자가 설치할 수 있는 공유에 보고서 작성기의 Windows Installer 패키지인 ReportBuilder3.msi 파일을 사용 가능하게 할 수 있습니다.  
  
 또한 명령줄 설치를 수행할 수 있고 자동 설치, 설치 로그 파일 작성 등의 옵션을 포함할 수 있습니다. .msi 파일을 실행하는 Windows Installer의 설명서에서 사용 가능한 옵션에 대한 정보를 확인할 수 있습니다.  
  
 자세한 내용은 [보고서 작성기 &#40;보고서 작성기&#41;독립 실행형 버전 설치](install-windows/install-report-builder.md)를 참조 하세요.  
  
 또한 관리자는 Microsoft Systems Manager Server(SMS)와 같은 소프트웨어를 사용하여 프로그램을 사용자의 컴퓨터에 배포할 수 있습니다. 특정 소프트웨어를 사용하여 보고서 작성기를 설치하는 방법을 확인하려면 해당 소프트웨어의 설명서를 참조하십시오.   
  
### <a name="installing-the-clickonce-version-of-report-builder-on-your-computer"></a>컴퓨터에 보고서 작성기의 ClickOnce 버전 설치  
 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 버전의 보고서 작성기는 [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)]와 함께 설치됩니다. 이 버전은 [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)]의 기본 설치 및 SharePoint 통합 설치 둘 다에서 설치됩니다.  
  
 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]는 Windows 애플리케이션을 배포하는 Microsoft 기술입니다. [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]에서는 사용자가 웹 페이지에서 링크를 클릭하여 보고서 작성기와 같은 Windows 애플리케이션을 설치하고 실행할 수 있습니다. 응용 프로그램을 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 배포 하거나, 응용 프로그램 보안을 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 적용 하거나, 인터넷 영역에서 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 응용 프로그램을 실행 하는 방법에 대 한 자세한 내용은 "Windows Forms 응용 프로그램에 대 한 ClickOnce 배포", "Windows Forms의 보안 개요를 참조 하십시오. "또는 [!INCLUDE[msCoName](../includes/msconame-md.md)] Developer Network 웹 사이트의" 신뢰할 수 있는 응용 프로그램 배포 개요 "문서 [https://developer.microsoft.com/](https://developer.microsoft.com/).  
  
 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 버전의 보고서 작성기는 보고서 서버에 있으며 보고서 관리자에서 **보고서 작성기** 단추를 클릭하거나 SharePoint 라이브러리의 **새 문서** 메뉴에서 **보고서 작성기 보고서** 옵션을 클릭할 때 컴퓨터에 설치됩니다.  
  
> [!NOTE]  
>  **새 문서** 메뉴에 **보고서 작성기 보고서**, **보고서 작성기 모델**및 **보고서 데이터 원본** 옵션이 나열되지 않은 경우 해당 콘텐츠 형식을 SharePoint 라이브러리에 추가해야 합니다.   
  
 보고서 작성기는 보고서 관리자나 SharePoint 라이브러리에서 열 수 있습니다. 보고서 작성기 열기에 대 한 자세한 내용은 [Start 보고서 작성기 &#40;보고서 작성기&#41;](report-builder/start-report-builder.md)를 참조 하세요.  
  
### <a name="report-builder-languages"></a>보고서 작성기 언어  
 보고서 작성기는 영어 외에 21개 언어를 지원합니다. 보고서 작성기의 독립 실행형 버전을 다운로드할 때 설치할 언어 버전을 선택합니다. 사용할 각 언어 버전을 개별적으로 다운로드해야 합니다.  
  
 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 버전의 경우 [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)]를 설치할 때 모든 언어 버전이 보고서 서버에 설치됩니다. 사용자 컴퓨터의 culture에 따라 컴퓨터에 설치될 언어 버전이 결정됩니다. culture에 일치하는 보고서 작성기 언어가 없는 경우 영어 버전이 설치됩니다.  
  
 다음 표에서는 사용할 수 있는 언어 버전에 대한 정보를 보여 줍니다.  
  
|LCID|언어|Culture|  
|----------|--------------|-------------|  
|1028|중국어(번체)|zh-TW|  
|1029|체코어|cs-CZ|  
|1030|덴마크어|da-DK|  
|1031|독일어|de-DE|  
|1032|그리스어|el-GR|  
|1033|영어|ko-KR|  
|1035|핀란드어|fi-FI|  
|1036|프랑스어|fr-FR|  
|1038|헝가리어|hu-HU|  
|1040|이탈리아어|it-IT|  
|1041|일본어|ja-JP|  
|1042|한국어|ko-KR|  
|1043|네덜란드어|nl-NL|  
|1044|노르웨이어(복말)|nb-NO|  
|1045|폴란드어|pl-PLl|  
|1046|포르투갈어(브라질)|pt-BR|  
|1049|러시아어|ru-RU|  
|1053|스웨덴어|sv-SE|  
|1055|터키어|tr-TR|  
|2052|중국어(간체)|zh-CN|  
|2070|포르투갈어(포르투갈)|pt-PT|  
|3082|스페인어(스페인)|es-ES|  
  
  
##  <a name="Uninstalling"></a>보고서 작성기 제거  
 제어판 또는 명령줄에서 독립 실행형 버전의 보고서 작성기를 제거할 수 있습니다. 이는 보고서 작성기의 독립 실행형 버전에만 적용됩니다. 보고서 작성기의 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 는 별도로 제거할 수 없으며, 항상 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]와 함께 설치되고 제거됩니다.  
  
 자세한 내용은 [보고서 작성기 &#40;보고서 작성기&#41;독립 실행형 버전 제거](install-windows/uninstall-report-builder.md)를 참조 하세요.  
  
  
##  <a name="Supporting"></a>지원 보고서 작성기  
 보고서 작성자를 지원하기 위해 관리자는 보고서 서버에서 폴더, 보고서 및 보고서 관련 항목을 관리하고 보고서 서버의 리소스에 대한 사용 권한을 부여하며 액세스를 위해 보고서 서버를 구성할 책임이 있습니다.  
  
### <a name="folders-reports-and-report-related-items"></a>폴더, 보고서 및 보고서 관련 항목  
 보고서 서버에서 다음 폴더, 보고서 및 보고서 관련 항목이 관리됩니다.  
  
-   보고서, 공유 데이터 원본, 모델 등을 저장하는 폴더  
  
-   사용자의 보고서 및 보고서 관련 항목을 저장하는 프라이빗 폴더인 내 보고서  
  
-   보고서 외부에 저장된 데이터 원본을 보고서 작성자가 사용할 수 있게 하는 공유 데이터 원본  
  
-   여러 사용자의 여러 보고서에 대한 즉시 사용 가능한 쿼리된 데이터를 제공할 수 있는 공유 데이터 세트.  
  
-   공동 작업 환경에서 다른 사용자가 만든 보고서의 일부를 사용자가 향상시키거나 다시 사용할 수 있게 하는 테이블 및 차트와 같은 보고서 파트  
  
-   복잡한 데이터 원본에서 보고서의 데이터를 더 쉽고 간단하게 가져올 수 있게 하는 보고서 모델  
  
-   여러 보고서에서 사용할 수 있으며 쉬운 유지 관리를 위해 보고서 외부에 저장되는 배경 이미지 및 로고와 같은 이미지  
  
 자세한 내용은 msdn.microsoft.com의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [온라인 설명서](https://go.microsoft.com/fwlink/?LinkId=154888) 에서 [보고서 &#40;서버 콘텐츠 관리&#41; SSRS 기본 모드](report-server/report-server-content-management-ssrs-native-mode.md) 를 참조 하세요.  
  
### <a name="permissions"></a>사용 권한  
 관리자는 보고서 서버에 대한 사용 권한을 부여합니다. 보고서 작성기 사용자는 보고서 서버에 대한 사용 권한이 있어야만 보고서 서버의 내용 및 기능에 액세스할 수 있습니다. 예를 들어 사용자는 보고서 서버에 저장된 보고서 파트를 사용하고 보고서를 업데이트하여 보고서 서버에 다시 저장하며 보고서 관리자에서 보고서를 실행해야 할 수 있습니다. 요구 사항과 수행하는 태스크에 따라 더 낮거나 높은 사용 권한이 부여될 수 있습니다. 예를 들어 공유 보고서를 열기만 하면 되는 사용자에게는 공유 보고서를 수정해야 하는 사용자보다 권한이 낮은 사용 권한이 부여됩니다.  
  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 가 기본 모드로 설치되어 있을 경우 관리자는 다음을 수행할 수 있습니다.  
  
-   내 보고서 기능을 설정하여 고유의 보고서를 만들고 저장하는 데 사용할 수 있는 프라이빗 폴더를 사용자에게 제공합니다.  
  
-   퍼블릭 폴더에서 보고서 작성기 역할을 사용하여 사용자가 공유 보고서의 복사본을 연 다음 수정된 버전을 프라이빗 폴더에 저장할 수 있도록 합니다.  
  
-   게시자 역할을 사용하여 사용자가 공용 폴더의 보고서 및 공유 데이터 원본을 관리할 수 있도록 합니다. 이 역할은 경험이 많은 사용자에게 부여됩니다.  
  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 가 SharePoint 통합 모드로 설치되어 있을 경우 관리자는 다음을 수행할 수 있습니다.  
  
-   기본적으로 방문자 그룹에 부여되는 읽기 권한 수준을 사용하여 사용자가 퍼블릭 폴더의 보고서 복사본을 연 다음 수정된 버전의 보고서를 프라이빗 폴더나 컴퓨터에 저장할 수 있도록 합니다.  
  
-   기본적으로 멤버 그룹에 부여되는 참가 권한 수준을 사용하여 사용자가 공용 폴더의 보고서 및 공유 데이터 원본을 관리할 수 있도록 합니다. 이 권한 수준은 경험이 많은 사용자에게 부여됩니다.  
  
 사용 권한 및 역할을 만들고 사용하는 방법에 대한 일반적인 내용은 msdn.microsoft.com의 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 온라인 설명서 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [에서](https://go.microsoft.com/fwlink/?LinkId=154888) 를 참조하십시오.  
  
### <a name="configuration-of-report-server"></a>보고서 서버 구성  
 보고서 작성기에서 보고서를 작성하고 Windows Vista, Windows Server 2008 또는 Windows 7에 설치된 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스에 연결하는 경우 보고서를 열거나 저장하기 위해 보고서 서버에 액세스할 때 액세스 거부 오류가 발생할 수 있습니다. 이러한 오류는 Windows Vista, Windows Server 2008 및 Windows 7의 보안 기능인 UAC(사용자 계정 컨트롤)가 애플리케이션에 액세스할 때 관리자 권한을 제거하여 승격된 권한이 남용되지 않도록 제한하기 때문입니다.  
  
 하지만 추가 구성을 통해 보고서 작성기 사용자가 보고서 서버를 사용할 수 있습니다. [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] URL을 신뢰할 수 있는 사이트에 추가할 수 있습니다. 기본적으로 Windows Vista, Windows Server 2008 및 Windows 7에서 Internet Explorer 7.0 이상은 보호 모드로 실행됩니다. 보호 모드는 같은 컴퓨터에서 실행되는 높은 수준의 프로세스에 브라우저 요청이 도달하지 못하도록 차단하는 기능입니다. 이 URL을 신뢰할 수 있는 사이트에 추가하면 보고서 서버 애플리케이션에 대한 보호 모드를 해제할 수 있습니다. 이 변경을 수행하려면 관리자 권한이 있어야 합니다.  
  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]를 구성 하는 방법에 대 한 자세한 내용은 msdn.microsoft.com의 [Reporting Services 설명서](https://go.microsoft.com/fwlink/?linkid=121312) 에서 [Reporting Services 구성 관리자 &#40;del&#41; ](https://docs.microsoft.com/sql/sql-server/install/reporting-services-configuration-manager-native-mode) 을 참조 하십시오.  
  
  
##  <a name="SampleDatabases"></a>예제 데이터베이스 SQL Server  
 예제 데이터베이스의 Adventure Works 제품군은 보고서 작성에 대해 배우고 예제 보고서를 작성하는 데 사용할 수 있는 데이터를 제공합니다.  
  
 다음 버전의 데이터베이스를 사용할 수 있습니다.  
  
-   Adventure Works OLTP 데이터베이스는 가상의 자전거 제조업체(Adventure Works Cycles)에 대한 표준 온라인 트랜잭션 처리 시나리오를 지원합니다. 시나리오에는 제조, 판매, 구매, 제품 관리, 연락처 관리, 인사 등이 포함됩니다.  
  
-   [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] 데이터베이스는 데이터 웨어하우스를 작성하는 방법을 보여 줍니다.  
  
-   [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)] 프로젝트를 사용하여 비즈니스 인텔리전스 시나리오를 위한 AS 데이터베이스를 작성할 수 있습니다.  
  
 예제 데이터베이스는 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 에 포함되어 있지 않으며 [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)] 또는 독립 실행형 버전의 보고서 작성기를 설치할 때 설치되지 않습니다. 대신 [CodePlex](https://go.microsoft.com/fwlink/?LinkId=87843)에서 예제 데이터베이스를 다운로드할 수 있습니다. 모든 버전의 예제 데이터베이스는 함께 다운로드됩니다. 또한 [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)], [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]및 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)]와 함께 출시된 이전 데이터베이스 버전을 다운로드할 수도 있습니다.  
  
 필수 구성 요소와 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 예제 데이터베이스 다운로드 및 설치에 대한 지침은 CodePlex에서 [SQL Server 2008 예제 데이터베이스의 설치 필수 구성 요소(Installation Prerequisites for the SQL Server 2008 Sample Databases)](https://go.microsoft.com/fwlink/?LinkId=166648) 및 [예제 데이터베이스 설치(Installing Sample Databases)](https://go.microsoft.com/fwlink/?LinkId=166649) 를 참조하십시오.  
  
  
##  <a name="HowTo"></a> 방법 도움말 항목  
 이 섹션에는 보고서 작성기를 설치 및 제거하는 방법을 보여 주는 절차가 나열되어 있습니다.  
  
 [독립 실행형 버전의 보고서 작성기 &#40;보고서 작성기 설치&#41;](install-windows/install-report-builder.md)  
  
 [독립 실행형 버전의 보고서 작성기 &#40;보고서 작성기 제거&#41;](install-windows/uninstall-report-builder.md)  
  
 [보고서 작성기 &#40;보고서 작성기 시작&#41;](report-builder/start-report-builder.md)  
  
  
## <a name="see-also"></a>관련 항목:  
 [SQL Server 2014의 보고서 작성기](report-builder/report-builder-in-sql-server-2016.md)  
  
  
