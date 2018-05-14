---
title: 링크된 보고서 만들기 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: reports
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- linked reports [Reporting Services], creating
ms.assetid: 12be8341-cb57-45e8-a421-2bf66b50234d
caps.latest.revision: 44
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: d666a071193ad436cadb83c24692231e10ab2857
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="create-a-linked-report"></a>링크된 보고서 만들기
  링크된 보고서는 기존 보고서에 대한 액세스 지점을 제공하는 보고서 서버 항목입니다. 개념적으로 링크된 보고서는 프로그램을 실행하거나 파일을 열 때 사용하는 프로그램 바로 가기와 비슷합니다.  
  
 링크된 보고서는 기존 보고서에서 파생되며 원본 보고서의 정의를 유지합니다. 또한 항상 원본 보고서의 보고서 레이아웃과 데이터 원본 속성을 상속합니다. 보안, 매개 변수, 위치, 구독 및 일정을 비롯한 다른 모든 속성 및 설정은 원본 보고서와 다를 수 있습니다.  
  
 기존 보고서의 다른 버전을 추가로 만들려는 경우에 링크된 보고서를 만들 수 있습니다. 예를 들어 한 지역의 판매 보고서를 사용하여 모든 판매 지역에 대한 지역별 보고서를 만들 수 있습니다.  
  
 링크된 보고서는 일반적으로 매개 변수가 있는 보고서를 기반으로 하지만 매개 변수가 있는 보고서가 반드시 필요하지는 않습니다. 기존 보고서를 다른 설정으로 배포하고자 할 때마다 링크된 보고서를 만들 수 있습니다.  
  
### <a name="to-create-a-linked-report"></a>링크된 보고서를 만들려면  
  
1.  보고서 관리자에서 링크하려는 보고서가 있는 폴더로 이동한 후 옵션 메뉴를 열고 **링크된 보고서 만들기**를 클릭합니다.  
  
2.  새 링크된 보고서의 이름을 입력합니다. 설명을 입력합니다(옵션).  
  
3.  보고서를 다른 폴더에 만들려면 **위치 변경**을 클릭합니다. 사용할 폴더를 클릭하거나 **위치** 상자에 폴더 이름을 입력합니다. [!INCLUDE[clickOK](../../includes/clickok-md.md)] 다른 폴더를 선택하지 않으면 현재 폴더(기반이 되는 보고서가 저장되어 있는 폴더)에 링크된 보고서가 만들어집니다.  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)] 링크된 보고서가 열립니다.  
  
     링크된 보고서의 아이콘은 보고서 서버가 관리하는 다른 항목의 아이콘과 다릅니다. 다음 아이콘은 링크된 보고서를 나타냅니다.  
  
     ![링크된 보고서 아이콘](../../reporting-services/report-server/media/hlp-16linked.gif "링크된 보고서 아이콘")  
  
## <a name="see-also"></a>참고 항목  
 [보고서 열기 및 닫기&#40;보고서 관리자&#41;](../../reporting-services/reports/open-and-close-a-report-report-manager.md)   
 [새 링크된 보고서 페이지&#40;보고서 관리자&#41;](http://msdn.microsoft.com/library/fefb46e8-6901-4d50-a3f8-7c49ad72e7b1)   
 [항목 위치 선택 페이지&#40;보고서 관리자&#41;](http://msdn.microsoft.com/library/4a53a1a8-d1e1-47ef-b1fc-63352ece7d3c)   
 [일반 속성 페이지, 보고서&#40;보고서 관리자&#41;](http://msdn.microsoft.com/library/66c99d28-ab41-45f0-bf02-ed560293595d)   
 [Reporting Services 개념&#40;SSRS&#41;](../../reporting-services/reporting-services-concepts-ssrs.md)   
 [보고서 관리자&#40;SSRS 기본 모드&#41;](http://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896)  
  
  
