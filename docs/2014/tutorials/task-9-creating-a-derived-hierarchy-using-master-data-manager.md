---
title: '태스크 9: 마스터 데이터 관리자를 사용 하 여 파생 계층 만들기 | Microsoft Docs'
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 3bd2ec05-933f-4947-b1fe-c9226961eb7d
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 6b3bc7d64e10e4803a2c2c069ab4b21cf8b139ec
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56039334"
---
# <a name="task-9-creating-a-derived-hierarchy-using-master-data-manager"></a>태스크 9: 마스터 데이터 관리자를 사용하여 파생 계층 만들기
  이 작업에서는 마스터 데이터 관리자를 사용하여 파생 계층을 만듭니다. 이 파생된 계층의 도메인 기반 특성 관계에서 파생 됩니다 합니다 **공급 업체** 하 고 **상태** 엔터티.  
  
1.  기본 페이지로 전환 **마스터 데이터 관리자** 를 클릭 하 여 **SQL Server 2012 Master Data Services** 페이지의 맨 위에 있는 합니다.  
  
2.  **관리 작업** 섹션에서 **시스템 관리** 를 클릭합니다.  
  
3.  마우스로 가리키면 **관리** 메뉴를 클릭 **파생 계층**합니다.  
  
     ![관리 메뉴-선택한 파생된 계층](../../2014/tutorials/media/et-creatingaderivedhierarchyusingmdm-01.jpg "메뉴-선택한 파생된 계층 관리")  
  
4.  클릭 **파생 계층 추가 (+)** 도구 모음 단추입니다.  
  
     ![파생된 계층 추가 단추](../../2014/tutorials/media/et-creatingaderivedhierarchyusingmdm-02.jpg "파생된 계층 추가 단추")  
  
5.  형식 **SuppliersInState** 에 대 한 합니다 **파생 계층 이름**합니다.  
  
6.  클릭 **저장할** 도구 모음 단추입니다.  
  
     ![저장 파생 계층 구조 단추](../../2014/tutorials/media/et-creatingaderivedhierarchyusingmdm-03.jpg "저장 파생 계층 구조 단추")  
  
7.  끌기 **공급 업체** 에서 **사용 가능한 수준: SuppliersInState** 에 **현재 수준: SuppliersInState**.  
  
     ![사용 가능한 엔터티 및 계층을 현재 수준](../../2014/tutorials/media/et-creatingaderivedhierarchyusingmdm-04.jpg "사용 가능한 엔터티 및 계층을 현재 수준")  
  
8.  끌기 **상태** 에서 **사용 가능한 수준: SuppliersInState** 에 **현재 수준: SuppliersInState**. 화면에 **현재 수준** 다음 그림에 나와 있는 것 처럼 합니다.  
  
     ![현재 수준 및 파생된 계층의 미리 보기](../../2014/tutorials/media/et-creatingaderivedhierarchyusingmdm-05.jpg "현재 수준 및 파생된 계층의 미리 보기")  
  
9. 에 **미리 보기** 창 확장 **NY {New York}** 이전 이미지에 표시 된 대로 공급자가 해당 상태를 확인 해야 합니다.  
  
10. 기본 페이지로 전환 **마스터 데이터 관리자** 를 클릭 하 여 **SQL Server 2012 Master Data Services** 페이지의 맨 위에 있는 합니다.  
  
11. **탐색기**를 클릭합니다.  
  
12. 마우스로 가리키면 **계층 구조** 클릭 **파생: SuppliersInState**합니다.  
  
     ![계층-Derived: SuppliersInState 메뉴](../../2014/tutorials/media/et-creatingaderivedhierarchyusingmdm-06.jpg "계층-Derived: SuppliersInState 메뉴")  
  
13. 클릭 **상태** 에서 노드를 **트리 보기** 오른쪽 창에서 해당 지역의 공급자 표시 되어야 합니다.  
  
     ![파생 계층 탐색기에서](../../2014/tutorials/media/et-creatingaderivedhierarchyusingmdm-07.jpg "파생 계층 탐색기에서")  
  
## <a name="next-step"></a>다음 단계  
 [5단원: 정리 및 일치 하는 SSIS를 사용 하 여 자동화](../../2014/tutorials/lesson-5-automating-the-cleansing-and-matching-using-ssis.md)  
  
  
