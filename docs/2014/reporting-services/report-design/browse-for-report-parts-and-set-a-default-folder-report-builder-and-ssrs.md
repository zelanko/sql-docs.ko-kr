---
title: 보고서 파트 찾아보기 및 기본 폴더 설정(보고서 작성기 및 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 5cf38068-65d1-4fe8-81f3-a404d8fbc663
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: ae8fddf7e008c1c97c30c18deb2d8aec60b77415
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56009585"
---
# <a name="browse-for-report-parts-and-set-a-default-folder-report-builder-and-ssrs"></a>보고서 파트 찾아보기 및 기본 폴더 설정(보고서 작성기 및 SSRS)
  보고서를 만드는 가장 쉬운 방법은 테이블, 차트 등의 기존 보고서 파트를 보고서 파트 갤러리에서 보고서에 추가하는 것입니다. 보고서 파트를 보고서에 추가할 때는 해당 파트가 작동하는 데 필요한 모든 항목도 추가하게 됩니다. 예를 들어 데이터를 표시하는 모든 보고서 파트는 데이터 세트, 즉 쿼리와 데이터 원본에 대한 연결을 사용합니다. 보고서 파트를 보고서에 추가한 후 필요한 만큼 구성 요소를 수정할 수 있습니다.  
  
 보고서 서버 또는 보고서 서버와 통합된 SharePoint 사이트로 보고서 파트를 게시하기 위한 기본 폴더를 설정할 수 있습니다.  
  
 자세한 내용은 [보고서 파트&#40;보고서 작성기 및 SSRS&#41;](../report-parts-report-builder-and-ssrs.md)를 참조하세요.  
  
### <a name="to-browse-for-report-parts"></a>보고서 파트를 찾아보려면  
  
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
  
### <a name="to-set-a-default-folder-for-report-parts"></a>보고서 파트의 기본 폴더를 설정하려면  
  
1.  **보고서 작성기**를 클릭한 다음 **옵션**을 클릭합니다.  
  
2.  **옵션** 대화 상자의 **설정** 탭에 있는 **다음 폴더에 보고서 파트를 기본적으로 게시** 입력란에 폴더 이름을 입력합니다.  
  
 보고서 서버에 폴더를 만들 수 있는 권한이 있는 경우 이 폴더가 없으면 보고서 작성기가 이 폴더를 만듭니다.  
  
 이 설정을 적용하기 위해 보고서 작성기를 다시 시작할 필요는 없습니다.  
  
## <a name="see-also"></a>관련 항목  
 [업데이트 확인 또는 업데이트 &#40;보고서 작성기 및 SSRS&#41;](../check-for-updates-or-turn-updates-off-report-builder-and-ssrs.md)   
 [보고서 파트&#40;보고서 작성기 및 SSRS&#41;](../report-parts-report-builder-and-ssrs.md)   
 [보고서 작성기의 보고서 파트 및 데이터 세트](../report-data/report-parts-and-datasets-in-report-builder.md)   
 [보고서 파트 문제 해결 &#40;보고서 작성기 및 SSRS&#41;](../troubleshoot-report-parts-report-builder-and-ssrs.md)   
 [보고서 파트 게시 및 다시 게시&#40;보고서 작성기 및 SSRS&#41;](publish-and-republish-report-parts-report-builder-and-ssrs.md)  
  
  
