---
title: "파일 공유 배달 Reporting Services의 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- subscriptions [Reporting Services], file share delivery
- file share delivery [Reporting Services]
ms.assetid: 9f338dd3-f68a-4355-b9d7-9b25dacf3b5e
caps.latest.revision: 54
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 5e33585c625c49967304ca36ad91ccc1ebac32f1
ms.contentlocale: ko-kr
ms.lasthandoff: 08/09/2017

---
# <a name="file-share-delivery-in-reporting-services"></a>Reporting Services의 파일 공유 배달
  SQL Server [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 에는 보고서를 폴더에 배달할 수 있도록 파일 공유 배달 확장 프로그램이 포함되어 있습니다. 파일 공유 배달 확장 프로그램은 기본적으로 사용 가능하며 추가 구성이 필요하지 않습니다. 파일을 성공적으로 배달하려면 공유 폴더에 쓰기 권한을 설정해야 합니다. 작성자 권한이 있어야 하는 계정은 구독에 구성되어 있는 자격 증명일 수도 있고 보고서 서버용으로 구성된 **파일 공유 계정** 일 수도 있습니다. 파일 공유 계정에 대한 자세한 내용은 [구독 설정 및 파일 공유 계정&#40;구성 관리자&#41;](../../reporting-services/install-windows/subscription-settings-and-a-file-share-account-configuration-manager.md)을 참조하세요. 또한 보고서에 액세스해야 하는 사용자에게 공유 폴더에 대한 읽기 권한이 있어야 합니다.  
  
 파일 공유에 보고서를 배포하려면 표준 구독 또는 데이터 기반 구독을 정의합니다. 데이터 기반 구독에서 파일 공유 배달을 사용 하는 방법을 알아보려면 참조 [데이터 기반 구독 &#40; 만들기 SSRS 자습서 &#41; ](../../reporting-services/create-a-data-driven-subscription-ssrs-tutorial.md). 또한 원격 파일 공유 구독을 실행하는 계정의 경우 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 컴퓨터에 로컬로 로그온할 수 있는 권한이 필요합니다.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 기본 모드 &#124; [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 모드|  
  
 **항목 내용**  
  
-   [보고서가 공유 폴더로 배달하는 특성](#bkmk_Characteristics)  
  
-   [대상 폴더](#bkmk_target_folders)  
  
-   [파일 형식](#bkmk_file_formats)  
  
-   [파일 옵션](#bkmk_file_options)  
  
##  <a name="bkmk_Characteristics"></a> 보고서가 공유 폴더로 배달하는 특성  
  
-   보고서 서버에서 호스팅하고 관리하는 보고서와 달리 공유 폴더에 배달되는 보고서는 정적 파일입니다.  
  
-   보고서에 대해 정의된 대화형 기능은 파일 시스템에서 파일로 저장된 보고서에 대해 작동하지 **않습니다** . 상호 작용 기능은 정적 요소로 표시됩니다. 예를 들어 행렬 보고서를 배달하는 경우 결과 파일은 보고서의 최상위 보기를 표시하기 때문에 행 및 열을 확장하여 지원 데이터를 볼 수 없습니다.  
  
-   보고서에 차트가 포함되어 있는 경우 기본 표시가 사용됩니다. 보고서에 포함되어 있는 다른 보고서에 대한 링크는 정적 텍스트로 렌더링됩니다.  
  
-   배달된 보고서에서 대화형 기능을 유지하려면 전자 메일 배달을 대신 사용하십시오. 전자 메일에는 보고서 서버의 보고서로 이동할 수 있는 링크가 포함되며, 사용자는 대화형 기능을 사용할 수 있습니다. 자세한 내용은 [Reporting Services의 전자 메일 배달](../../reporting-services/subscriptions/e-mail-delivery-in-reporting-services.md)을 참조하세요.  
  
##  <a name="bkmk_target_folders"></a> 대상 폴더  
 파일 공유 배달을 사용하는 구독을 정의할 때는 기존 폴더를 대상 폴더로 지정해야 합니다. 보고서 서버는 파일 시스템에 폴더를 만들지 않습니다. 지정하는 폴더는 네트워크 연결을 통해 액세스할 수 있어야 합니다.  
  
 공유 폴더의 보고서를 **볼** 사용자에게 읽기 권한이 있는지 확인합니다.  
  
 구독에 대상 폴더를 지정하는 경우 컴퓨터의 네트워크 이름을 포함하는 UNC(Uniform Naming Convention) 형식을 사용합니다. 이때 폴더 경로에 후행 백슬래시를 포함하지 마세요. 다음은 UNC 경로를 보여 주는 예입니다.  
  
```  
\\<servername>\reportarchive\operations\2014  
```  
  
 폴더를 만들 때 필요한 연결 제한을 고려합니다. 보고서 서버에는 두 개의 연결이 필요하지만 공유 폴더의 보고서를 열려는 다른 사용자를 수용할 만큼 충분한 연결을 포함해야 합니다.  
  
##  <a name="bkmk_file_formats"></a> 파일 형식  
 HTML, DOCX, Excel 등의 다양한 파일 형식으로 보고서를 렌더링할 수 있습니다. 보고서를 특정 파일 형식으로 저장하려면 구독을 만들 때 해당 렌더링 형식을 선택합니다. 예를 들어 **Excel** 을 선택하면 보고서가 [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] 파일로 저장됩니다. 지원되는 모든 렌더링 형식 중에서 선택할 수 있지만 파일로 렌더링하기에 보다 나은 형식이 있습니다.  
  
 파일 공유 배달의 경우 보고서를 단일 파일로 배달하는 형식을 선택하세요. 이 형식에서는 모든 이미지와 관련 내용이 보고서에 포함됩니다. 적합한 형식으로는 웹 보관 파일, PDF, TIFF, Excel 등이 있습니다. HTML4.0은 선택하지 마세요. 보고서에 이미지가 있는 경우 HTML 4.0 형식을 사용하면 파일에 이미지가 포함되지 않습니다.  
  
##  <a name="bkmk_file_options"></a> 파일 옵션  
 파일 공유 구독을 만들 때는 파일 이름이 생성되는 방식 및 파일이 이전 버전 보고서를 덮어쓰는지 여부를 구성할 수 있습니다. 정규화된 파일 이름에는 이름, 확장명, 그리고 고유한 파일 이름을 만들기 위해 파일에 추가되는 텍스트나 숫자의 세 부분이 포함됩니다.  
  
 **파일 이름:** 기본 파일 이름은 원본 보고서 이름을 따르지만 구독에서 사용자 지정 이름을 제공할 수 있습니다. 확장명은 옵션이지만 사용자가 지정하면 보고서 서버가 렌더링 형식에 해당하는 확장명을 만듭니다.  
  
 **덮어쓰기:** 덮어쓰기 옵션을 지정해 각각의 보고서 배달에 대해 동일한 파일 이름을 다시 사용할지 아니면 새 파일을 만들지를 선택할 수 있습니다. 파일을 덮어쓰려면 동일한 파일 이름 및 확장명을 사용해야 합니다.  
  
 배달마다 고유한 파일을 만들기 위한 또 다른 방법은 파일 이름에 타임스탬프를 포함하는 것입니다. 이렇게 하려면 파일 이름에 **@timestamp** 변수를 추가하세요(예: *CompanySales@timestamp*). 이 방법을 사용하면 파일 이름 정의가 고유하게 되므로 덮어쓰는 일이 생기지 않습니다.  
  
 다음 이미지에는 파일 공유 배달에 대해 구성된 구독의 파일 설정 예가 나와 있습니다.  
  
 ![파일 공유 구독](../../reporting-services/subscriptions/media/ssrs-file-share-subscription.png "파일 공유 구독")  
  
## <a name="see-also"></a>관련 항목:  
 [기본 모드 보고서 서버 구독 만들기 및 관리](../../reporting-services/subscriptions/create-and-manage-subscriptions-for-native-mode-report-servers.md)   
 [구독 설정 및 파일 공유 계정 &#40; 구성 관리자 &#41;](../../reporting-services/install-windows/subscription-settings-and-a-file-share-account-configuration-manager.md)  
  
  
