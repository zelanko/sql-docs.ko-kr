---
title: '작업 1: 일치 하는 정책을 정의 하 | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 6f89a720-fce5-4f60-bef3-a159bbc9f25c
caps.latest.revision: 6
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 58507594fa2872bc5433b63e0f932d2914291a31
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37282359"
---
# <a name="task-1-defining-a-matching-policy"></a>태스크 1: 일치 정책 정의
  이 작업에서는 규칙이 포함된 일치 정책을 만듭니다. 규칙에는 하나의 필요 조건이 포함 됩니다. **Supplier ID**, 규칙의 다른 도메인을 사용 하려면 먼저 Supplier Id와 일치 해야 함을 의미 합니다. 다른 두 도메인을 사용 하는 규칙: **Supplier Name** 사용 하 여 **유사성** 값으로 설정 **70%** 고 **Contact Email** 사용 하 여  **유사성** 값으로 설정 **30%** 합니다.  
  
1.  기본 페이지에서 **DQS 클라이언트**, 클릭 **오른쪽 화살표** 옆에 **Suppliers** 지식 베이스를 선택한 **일치 정책**합니다.  
  
     ![정책 메뉴 Main에서 일치 하는 페이지](../../2014/tutorials/media/et-definingamatchingpolicy-01.jpg "정책 메뉴 Main에서 일치 하는 페이지")  
  
2.  에 **지도** 페이지에서 **Excel 파일** 에 대 한 **데이터 원본**합니다.  
  
3.  클릭 **찾아보기**, 해당 필터 설정 되어 있는지 확인 **Excel 통합 문서**를 선택 하 고 **Cleansed Supplier List.xls** 정리 작업을 수행한 후 내보낸는 파일입니다.  
  
    > [!NOTE]  
    >  이 작업은 주로 일치 정책을 정의하기 위한 것이기 때문에 이 작업을 마친 후에는 결과를 내보낼 수 없습니다. 다음 단원에서는 일치 작업에 대한 데이터 품질 프로젝트를 만들어서 실행하고 이 일치 정책을 사용해서 공급자 목록에서 중복된 항목을 제거합니다.  
  
4.  지도 **SupplierID** 열을 **Supplier ID** 도메인 **Supplier Name** 열의 **Supplier Name** 도메인  **ContactEmailAddress** 열을 **Contact Email** 도메인입니다. 원본 열은 일치 정책을 정의하는 데 사용할 도메인에 매핑하기만 하면 됩니다. 여기에서는 일치 정책 작업을 위해 Supplier ID, Supplier Name 및 Contact Email 도메인을 사용할 수 있도록 설정합니다.  
  
     ![일치 정책 정의 프로세스의 맵 페이지](../../2014/tutorials/media/et-definingamatchingpolicy-02.jpg "일치 정책 정의 프로세스의 맵 페이지")  
  
5.  클릭 **다음** 이동할 합니다 **일치 정책** 페이지를 정의 합니다 하나의 규칙으로 일치 하는 정책에서.  
  
6.  클릭 **일치 규칙 만들기** 정책에 규칙을 만들려면 도구 모음의 단추입니다.  
  
     ![일치 하는 규칙 도구 모음 단추를 만듭니다](../../2014/tutorials/media/et-definingamatchingpolicy-03.jpg "일치 하는 규칙 도구 모음 단추 만들기")  
  
7.  에 **규칙 세부 정보** 창 오른쪽의 입력 **Remove Duplicate Suppliers** 에 대 한 합니다 **규칙 이름**합니다.  
  
8.  클릭 **새 도메인 요소 추가** 오른쪽 창의 도구 모음에서.  
  
     ![새 도메인 요소 단추 추가 규칙 정보-](../../2014/tutorials/media/et-definingamatchingpolicy-04.jpg "새 도메인 요소 단추 추가 규칙 정보-")  
  
9. 선택 **Supplier ID** 에 대 한 합니다 **도메인** 선택 합니다 **필수 구성 요소** 확인란 합니다. 있음을 **유사성** 로 자동 설정 됩니다 **Exact**합니다. 설정 하 여 **Supplier ID** 으로 **필수 구성 요소**로 지정 하면이 필드의 두 레코드에 대 한 값이 100% 일치를 반환 해야 다른 레코드 없습니다 것으로 간주 되어 일치 하는 항목의 다른 절은 규칙은 무시 됩니다.  
  
     ![중복 공급자 규칙 정의 제거](../../2014/tutorials/media/et-definingamatchingpolicy-05.jpg "중복 공급자 규칙 정의 제거")  
  
10. 클릭 **새 도메인 요소 추가** 다시 도구 모음에서.  
  
11. 선택 **Supplier Name** 도메인 **근사치** 에 대 한 **유사성**, 형식과 **70** 에 대 한는 **가중치**.  여기에서는 공급자 이름이 동일하지 않고 유사하기만 해도 일치하는 것으로 간주되도록 지정합니다. 가중치는 전체 일치 점수에 대한 이 필드 점수의 기여도를 나타냅니다.  
  
12. 이전 두 단계를 반복 추가 **Contact Email** 도메인과 **30** 에 대 한 합니다 **가중치**합니다.  
  
13. **최소 일치 점수** 로 설정 된 **80%**, 값에 표시 되는 **일반** 탭을 **구성** 페이지 **DQS 관리**합니다. 이 점수는 이 임계값 위로만 늘릴 수 있습니다.  
  
14. 있음을 **겹치는 클러스터** 옵션을 선택 합니다. 이 옵션을 사용하면 레코드를 여러 클러스터에 표시할 수 있습니다. 설정을 겹치지 않는 클러스터로 변경하면 공통 레코드를 포함하는 여러 클러스터가 단일 클러스터로 조합됩니다.  
  
15. 합니다 **시작** 이 페이지에서 단추 하면 정책의 각 규칙을 개별적으로 테스트할 반면, 다음 페이지에서 시작 단추를 사용 하면 전체 정책 (모든 규칙 정책에서)를 테스트할 수 있습니다.  
  
16. 클릭 **다음** 으로 전환 합니다 **일치 결과** 페이지입니다.  
  
## <a name="next-step"></a>다음 단계  
 [태스크 2: 일치 정책 테스트 및 게시](../../2014/tutorials/task-2-testing-and-publishing-the-matching-policy.md)  
  
  
