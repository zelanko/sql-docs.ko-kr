---
title: '태스크 9: 마스터 데이터 관리자을 사용 하 여 파생 계층 만들기 | Microsoft Docs'
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 3bd2ec05-933f-4947-b1fe-c9226961eb7d
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 7cb2f12115e3fe743c49c2f7e69f765da4501ba2
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "65489538"
---
# <a name="task-9-creating-a-derived-hierarchy-using-master-data-manager"></a>태스크 9: 마스터 데이터 관리자를 사용하여 파생 계층 만들기
  이 작업에서는 마스터 데이터 관리자를 사용하여 파생 계층을 만듭니다. 이 파생 계층은 **공급자** 와 **상태** 엔터티 간의 도메인 기반 특성 관계에서 파생 됩니다.  
  
1.  페이지 맨 위에 있는 **SQL Server 2012 MDS(Master Data Services)** 를 클릭 하 여 **마스터 데이터 관리자** 의 기본 페이지로 전환 합니다.  
  
2.  **관리 작업** 섹션에서 **시스템 관리** 를 클릭합니다.  
  
3.  메뉴 모음에서 **관리** 위로 마우스를 가져가서 **파생 계층**을 클릭 합니다.  
  
     ![관리 메뉴 - 선택한 파생 계층](../../2014/tutorials/media/et-creatingaderivedhierarchyusingmdm-01.jpg "관리 메뉴 - 선택한 파생 계층")  
  
4.  도구 모음에서 **파생 계층 추가 (+)** 단추를 클릭 합니다.  
  
     ![파생 계층 추가 단추](../../2014/tutorials/media/et-creatingaderivedhierarchyusingmdm-02.jpg "파생 계층 추가 단추")  
  
5.  **파생 계층 이름**에 **SuppliersInState** 을 입력 합니다.  
  
6.  도구 모음에서 **저장** 단추를 클릭 합니다.  
  
     ![파생 계층 저장 단추](../../2014/tutorials/media/et-creatingaderivedhierarchyusingmdm-03.jpg "파생 계층 저장 단추")  
  
7.  **공급 업체** 를 **사용 가능한 수준: SuppliersInState** 에서 **현재 수준: SuppliersInState**로 끕니다.  
  
     ![현재 수준에 사용 가능한 엔터티 및 계층](../../2014/tutorials/media/et-creatingaderivedhierarchyusingmdm-04.jpg "현재 수준에 사용 가능한 엔터티 및 계층")  
  
8.  **사용 가능한 수준: SuppliersInState** 에서 **현재 수준: SuppliersInState**로 **상태** 를 끕니다. 화면에는 다음 그림과 같이 **현재 수준이** 있어야 합니다.  
  
     ![현재 수준 및 파생 계층의 미리 보기](../../2014/tutorials/media/et-creatingaderivedhierarchyusingmdm-05.jpg "현재 수준 및 파생 계층의 미리 보기")  
  
9. **미리 보기** 창에서 사용자 **{뉴욕}** 을 (를) 확장 하면 이전 이미지에 표시 된 것 처럼 해당 상태에서 하나의 공급자가 표시 됩니다.  
  
10. 페이지 맨 위에 있는 **SQL Server 2012 MDS(Master Data Services)** 를 클릭 하 여 **마스터 데이터 관리자** 의 기본 페이지로 전환 합니다.  
  
11. **탐색기**를 클릭합니다.  
  
12. **계층** 위로 마우스를 이동 하 고 **파생: SuppliersInState**를 클릭 합니다.  
  
     ![계층 - Derived:SuppliersInState 메뉴](../../2014/tutorials/media/et-creatingaderivedhierarchyusingmdm-06.jpg "계층 - Derived:SuppliersInState 메뉴")  
  
13. **트리 뷰에서** 모든 **상태** 노드를 클릭 하면 오른쪽 창에 해당 주 공급자가 표시 됩니다.  
  
     ![탐색기의 파생 계층](../../2014/tutorials/media/et-creatingaderivedhierarchyusingmdm-07.jpg "탐색기의 파생 계층")  
  
## <a name="next-step"></a>다음 단계  
 [5단원: SSIS를 사용하여 정리 및 일치 자동화](../../2014/tutorials/lesson-5-automating-the-cleansing-and-matching-using-ssis.md)  
  
  
