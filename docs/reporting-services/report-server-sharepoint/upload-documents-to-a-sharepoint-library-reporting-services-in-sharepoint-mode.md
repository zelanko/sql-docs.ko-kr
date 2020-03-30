---
title: SharePoint 라이브러리에 문서 업로드(SharePoint 모드의 Reporting Services) | Microsoft Docs
ms.date: 09/25/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-sharepoint
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
monikerRange: '>=sql-server-2016 <=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 2187cd5f69b49095b085ee6f49241227207842c2
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "65580465"
---
# <a name="upload-documents-to-a-sharepoint-library-reporting-services-in-sharepoint-mode"></a>SharePoint 라이브러리에 문서 업로드(SharePoint 모드의 Reporting Services)

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

SharePoint 라이브러리에 보고서 정의 및 보고서 모델을 업로드할 수 있습니다. 보고서 서버 항목을 업로드하는 경우 라이브러리 또는 라이브러리 내의 폴더를 선택해야 합니다. 보고서 서버 항목을 목록 또는 페이지에 업로드할 수는 없습니다.  

> [!NOTE]
> SQL Server 2016 이후부터 SharePoint와의 Reporting Services 통합을 사용할 수 없습니다.

 데이터 원본 파일(.rds)을 업로드할 수 없습니다. 그러나 보고서 디자이너와 같은 디자인 도구에서 SharePoint 라이브러리로 .rds 파일을 게시할 수 있습니다. 게시하는 동안 솔루션의 원래 .rds 파일에서 새 .rsds 파일이 생성됩니다. SharePoint 라이브러리에서 새 .rsds 파일을 만든 다음 업로드된 보고서 및 모델의 데이터 원본 연결 속성을 설정하여 새 연결을 사용하도록 만들 수도 있습니다.  
  
> [!NOTE]  
>  보고서 서버는 SharePoint 모드로 구성해야 하며 SharePoint 제품 인스턴스에는 SharePoint 사이트의 보고서 서버 항목을 저장 및 액세스하기 위한 프로그램 파일을 제공하는 Reporting Services 추가 기능이 있어야 합니다.  
  
 라이브러리에 문서를 업로드하려면 사이트 수준의 "항목 추가" 권한이 있어야 합니다. 기본 보안 설정을 사용하는 경우 이 권한은 모든 권한 수준의 사용 권한이 있는 **Owners** 그룹의 멤버와 참가 수준의 사용 권한이 있는 **Members** 그룹의 멤버에게 부여됩니다.  
  
## <a name="add-a-report-definition-or-report-model-to-a-library"></a>라이브러리에 보고서 정의 또는 보고서 모델 추가
  
1.  라이브러리 또는 라이브러리 내의 폴더를 엽니다. 라이브러리가 열려 있지 않으면 빠른 실행에서 해당 이름을 클릭합니다. 라이브러리 이름이 나타나지 않으면 **모든 사이트 콘텐츠 보기**를 클릭한 다음 라이브러리 이름을 클릭합니다.  
  
2.  **업로드** 메뉴에서 **문서 업로드**를 클릭합니다.  
  
3.  단일 보고서 또는 보고서 모델 파일을 업로드하려면 보고서 정의 파일(.rdl) 또는 보고서 모델 파일(.smdl)을 선택한 다음 **확인**을 클릭합니다.  
  
     보고서 정의가 공유 데이터 원본 파일(.rsds)을 사용하여 외부 데이터 원본에 대한 연결 정보를 저장하는 경우 .rdl 파일 및 .rsds 파일을 동시에 업로드할 수 있습니다. 이렇게 하려면 **여러 문서 업로드**를 클릭하고 두 파일을 모두 지정한 다음 **확인**을 클릭합니다.  
  
 공유 데이터 원본, 보고서 모델 또는 보고서에 대한 참조를 포함하는 보고서를 업로드하는 경우 파일을 업로드하면 해당 참조가 손상됩니다. 참조를 다시 설정하는 방법은 [공유 데이터 원본 만들기 및 관리&#40;SharePoint 통합 모드의 Reporting Services&#41;](https://msdn.microsoft.com/library/2d3428e4-a810-4e66-a287-ff18e57fad76)를 참조하세요.  
  
 보고서를 업로드하면 사용자가 열 때 해당 보고서가 요청 시 실행되어 데이터 원본의 라이브 데이터가 검색됩니다. 일정에 따라 데이터를 검색하거나 캐시된 데이터를 사용하도록 보고서를 구성할 수도 있습니다. 자세한 내용은 [처리 옵션 설정&#40;SharePoint 통합 모드의 Reporting Services&#41;](../../reporting-services/report-server-sharepoint/set-processing-options-reporting-services-in-sharepoint-integrated-mode.md)을 참조하세요.  
  
 사용자가 데이터를 필터링할 수 있도록 보고서에 매개 변수를 포함할 수 있으며 이러한 매개 변수에 특정 값을 지정하거나 사용자에게 매개 변수가 표시되는 방식을 변경할 수 있습니다. 자세한 내용은 [게시된 보고서에 매개 변수 설정&#40;SharePoint 통합 모드의 Reporting Services&#41;](../../reporting-services/report-design/set-parameters-on-a-published-report-sharepoint-integrated-mode.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목

 [SharePoint 라이브러리에 보고서 게시](../../reporting-services/reports/publish-a-report-to-a-sharepoint-library.md)   
 [SharePoint 라이브러리에 공유 데이터 원본 게시](../../reporting-services/reports/publish-a-shared-data-source-to-a-sharepoint-library.md)   
 [SharePoint 사이트의 보고서 서버 항목에 대한 사용 권한 부여](../../reporting-services/security/granting-permissions-on-report-server-items-on-a-sharepoint-site.md)  

추가 질문이 있으신가요? [Reporting Services 포럼에서 질문하기](https://go.microsoft.com/fwlink/?LinkId=620231)
