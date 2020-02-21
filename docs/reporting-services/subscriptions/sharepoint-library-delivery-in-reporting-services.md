---
title: Reporting Services의 SharePoint 라이브러리 배달 | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: subscriptions
ms.topic: conceptual
helpviewer_keywords:
- SharePoint integration [Reporting Services], report delivery
- delivering reports [Reporting Services]
- subscriptions [Reporting Services], SharePoint library delivery
ms.assetid: cb4e4f71-f2d5-475a-9284-ea324c93c7de
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: b4bf1f99d6ebadaa0b5740d3563386802bbc3e69
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "65578072"
---
# <a name="sharepoint-library-delivery-in-reporting-services"></a>Reporting Services의 SharePoint 라이브러리 배달
  SharePoint 통합용으로 구성된 보고서 서버는 보고서를 SharePoint 라이브러리로 보내는 데 사용할 수 있는 배달 확장 프로그램이 포함되어 있습니다.  
  
 SharePoint 배달 확장 프로그램을 사용하려면 SharePoint 사이트의 애플리케이션 페이지에서 구독을 만든 다음 배달 유형으로 **SharePoint 문서 라이브러리** 를 선택해야 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 또는 보고서 관리자에서 만든 구독에 대해서는 SharePoint 배달 확장 프로그램을 사용할 수 없습니다.  
  
> [!NOTE]  
>  배달 확장 프로그램은 보고서 서버가 기본 모드로 실행되고 있는 경우 SharePoint 사이트로의 보고서 배달을 지원하지 않습니다. 기본 모드 보고서 서버에 대해 프로그래밍 방식으로 배달 확장 프로그램을 호출하려고 하면 서버에서 **rsDeliveryExtensionNotFound** 오류를 반환하고 보고서 서버 로그 파일에 **rsOperationNotSupportedSharePointMode** 오류를 기록합니다.  
  
## <a name="requirements"></a>요구 사항  
 렌더링된 보고서를 라이브러리에 배달하기 위한 요구 사항은 다음과 같습니다.  
  
-   보고서 서버는 SharePoint 통합 모드용으로 구성되어야 합니다.  
  
-   보고서 서버에 SharePoint 배달 확장 프로그램이 설치 및 구성되어 있어야 합니다.  
  
-   보고서는 보고서 정의 파일(.rdl)이어야 합니다. 구독을 통해 모델이나 리소스와 같은 다른 보고서 서버 콘텐츠 형식을 배달할 수는 없습니다. 또한 모델을 데이터 원본으로 사용하는 임시 보고서는 구독할 수 없습니다.  
  
-   보고서는 저장된 자격 증명을 사용해야 합니다. 이는 배달 유형에 관계없이 보고서에 대한 구독을 만들기 위한 선행 조건입니다.  
  
-   대상은 SharePoint 라이브러리여야 합니다. 대상 라이브러리를 선택할 때는 동일한 SharePoint 사이트에 있는 라이브러리를 선택해야 합니다. 다른 서버 또는 동일한 사이트 모음 내에 있는 다른 사이트의 라이브러리에는 보고서를 배달할 수 없습니다.  
  
 속성과 메타데이터는 보고서 배달에 포함되지 않습니다. 보고서는 처음 배달될 때 해당 보고서가 포함된 폴더나 목록의 보안 설정을 상속받습니다. 이후에 보안 설정을 수정하거나 보안 속성을 설정해도 이러한 설정은 유지됩니다. 구독에서는 단순히 지정된 위치에 저장된 보고서를 새로 고칩니다.  
  
## <a name="sharepoint-permissions"></a>SharePoint 사용 권한  
 구독을 만들려면 보고서에 대한 항목 보기 권한이 있어야 합니다. 보고서를 배달하려면 보고서가 배달되는 라이브러리에 대한 항목 추가 권한이 있어야 합니다.  
  
## <a name="how-to-create-modify-and-delete-subscriptions"></a>구독 생성, 수정 및 삭제 방법  
  
1.  보고서에 액세스할 SharePoint 사이트로 이동합니다.  
  
