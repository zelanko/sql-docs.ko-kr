---
title: '태스크 8: Excel에서 State 엔터티에 새 값을 추가 합니다. | Microsoft Docs'
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: a763d76b-06a3-4d51-9614-01fc9fb1c158
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 831d0b504a65d485413772ee3711e689e29ee2a3
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65489702"
---
# <a name="task-8-adding-a-new-value-for-state-entity-in-excel"></a>태스크 8: Excel에서 State 엔터티에 새 값 추가
  이 작업에서는 Excel에서 State 엔터티에 대한 값을 추가하고 변경 내용을 MDS 서버에 게시합니다.  
  
1.  추가 된 **워크시트** 맨 아래에 새 탭을 클릭 하 여 Excel에서.  
  
     ![Excel-새 워크시트 탭](../../2014/tutorials/media/et-addinganewvalueforstateentityinexcel-01.jpg "Excel-새 워크시트 탭")  
  
2.  **Excel**를 클릭 합니다 **마스터 데이터** 메뉴의 탭을 클릭 **탐색기 표시** 리본의.  
  
3.  에 **마스터 데이터 탐색기**를 선택 **Suppliers** 에 대 한 **모델**합니다. 두 개의 엔터티가 표시 됩니다. **공급 업체** 하 고 **상태** 엔터티 목록에서.  
  
4.  두 번 클릭 **상태** 목록에서입니다. 모든 멤버를 **상태** 워크시트에 MDS에서 엔터티를 표시 해야 합니다.  
  
5.  이제 다음 값을 사용 하 여 끝에 행을 추가: **North Carolina** 에 대 한 **이름** 하 고 **NC** 에 대 한 **코드**합니다. 색 구분에 따라 새 레코드/업데이트된 레코드가 다른 레코드와 구분됩니다.  
  
     ![Excel-상태에 North Carolina 추가](../../2014/tutorials/media/et-addinganewvalueforstateentityinexcel-02.jpg "Excel-상태에 North Carolina 추가")  
  
6.  클릭 **게시** MDS에 변경 내용을 게시 하려면 리본 메뉴에 있습니다.  
  
     ![Excel-마스터 데이터 탭의 단추를 게시](../../2014/tutorials/media/et-addinganewvalueforstateentityinexcel-03.jpg "Excel-마스터 데이터 탭의 게시 단추")  
  
7.  에 **게시 및 주석** 대화 상자에서 **모든 변경 내용에 동일한 주석 사용** 을 선택 합니다. 여기에서 모든 변경 내용에 대해 단일 주석을 입력할 수 있습니다.  
  
8.  선택 **변경 내용을 검토 하 고 개별적으로 주석 제공** (이 예제의 경우 하나만) 각 변경에 대해 주석을 제공 하는 옵션입니다.  
  
     ![Excel-게시 및 주석 대화 상자](../../2014/tutorials/media/et-addinganewvalueforstateentityinexcel-04.jpg "Excel-게시 및 주석 대화 상자")  
  
9. 클릭 **게시** MDS에 데이터를 게시할 수 있습니다.  
  
10. 있음을 **색 코딩** 행에 대 한 **North Carolina** 으로 **상태** 이제 다른 레코드와 동일 하 게 됩니다.  
  
11. **선택 사항:** 새 멤버 (NC)에 추가 되었는지 확인 합니다 **상태** 사용 하 여 엔터티를 **탐색기** 에서 **마스터 데이터 관리자**합니다.  
  
12. Excel에서 마우스 오른쪽 단추로 클릭 합니다 **상태** 아래쪽과 클릭 워크시트 **삭제** 워크시트를 삭제 하려면. 워크시트를 삭제해도 MDS 서버에서는 데이터가 삭제되지 않습니다.  
  
## <a name="next-step"></a>다음 단계  
 [태스크 9: 마스터 데이터 관리자를 사용 하 여 파생 계층 만들기](../../2014/tutorials/task-9-creating-a-derived-hierarchy-using-master-data-manager.md)  
  
  
