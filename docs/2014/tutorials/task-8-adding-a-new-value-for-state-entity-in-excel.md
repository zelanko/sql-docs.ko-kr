---
title: '작업 8: Excel에서 State 엔터티에 대 한 새 값 추가 | Microsoft Docs'
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
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "65489702"
---
# <a name="task-8-adding-a-new-value-for-state-entity-in-excel"></a>태스크 8: Excel에서 State 엔터티에 새 값 추가
  이 작업에서는 Excel에서 State 엔터티에 대한 값을 추가하고 변경 내용을 MDS 서버에 게시합니다.  
  
1.  맨 아래에 있는 새로 만들기 탭을 클릭 하 여 Excel에서 **작업 시트** 를 추가 합니다.  
  
     ![Excel - 새 워크시트 탭](../../2014/tutorials/media/et-addinganewvalueforstateentityinexcel-01.jpg "Excel - 새 워크시트 탭")  
  
2.  **Excel**의 메뉴에서 **마스터 데이터** 탭을 클릭 한 다음 리본 메뉴에서 **탐색기 표시** 를 클릭 합니다.  
  
3.  **마스터 데이터 탐색기**에서 **모델**에 대해 **Suppliers** 를 선택 합니다. 엔터티 목록에 **공급자** 와 **상태** 라는 두 엔터티가 표시 됩니다.  
  
4.  목록에서 **상태** 를 두 번 클릭 합니다. MDS의 **State** 엔터티에 대 한 모든 멤버가 워크시트에 표시 됩니다.  
  
5.  이제 **이름** 에는 **북쪽 Carolina** , **코드** **의 경우에는** 다음 값으로 끝에 행을 추가 합니다. 색 구분에 따라 새 레코드/업데이트된 레코드가 다른 레코드와 구분됩니다.  
  
     ![Excel - 미국에 North Carolina 추가](../../2014/tutorials/media/et-addinganewvalueforstateentityinexcel-02.jpg "Excel - 미국에 North Carolina 추가")  
  
6.  리본에서 **게시** 를 클릭 하 여 변경 내용을 MDS에 게시 합니다.  
  
     ![Excel - 마스터 데이터 탭의 게시 단추](../../2014/tutorials/media/et-addinganewvalueforstateentityinexcel-03.jpg "Excel - 마스터 데이터 탭의 게시 단추")  
  
7.  **게시 및 주석** 대화 상자에서 **모든 변경 내용에 동일한 주석 사용** 이 선택 되어 있는지 확인 합니다. 여기에서 모든 변경 내용에 대해 단일 주석을 입력할 수 있습니다.  
  
8.  변경 **내용을 검토 하 고 개별적으로 주석 제공** 옵션을 선택 하 여 각 변경 내용에 대 한 주석을 제공 합니다 (이 경우에만).  
  
     ![Excel - 게시 및 주석 달기 대화 상자](../../2014/tutorials/media/et-addinganewvalueforstateentityinexcel-04.jpg "Excel - 게시 및 주석 달기 대화 상자")  
  
9. **게시** 를 클릭 하 여 데이터를 MDS에 게시 합니다.  
  
10. **북쪽 Carolina** 이 있는 행에 대 한 **색 구분** 이 현재 다른 레코드와 **동일 합니다.**  
  
11. **선택 사항:** **마스터 데이터 관리자**에서 **탐색기** 를 사용 하 여 새 멤버 (NC)가 **상태** 엔터티에 추가 되었는지 확인 합니다.  
  
12. Excel에서 아래쪽의 **상태** 워크시트를 마우스 오른쪽 단추로 클릭 하 고 **삭제** 를 클릭 하 여 워크시트를 삭제 합니다. 워크시트를 삭제해도 MDS 서버에서는 데이터가 삭제되지 않습니다.  
  
## <a name="next-step"></a>다음 단계  
 [태스크 9: 마스터 데이터 관리자를 사용하여 파생 계층 만들기](../../2014/tutorials/task-9-creating-a-derived-hierarchy-using-master-data-manager.md)  
  
  
