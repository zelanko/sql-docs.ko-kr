---
title: 보고서 작성기에서 자격 증명을 지정 합니다. | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 7412ce68-aece-41c0-8c37-76a0e54b6b53
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 32bd106320c8969813dbae107a7569af8560aba4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62513325"
---
# <a name="specify-credentials-in-report-builder"></a>보고서 작성기에 자격 증명 지정
  자격 증명은 데이터 원본에서 데이터를 검색하려는 사용자를 인증합니다. 데이터 원본의 소유자는 사용해야 하는 자격 증명의 유형을 결정합니다. 예를 들어, 데이터베이스 관리자는 사용자가 Windows 사용자 이름과 암호를 입력해야 하도록 지정할 수 있습니다.  
  
 보고서 정의에서 각 데이터 원본 정의는 이름, 연결 문자열 및 통합 보안 사용 여부 그리고 자격 증명이 요구되는데 지정되지 않았을 경우 표시할 메시지를 지정합니다. 자격 증명은 보고서 정의에 저장되지 않으며 보고서 서버에 보고서를 게시하고 나면 보고서 정의와 독립적으로 데이터 원본을 관리할 수 있습니다. 데이터 원본 소유자는 보고서 서버의 포함 데이터 원본과 고유 데이터 원본 모두에 대한 자격 증명을 지정할 수 있습니다.  
  
> [!NOTE]  
>  보고서 서버 관리자는 사용자에게 보고서 서버에서 공유 데이터 원본이나 모델을 찾아 선택하거나 보고서를 열거나 저장할 수 있는 적절한 권한을 부여해야 합니다. 자세한 내용은 [설치, 제거 및 보고서 작성기 지원](../../2014/reporting-services/install-uninstall-and-report-builder-support.md)합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../includes/ssrbrddup-md.md)]  
  
## <a name="understanding-when-credentials-are-used"></a>자격 증명이 사용되는 경우 이해  
 보고서 작성기에서 자격 증명은 주로 보고서 서버에 연결할 때 또는 포함된 데이터 원본 작성, 데이터 세트 쿼리 실행 또는 보고서 미리 보기와 같은 데이터 관련 태스크를 위해 사용됩니다. 자격 증명은 보고서에 저장되지 않습니다. 자격 증명은 보고서 서버나 로컬 클라이언트에서 별도로 관리됩니다. 다음 목록에서는 제공해야 하는 자격 증명 유형, 자격 증명이 저장되는 위치 및 사용 방법을 설명합니다.  
  
