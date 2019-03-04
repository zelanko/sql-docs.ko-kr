---
title: 자습서의 사전 요구 사항(보고서 작성기) | Microsoft Docs
ms.date: 05/30/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: 9b8346a6-f4f4-4ad3-bc98-8f2be342ef2d
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 9584e07c3669548418a641eae4e3e92281a397f9
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/15/2019
ms.locfileid: "56296391"
---
# <a name="prerequisites-for-tutorials-report-builder"></a>자습서의 사전 요구 사항(보고서 작성기)

보고서 작성기 자습서를 수행하려면 보고서 서버와 통합된 SharePoint 사이트 또는 보고서 서버에서 페이지가 매겨진 [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)] 보고서를 보고 저장할 수 있어야 합니다. 모든 자습서에서는 데이터에 대해 SQL Server의 인스턴스에서 처리해야 하는 리터럴 쿼리를 사용합니다.  
  
보고서 서버, SharePoint 사이트 또는 데이터 원본에 대한 액세스 권한이 없는 경우에는 오프라인 보고서 작성을 통해 보고서 작성기에 대해 배울 수 있습니다. [자습서: 오프라인에서 빠른 차트 보고서 만들기&#40;보고서 작성기&#41;](../reporting-services/report-builder/tutorial-create-a-quick-chart-report-offline-report-builder.md)를 참조하세요.  

## <a name="requirements"></a>요구 사항

보고서 작성기 자습서를 완료하려면 다음이 필요합니다.  
  
-   보고서 작성기에 대한 액세스. [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] 보고서 서버 또는 SharePoint 통합 모드의 [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] 보고서 서버에서 보고서 작성기를 실행할 수 있습니다. 첫 번째 단계인 보고서 작성기를 여는 방법은 서버마다 다릅니다.  
  
    보고서 서버에서 **새로 만들기** > **페이지가 매겨진 보고서**를 선택합니다.
  
    SharePoint 통합 모드의 보고서 서버에서 **문서** 탭의 **새 문서**를 선택하고 드롭다운 목록에서 **보고서 작성기 보고서**를 선택합니다. `https://<servername>/sites/mySite/reports`)을 입력합니다. SharePoint 관리자는 각 문서 라이브러리에서 보고서 작성기 보고서를 사용할 수 있도록 설정해야 합니다.  
  
-   [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] 보고서 서버와 통합된 SharePoint 사이트 또는 [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] 보고서 서버의 URL. 보고서, 공유 데이터 원본, 공유 데이터 세트, 보고서 파트 및 모델을 저장하고 볼 수 있는 권한이 있어야 합니다. 기본적으로 보고서 서버의 URL은 `https://<servername>/reportserver`이고, SharePoint 사이트의 URL은 `https://<sitename>` 또는 `https://<server>/site`입니다.  
  
-   SQL Server 인스턴스의 이름과 모든 데이터베이스에 대한 읽기 전용 액세스에 필요한 자격 증명. 자습서의 데이터 세트 쿼리에서는 리터럴 데이터를 사용하지만 보고서 데이터 세트에 필요한 메타데이터가 반환되도록 하려면 각 쿼리를 SQL Server 인스턴스에서 처리해야 합니다. 예를 들어 연결 문자열 `data source=<servername>`은 서버만 지정합니다. 서버에 액세스할 수 있는 권한을 부여하는 시스템 관리자가 할당한 기본 데이터베이스에 대한 읽기 권한이 있어야 합니다. 연결 문자열 `data source=<servername>;initial catalog=<database>`에 표시된 것처럼 데이터베이스를 지정할 수도 있습니다.  
  
-   [자습서: 맵 보고서(보고서 작성기)](Tutorial:%20Map%20Report%20\(Report%20Builder\).md)에서는 Bing 지도를 배경으로 지원하도록 보고서 서버를 구성해야 합니다. 자세한 내용은 [지도 보고서 지원 계획](https://msdn.microsoft.com/5ddc97a7-7ee5-475d-bc49-3b814dce7e19)을 참조하세요.   

-   [자습서: 드릴스루 보고서 및 주 보고서 만들기(보고서 작성기)](Tutorial:%20Creating%20Drillthrough%20and%20Main%20Reports%20\(Report%20Builder\).md) 자습서를 실행하려면 Contoso Sales 큐브에 액세스해야 합니다. 자세한 내용은 자습서를 참조하세요. 
  
보고서 서버 관리자는 보고서 서버에서 필요한 권한을 부여하고, [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] 폴더 위치를 구성하고, 보고서 작성기 기본 옵션을 구성해야 합니다. 자세한 내용은 [보고서 작성기 설치 및 제거](https://msdn.microsoft.com/library/2c9a5814-17bf-4947-8fb3-6269e7caa416)를 참조하세요.  

## <a name="next-steps"></a>다음 단계

[보고서 작성기 자습서](../reporting-services/report-builder-tutorials.md)  

추가 질문이 있으신가요? [Reporting Services 포럼에서 질문하기](https://go.microsoft.com/fwlink/?LinkId=620231)
