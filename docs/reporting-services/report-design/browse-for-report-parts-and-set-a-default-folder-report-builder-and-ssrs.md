---
title: 보고서 파트 찾아보기 및 기본 폴더 설정(보고서 작성기 및 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: report-design
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 5cf38068-65d1-4fe8-81f3-a404d8fbc663
caps.latest.revision: 8
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 473ff7e9344534bde01fd95a0d5c16a245f3d3dd
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33021170"
---
# <a name="browse-for-report-parts-and-set-a-default-folder-report-builder-and-ssrs"></a>보고서 파트 찾아보기 및 기본 폴더 설정(보고서 작성기 및 SSRS)
페이지가 매겨진 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보고서를 만드는 가장 쉬운 방법은 테이블, 차트 등의 기존 보고서 파트를 보고서 파트 갤러리에서 보고서에 추가하는 것입니다. 보고서 파트를 보고서에 추가할 때는 해당 파트가 작동하는 데 필요한 모든 항목도 추가하게 됩니다. 예를 들어 데이터를 표시하는 모든 보고서 파트는 데이터 집합, 즉 쿼리와 데이터 원본에 대한 연결을 사용합니다. 보고서 파트를 보고서에 추가한 후 필요한 만큼 구성 요소를 수정할 수 있습니다.  
  
 보고서 서버 또는 보고서 서버와 통합된 SharePoint 사이트로 보고서 파트를 게시하기 위한 기본 폴더를 설정할 수 있습니다.  
  
 자세한 내용은 [보고서 파트&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/report-parts-report-builder-and-ssrs.md)를 참조하세요.  
  
## <a name="to-browse-for-report-parts"></a>보고서 파트를 찾아보려면  
  
1.  **삽입** 메뉴에서 **보고서 파트**를 클릭합니다.  
  
     아직 연결되어 있지 않은 경우 **보고서 서버에 연결**을 클릭하고 이름을 입력합니다.  
  
    > [!NOTE]  
    >  보고서 파트를 찾아보려면 보고서 서버에 연결되어 있어야 합니다.  
  
2.  보고서 파트에 대한 정보를 지정하여 검색 범위를 좁힐 수 있습니다. **검색** 상자에 이름과 설명의 전부 또는 일부를 입력하거나 **조건 추가** 를 클릭하고 다음 필드 중 하나나 모두의 값을 추가합니다.  
  
    -   만든 사람  
  
    -   만든 날짜  
  
    -   마지막으로 수정한 날짜  
  
    -   마지막으로 수정한 사람  
  
    -   서버 폴더  
  
    -   형식  
  
     예를 들어 이미지를 찾으려면 **조건 추가**를 클릭하고 **유형**을 클릭합니다. 드롭다운 상자에서 **이미지** 확인란을 선택하고 ENTER 키를 누르고 검색 돋보기 단추를 클릭합니다.  
  
    > [!NOTE]  
    >  **만든 사람** 및 **마지막으로 수정한 사람** 값의 경우에는 보고서 서버에 표시되어 있는 사람의 사용자 이름을 검색합니다.  
  
## <a name="to-set-a-default-folder-for-report-parts"></a>보고서 파트의 기본 폴더를 설정하려면  
  
1.  **보고서 작성기**를 클릭한 다음 **옵션**을 클릭합니다.  
  
2.  **옵션** 대화 상자의 **설정** 탭에 있는 **다음 폴더에 보고서 파트를 기본적으로 게시** 입력란에 폴더 이름을 입력합니다.  
  
 보고서 서버에 폴더를 만들 수 있는 권한이 있는 경우 이 폴더가 없으면 보고서 작성기가 이 폴더를 만듭니다.  
  
 이 설정을 적용하기 위해 보고서 작성기를 다시 시작할 필요는 없습니다.  
  
## <a name="see-also"></a>참고 항목  
 [업데이트 확인 또는 업데이트 해제(보고서 작성기 및 SSRS)](http://msdn.microsoft.com/en-us/9c69792d-d7c4-453b-ae2f-6d2d071d8606)   
 [보고서 파트&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/report-parts-report-builder-and-ssrs.md)   
 [보고서 작성기의 보고서 파트 및 데이터 집합](../../reporting-services/report-data/report-parts-and-datasets-in-report-builder.md)   
 [보고서 파트 문제 해결(보고서 작성기 및 SSRS)](http://msdn.microsoft.com/en-us/d9fe1932-46e7-421b-a8a9-4c54d9576e94)   
 [보고서 파트 게시 및 다시 게시&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/publish-and-republish-report-parts-report-builder-and-ssrs.md)  
  
  
