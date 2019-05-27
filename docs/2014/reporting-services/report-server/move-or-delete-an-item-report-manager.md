---
title: 항목 이동 또는 삭제(보고서 관리자) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- moving items
- items [Reporting Services], moving
ms.assetid: 980a66c7-a18b-4af7-8954-45726fa517d6
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: aafd2ff32e8c554186d18a6329649081e8babe6b
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66103733"
---
# <a name="move-or-delete-an-item-report-manager"></a>항목 이동 또는 삭제(보고서 관리자)
  보고서 서버에 게시하는 보고서 및 보고서 관련 항목은 폴더에 저장됩니다. 항목을 다른 폴더로 이동할 수 있으며 해당 항목에 대한 참조는 보고서 서버에서 자동으로 유지 관리됩니다. 항목을 삭제하기 전에 해당 항목에 다른 항목이 종속되어 있는지 확인하십시오.  
  
## <a name="move-an-item"></a>항목 이동  
 보고서 서버 항목을 보고서 서버 폴더 계층의 다른 폴더 위치로 이동할 수 있습니다. 항목을 이동하면 모든 속성(보안 설정 포함)도 항목과 함께 새 위치로 이동됩니다. 폴더를 이동하면 폴더 내의 모든 항목이 함께 이동됩니다.  
  
 보고서 관리자에서 이동할 수 있는 항목은 폴더 계층 구조에 표시됩니다. 다음 표에서는 이동 가능한 각 항목의 아이콘을 보여 줍니다.  
  
|아이콘|이동 가능한 항목|  
|----------|-------------------|  
|![보고서 아이콘](../media/hlp-16doc.gif "보고서 아이콘")|보고서|  
|![링크된 보고서 아이콘](../media/hlp-16linked.gif "링크된 보고서 아이콘")|링크된 보고서|  
|![폴더 아이콘](../media/hlp-16folder.gif "폴더 아이콘")|Folder|  
|![일반 리소스 아이콘](../media/hlp-16file.gif "일반 리소스 아이콘")|일반 리소스|  
|![공유 데이터 원본 아이콘](../media/hlp-16datasource.png "공유 데이터 원본 아이콘")|공유 데이터 원본|  
||공유 데이터 세트|  
  
 작업하는 모든 항목을 이동할 수 있는 것은 아닙니다. 구독이나 보고서 기록과 같이 보고서와 연결된 항목은 이동할 수 없습니다. 이러한 항목은 연결된 보고서와 함께 이동됩니다. 마찬가지로 공유 일정과 같이 폴더 계층 밖에 있는 항목도 이동할 수 없습니다. 항목 이동 권한이 없으면 항목을 이동할 수 없습니다. 항목 이동 권한은 해당 항목에 대한 역할 할당에서 "보고서 관리," "모델 관리," "폴더 관리" 및 "데이터 원본 관리" 태스크를 선택한 경우에만 부여됩니다.  
  
#### <a name="to-move-an-item-from-within-the-contents-page"></a>내용 페이지에서 항목을 이동하려면  
  
1.  시작 [보고서 관리자 &#40;SSRS 기본 모드&#41;]... / 보고서-manager-ssrs-네이티브-mode.md).  
  
2.  보고서 관리자에서 **내용** 페이지로 이동한 다음 이동할 항목을 찾습니다.  
  
3.  항목 위로 마우스를 이동하여 드롭다운 화살표를 클릭합니다.  
  
4.  드롭다운 메뉴에서 **이동**을 클릭합니다.  
  
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
6.  **위치**에서 항목을 이동할 폴더를 지정합니다. 정규화된 폴더 이름을 입력하거나 트리 컨트롤을 사용하여 해당 폴더로 이동합니다.  
  
7.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
 또는 이동할 개체로 이동하고 **속성**을 클릭한 후 페이지 맨 위에서 **이동** 을 클릭합니다.  
  
## <a name="delete-an-item"></a>항목 삭제  
 항목을 삭제하기 전에 해당 항목이 다른 항목에 사용되고 있는지 확인하십시오. 예를 들어 공유 데이터 원본을 삭제하는 경우 해당 데이터 원본을 사용하는 보고서와 모델이 더 이상 실행되지 않습니다. 보고서를 삭제하는 경우 해당 보고서와 관련된 구독 및 보고서 기록도 삭제됩니다. 참조 항목에 대 한 종속 항목을 찾으려면 [종속 항목 페이지 &#40;보고서 관리자&#41;]... / 종속-항목-페이지-보고서-manager.md).  
  
#### <a name="to-delete-a-report-or-item"></a>보고서 또는 항목을 삭제하려면  
  
1.  시작 [보고서 관리자 &#40;SSRS 기본 모드&#41;]... / 보고서-manager-ssrs-네이티브-mode.md).  
  
2.  보고서 관리자에서 **내용** 페이지로 이동한 다음 삭제할 항목을 찾습니다.  
  
3.  항목 위로 마우스를 이동하여 드롭다운 화살표를 클릭합니다.  
  
4.  드롭다운 메뉴에서 **삭제**를 클릭합니다.  
  
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>관련 항목  
 [페이지 콘텐츠를 &#40;보고서 관리자&#41;]... / 콘텐츠 페이지-보고서 manager.md)   
 [보고서 찾기, 보기 및 관리&#40;보고서 작성기 및 SSRS&#41;](../report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)  
  
  