2.  보고서를 선택하고 보고서 옆의 아래쪽 화살표를 클릭한 다음 **구독 관리**를 선택합니다.  
  
3.  **만들기**, **편집**또는 **삭제**를 클릭합니다.  
  
 구독 관리 목록의 상태 메시지에 구독 성공 여부 및 구독이 마지막으로 실행된 날짜/시간을 비롯하여 구독에 대한 현재 정보가 표시됩니다.  
  
## <a name="setting-delivery-options"></a>배달 옵션 설정  
 SharePoint 라이브러리에 보고서를 배달하는 구독에 대해 다음 배달 옵션을 설정할 수 있습니다.  
  
 출력 형식 렌더링  
 보고서를 배달할 애플리케이션 형식을 지정합니다. 보고서는 배달되기 전에 이 형식으로 렌더링됩니다. 선택한 출력 형식에 따라 기본 파일 확장명이 결정됩니다.  
  
 선택할 수 있는 출력 형식은 보고서 서버에 설치된 렌더링 확장 프로그램 집합입니다.  
  
 내부에서만 사용되거나 SharePoint 통합 모드로 실행되는 보고서 서버에 대해 지원되지 않는 출력 형식은 지정할 수 없습니다. 이러한 형식에는 Null, RGDI 및 HTMLOWC가 있습니다.  
  
 파일 이름 및 확장명  
 대상 라이브러리에 표시할 보고서의 파일 이름과 확장명을 지정합니다. 파일 확장명을 지정하지 않으면 보고서 서버에서 보고서 출력 형식을 기반으로 확장명을 만듭니다. 이 값은 필수입니다. 파일 이름에 다음 문자는 포함하지 마세요. : \ / * ? " < > | # { } %  
  
 제목  
 대상 라이브러리에 있는 보고서의 선택적 **Title** 속성을 지정합니다. 이는 라이브러리에 저장된 모든 항목의 표준 속성입니다. 사용자는 SharePoint 사이트의 라이브러리 내용을 볼 때 이 속성을 표시할지 여부를 지정할 수 있습니다.  
  
 경로  
 SharePoint 웹 애플리케이션 및 사이트를 포함하는 SharePoint 라이브러리에 대한 정규화된 URL을 지정합니다. 예를 들어 `https://mySharePointWeb/MySite/MyDocLib`에서 `https://mySharePointWeb`은 웹 애플리케이션을 나타내고 "MySite"는 SharePoint 사이트를 나타내며 "MyDocLib"는 보고서가 배달될 SharePoint 라이브러리를 나타냅니다.  
  
 페이지, 사이트 또는 목록은 지정할 수 없습니다. 대상 컨테이너는 동일한 사이트나 팜에 있는 라이브러리여야 합니다.  
  
 덮어쓰기 옵션  
 구독을 처리할 때 이름과 확장명이 같은 파일을 최신 버전으로 바꿀지 여부를 지정합니다. 기존 파일을 최신 버전으로 바꾸려면 **덮어쓰기** 를 선택합니다. 구독에서 파일을 바꾸지 않도록 하려면 **없음** 을 선택합니다. 이 경우 대상 이름 및 확장명과 동일한 파일이 있으면 배달 작업이 수행되지 않습니다. 파일 이름 끝에 번호를 추가하여 동일한 파일의 연속 버전을 추가하려면 **자동 증가** 를 선택합니다.  
  
 자동 복사  
 자동 복사 기능을 사용하여 파일의 최신 버전을 자동으로 여러 위치에 복사하는 경우 **덮어쓰기** 가 설정되어 있으면 파일이 복사됩니다. **자동 증가** 또는 **없음**을 사용하는 경우에는 배달이 실패하고 **rsDeliveryError** 오류가 발생합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SharePoint 모드 보고서 서버 구독 만들기 및 관리](../../reporting-services/subscriptions/create-and-manage-subscriptions-for-sharepoint-mode-report-servers.md)   
 [구독 및 배달&#40;Reporting Services&#41;](../../reporting-services/subscriptions/subscriptions-and-delivery-reporting-services.md)   
 [보고서 데이터 원본에 대한 자격 증명 및 연결 정보 지정](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md)  
  
  