-   [Reporting Services 로그인 대화 상자&#40;보고서 작성기&#41;](report-builder/reporting-services-login-dialog-box-report-builder.md)에 입력하는 보고서 서버 자격 증명  
  
     보고서 서버나 SharePoint 사이트로 처음 저장, 게시 또는 이동할 때 자격 증명을 입력해야 할 수도 있습니다. 입력한 자격 증명은 보고서 작성기 세션이 종료될 때까지 사용됩니다. 이러한 자격 증명을 저장하도록 선택한 경우에는 해당 자격 증명이 사용자 설정과 함께 컴퓨터에 안전하게 저장됩니다. 이후의 보고서 작성기 세션에서 저장된 자격 증명은 같은 보고서 서버나 SharePoint 사이트에 연결하는 데 사용됩니다. 보고서 서버 관리자나 SharePoint 관리자는 사용할 자격 증명 유형을 지정합니다.  
  
-   포함된 데이터 원본에 대한 [데이터 원본 속성 대화 상자, 자격 증명&#40;보고서 작성기&#41;](../../2014/reporting-services/data-source-properties-dialog-box-credentials-report-builder.md) 페이지에 입력하는 데이터 원본 자격 증명  
  
     보고서 서버에서는 이러한 자격 증명을 외부 데이터 원본으로 데이터를 연결하는 데 사용합니다. 일부 데이터 원본 유형의 경우 자격 증명을 보고서 서버에 안전하게 저장할 수 있습니다. 이러한 자격 증명을 사용하면 다른 사용자가 기본 데이터 연결에 자격 증명을 제공하지 않고 보고서를 실행할 수 있습니다.  
  
-   데이터 집합 쿼리를 실행하거나, 데이터 집합 필드를 새로 고치거나, 보고서를 미리 볼 때 [데이터 원본 자격 증명 입력 대화 상자&#40;보고서 작성기&#41;](report-data/enter-data-source-credentials-dialog-box-report-builder.md)에서 입력한 데이터 원본 자격 증명  
  
     이러한 자격 증명은 보고서 작성기에서 외부 데이터 원본으로 데이터를 연결하거나 자격 증명을 요구하도록 구성된 보고서를 미리 볼 때 사용합니다. 이 대화 상자에 입력한 자격 증명은 보고서 서버에 저장되지 않으며 다른 사용자가 사용할 수 없습니다. 보고서 작성기는 보고서 편집 세션 중에 자격 증명을 캐시하므로 쿼리를 실행하거나 보고서를 미리 볼 때마다 자격 증명을 입력하지 않아도 됩니다.  
  
     공유 데이터 원본에 대해서는 **암호 저장** 옵션을 사용하여 자격 증명을 사용자 설정과 함께 컴퓨터에 로컬로 저장할 수 있습니다. 보고서 작성기는 해당 외부 데이터 원본에 연결할 때마다 저장된 자격 증명을 사용합니다.  
  
 자세한 내용은 [데이터 원본 속성 대화 상자, 일반&#40;보고서 작성기&#41;](../../2014/reporting-services/data-source-properties-dialog-box-general-report-builder.md) 및 [보고서 작성기에서 보고서 미리 보기](report-builder/previewing-reports-in-report-builder.md)를 참조하세요.  
  
## <a name="types-of-credentials"></a>자격 증명 유형  
 데이터 원본에서 지원하는 자격 증명의 유형은 데이터 원본 소유자가 지정합니다. 예를 들어, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 데이터베이스에 액세스하기 위해 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 로그인 사용자 이름과 암호를 입력해야 하고, 다른 데이터 원본에 액세스하기 위해서는 Windows 로그인 사용자 이름과 암호를 입력해야 할 수 있습니다. 일부 데이터 원본에는 자격 증명이 필요하지 않습니다.  
  
### <a name="options-for-specifying-credentials"></a>자격 증명 지정 옵션  
 다음은 데이터 원본에 대한 자격 증명을 지정할 때 사용할 수 있는 옵션입니다.  
  
-   현재 Windows 사용자 사용(통합 보안).  
  
-   저장된 사용자 이름 및 암호 사용  
  
-   사용자에게 자격 증명을 입력하도록 메시지 표시  
  
-   자격 증명 필요 없음  
  
### <a name="windows-integrated-security"></a>Windows 통합 보안  
 **Windows 인증 사용(통합 보안)** 을 선택하면 현재 사용자의 보안 토큰이 데이터 원본으로 전달됩니다. 이 경우 사용자 이름이나 암호를 입력하라는 메시지가 표시되지 않습니다. 이 옵션을 사용하려면 일반적으로 위임 기능을 사용할 수 있어야 합니다. 이러한 기능을 사용할 수 없으면 동일한 컴퓨터에 있는 데이터 원본을 액세스할 때만 이 옵션을 사용할 수 있습니다.  
  
### <a name="user-name-and-password-login"></a>사용자 이름 및 암호 로그인  
 **이 사용자 이름 및 암호 사용**을 선택할 경우 사용자 이름과 암호를 제공해야 데이터 원본에 액세스할 수 있습니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 데이터베이스의 경우 데이터베이스 로그인에 대해 자격 증명을 사용할 수 있습니다. 자격 증명은 인증을 위해 데이터 원본으로 전달됩니다.  
  
### <a name="prompted-credentials"></a>입력 정보를 요청하는 자격 증명  
 입력 정보를 요청하는 자격 증명을 지정하면 보고서에 액세스하는 각 사용자가 데이터를 검색할 때 사용자 이름과 암호를 입력해야 합니다. 이 옵션은 기밀 데이터를 포함하는 보고서에 사용하는 것이 좋습니다. 입력 정보를 요청하는 자격 증명은 Windows 계정이거나 데이터베이스 로그인에 사용할 수 있습니다. 사용자가 입력한 자격 증명을 데이터베이스 서버에서 인식하지 못하거나, 지정한 사용자가 데이터를 검색할 수 있는 권한이 없는 경우 연결이 실패합니다.  
  
### <a name="no-credentials"></a>자격 증명 사용 안 함  
 이 데이터 원본에 대해서는 자격 증명이 필요하지 않습니다. 보고 서버에서 이 보고서를 실행하려면 무인 실행 계정을 구성해야 합니다. 자세한 내용은 참조 하세요. [무인 실행 계정 구성 &#40;SSRS 구성 관리자&#41; ](install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md) 에 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 설명서에서 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [온라인](https://go.microsoft.com/fwlink/?linkid=121312).  
  
## <a name="see-also"></a>관련 항목  
 [설치, 제거 및 보고서 작성기 지원](../../2014/reporting-services/install-uninstall-and-report-builder-support.md)   
 [포함된 데이터 연결 및 공유 데이터 연결 또는 데이터 원본&#40;보고서 작성기 및 SSRS&#41;](../../2014/reporting-services/embedded-and-shared-data-connections-or-data-sources-report-builder-and-ssrs.md)   
 [보고서 작성기 옵션 대화 상자, 설정 &#40;보고서 작성기&#41;](report-builder/set-default-options-for-report-builder.md)   
 [보고서 작성기의 데이터 연결, 데이터 원본 및 연결 문자열](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-report-builder.md)   
 [보고서에 데이터 추가 &#40;보고서 작성기 및 SSRS&#41;](report-data/report-datasets-ssrs.md)   
 [데이터 연결이 나 데이터 원본 추가 및 확인 &#40;보고서 작성기 및 SSRS&#41;](report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)  
  
  
