---
title: Reporting Services 보고서 서버(기본 모드) | Microsoft Docs
ms.date: 06/06/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
helpviewer_keywords:
- administering Reporting Services
- administering [Reporting Services]
- Reporting Services, administration
ms.assetid: fa0d84e2-4c21-432c-aa7c-23517da75253
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 4a0e3f521549bb309fcbd69fc7905746be09d84b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66826899"
---
# <a name="reporting-services-report-server-native-mode"></a>Reporting Services 보고서 서버(기본 모드)
  기본 모드에 대해 구성된 보고서 서버는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]구성 요소를 통해 모든 처리 및 관리 기능을 배타적으로 제공하는 애플리케이션 서버로 실행됩니다.  
  
 사용할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 관리 하려면 웹 포털 또는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보고서입니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 관리자를 사용하여 기본 모드에서 보고서 서버를 관리할 수 있습니다.  
  
 보고서 서버가 SharePoint 모드용으로 구성된 경우 SharePoint 사이트의 내용 관리 페이지를 사용하여 보고서, 공유 데이터 원본 및 다른 보고서 서버 항목을 관리해야 합니다.  
  
 이 문서는 다음 정보를 포함합니다.  
  
-   [기본 모드 요약](#bkmk_sum)  
  
-   [내용 관리](#bkmk_managecontent)  
  
-   [리소스 보안 설정 및 관리](#bkmk_manageresources)  
  
-   [보고서에서 이미지 리소스 참조](#bkmk_referenceimage)  
  
##  <a name="bkmk_sum"></a> 기본 모드 요약  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 기본 모드 설치는 관리 및 유지해야 하는 여러 서버 쪽 기능으로 구성됩니다. 서버 기능에는 다음이 포함됩니다.  
  
-   보고서 서버 서비스 내에서 실행되는 보고서 서버 웹 서비스  
  
-   예약된 작업 및 보고서 배달을 처리하는 백그라운드 처리 애플리케이션  
  
-   보고서 서버 데이터베이스  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 설치를 완전하게 관리하려면 다음 권한이 있어야 합니다.  
  
-   보고서 서버 컴퓨터에 대한 로컬 관리자 그룹의 멤버 자격이 있어야 합니다. 원격 컴퓨터에서 실행되는 서버 기능을 함께 설치할 경우 원격 연결을 통해 서버를 관리하려면 해당 컴퓨터에 대한 관리자 권한이 있어야 합니다.  
  
-   데이터베이스를 호스팅하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대한 데이터베이스 관리자 권한이 있어야 합니다.  
  
-   도메인 컨트롤러에 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 를 설치하려면 도메인 관리자여야 합니다.  
  
##  <a name="bkmk_managecontent"></a> 내용 관리  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에서 내용 관리는 보고서, 모델, 폴더, 리소스 및 공유 데이터 원본의 관리를 의미합니다. 이러한 모든 항목은 속성 및 보안 설정을 통해 개별적으로 관리할 수 있습니다. 모든 항목을 보고서 서버 폴더 네임스페이스의 다른 위치로 이동할 수 있습니다. 항목을 효과적으로 관리하려면 내용 관리자가 수행하는 태스크에 대한 지식이 필요합니다.  
  
> [!NOTE]  
>  내용 관리는 보고서 서버 관리와 다릅니다. 보고서 서버가 실행되는 환경을 관리하는 방법은 [보고서 서버 구성 및 관리&#40;Reporting Services SharePoint 모드&#41;](../../reporting-services/report-server-sharepoint/configuration-and-administration-of-a-report-server.md)를 참조하세요.  
  
 내용 관리에는 다음 태스크가 포함됩니다.  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]와 함께 제공되는 역할 기반 보안을 적용하여 보고서 서버 사이트 및 항목에 보안을 설정합니다.  
  
-   폴더를 추가, 수정 및 삭제하여 보고서 서버 폴더 계층 구조를 구성합니다.  
  
-   보고서 서버에서 관리하는 항목에 적용되는 기본값과 속성을 설정합니다. 예를 들어 보고서 기록 스토리지 정책을 결정하는 기준 최대값을 설정할 수 있습니다.  
  
-   보고서별 데이터 원본 연결 대신 사용할 수 있는 공유 데이터 원본 항목을 만듭니다. 게시자나 내용 관리자는 보고서에 원래 정의된 원본과 다른 데이터 원본을 선택할 수 있습니다. 예를 들어 테스트 데이터베이스에 대한 참조를 프로덕션 데이터베이스에 대한 참조로 바꿀 수 있습니다.  
  
-   보고서별 일정 및 구독별 일정 대신 사용할 수 있는 공유 일정을 만들어 시간에 따른 일정 정보를 보다 쉽게 관리할 수 있도록 합니다.  
  
-   데이터 저장소에서 데이터를 검색하여 받는 사람 목록을 만드는 데이터 기반 구독을 만듭니다.  
  
-   보고서 처리를 예약하고 요청 시 실행될 수 있는 보고서 처리와 캐시에서 로드되는 보고서 처리를 지정하여 서버에 대한 보고서 처리 요청의 균형을 조정합니다.  
  
 관리 태스크 수행 권한은 미리 정의된 **시스템 관리자** 및 **내용 관리자**역할을 통해 제공합니다. 보고서 서버 내용을 효과적으로 관리하려면 두 역할을 모두 할당 받아야 합니다. 이러한 미리 정의된 역할에 대한 자세한 내용은 [역할 및 권한&#40;Reporting Services&#41;](../../reporting-services/security/roles-and-permissions-reporting-services.md)를 참조하세요.  
  
 보고서 서버 내용을 관리하기 위한 도구에는 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 또는 웹 포털이 있습니다. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 를 사용하면 기본값을 설정하고 기능을 활성화할 수 있습니다. 웹 포털은 사용자에게 보고서 서버 항목 및 작업에 대한 액세스 권한을 부여하고, 보고서 및 기타 내용 유형을 확인 및 사용하고, 모든 공유 항목 및 보고서 배포 기능을 확인 및 사용하는 데 사용됩니다.  
  
##  <a name="bkmk_manageresources"></a> 리소스 보안 설정 및 관리  
 리소스는 보고서 서버에 저장되지만 보고서 서버에서 처리되지는 않는 관리되는 항목입니다. 일반적으로 리소스는 보고서 사용자에게 외부 콘텐츠를 제공합니다. 보고서에 사용되는 비즈니스 규칙을 설명하는 HTML 파일 또는 .jpg 파일의 이미지를 예로 들 수 있습니다. JPG 또는 HTML 파일은 보고서 서버에 저장되지만 보고서 서버는 이러한 파일을 먼저 처리하지 않고 브라우저에 직접 전달합니다.  
  
 보고서 서버에 리소스를 추가하려면 다음과 같이 파일을 업로드하거나 게시합니다.  
  
|연산|파일 유형|  
|---------------|---------------|  
|업로드|보고서 정의 파일(.rdl) 및 보고서 모델 파일(.smdl)을 제외한 모든 파일이 리소스로 업로드됩니다.<br /><br /> 리소스를 업로드하려면 보고서 서버가 기본 모드에서 실행되는 경우 웹 포털을 사용하고 보고서 서버가 SharePoint 통합 모드에서 실행되는 경우 SharePoint 사이트의 애플리케이션 페이지를 사용해야 합니다. 자세한 내용은 [Upload a File or Report in the Report Server](../../reporting-services/reports/upload-a-file-or-report-report-manager.md)(보고서 서버에서 파일 또는 보고서 업로드) 또는 [Upload Documents to a SharePoint Library &#40;Reporting Services in SharePoint Mode&#41;](../../reporting-services/report-server-sharepoint/upload-documents-to-a-sharepoint-library-reporting-services-in-sharepoint-mode.md)(SharePoint 라이브러리에 문서 업로드&#40;SharePoint 모드의 Reporting Services&#41;)를 참조하세요.|  
|게시|.rdl, .smdl 및 .rds 데이터 원본 파일을 제외한 프로젝트의 모든 파일이 리소스로 업로드됩니다. 리소스를 게시하려면 보고서 디자이너에서 프로젝트에 기존 항목을 추가한 다음 보고서 서버에 해당 프로젝트를 게시합니다.|  
  
 모든 리소스는 파일 시스템의 파일로 시작되어 이후에 보고서 서버에 업로드됩니다. 제한은 없습니다 최대 1GB 크기 파일 종류가 파일을 업로드할 수 있습니다. 그러나 보고서 서버에 리소스로 게시할 경우 MIME 형식이 동일한 파일 유형이 다른 파일 유형보다 적합합니다. 예를 들어 HTML 및 JPG 파일 기반의 리소스는 사용자가 클릭할 때 각각 웹 페이지와 사용자가 볼 수 있는 이미지로 렌더링되어 브라우저 창에서 열립니다. 이와 달리 데스크톱 애플리케이션 파일처럼 동일한 MIME 형식이 없는 리소스는 브라우저 창에서 렌더링되지 않을 수 있습니다.  
  
 보고서 사용자가 리소스를 볼 수 있는지 여부는 브라우저의 보기 기능에 따라 다릅니다. 리소스는 보고서 서버에서 처리되지 않기 때문에 특정 MIME 형식을 렌더링하기 위한 보기 기능을 브라우저에서 제공해야 합니다. 브라우저에서 콘텐츠를 렌더링할 수 없으면 리소스를 보는 사용자에게 리소스의 일반 속성만 표시됩니다.  
  
 리소스는 보고서, 공유 데이터 원본, 공유 일정 및 폴더와 함께 명명된 항목으로 보고서 서버 폴더 계층 구조에 존재합니다. 보고서 서버에 저장되어 있는 여느 항목과 마찬가지로 리소스를 검색하고 확인하며 보안 및 속성을 설정할 수 있습니다. 리소스를 보거나 관리하려면 역할 할당에 리소스 보기 또는 리소스 관리 태스크가 있어야 합니다.  
  
##  <a name="bkmk_referenceimage"></a> 보고서에서 이미지 리소스 참조  
 리소스에는 보고서에서 참조하는 이미지가 포함될 수 있습니다. 보고서 요구 사항에 외부 이미지 사용이 포함된 경우 이미지를 리소스로 저장하면 다음과 같은 이점이 있습니다.  
  
-   보고서 서버 데이터베이스의 중앙 집중식 스토리지. 보고서 서버 데이터베이스와 해당 내용을 다른 컴퓨터로 이동하는 경우 외부 이미지는 보고서와 함께 유지됩니다. 다른 컴퓨터의 디스크에 저장된 이미지 파일을 추적할 필요가 없습니다.  
  
-   파일 시스템 보안 대신 역할 할당을 통한 보안 유지. 보고서를 보는 데 사용된 것과 같은 사용 권한이 리소스에 적용될 수 있습니다. 이와 달리 이미지를 디스크에 저장하는 경우에는 익명 사용자 계정 또는 무인 실행 계정에 파일에 액세스할 수 있는 사용 권한이 있는지 확인해야 합니다.  
  
 보고서에서 이미지 리소스를 사용하려면 해당 이미지 파일을 프로젝트에 추가하고 보고서와 함께 게시합니다. 이미지가 게시되면 보고서의 이미지 참조가 보고서 서버의 리소스를 가리키도록 업데이트한 다음 보고서만 다시 게시하여 변경 내용을 저장할 수 있습니다. 이후에 리소스를 다시 게시하여 보고서와 독립적으로 이미지를 업데이트할 수 있습니다. 보고서는 보고서 서버에서 사용할 수 있는 가장 최신 버전의 이미지를 사용합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [보고서 서버 구성 및 관리&#40;SSRS 기본 모드&#41;](../../reporting-services/report-server/configure-and-administer-a-report-server-ssrs-native-mode.md)   
 [Reporting Services 설치 문제 해결](../../reporting-services/install-windows/troubleshoot-a-reporting-services-installation.md)  
  
  
