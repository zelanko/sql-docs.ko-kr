---
title: '작업 5: Excel에서 도메인 기반 특성 만들기 | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 07cbc624-2c6b-4568-96e4-f18663a05d80
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 1a2826bb0c9b542837e05b7f600c9ce7d934fd4e
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56031604"
---
# <a name="task-5-creating-a-domain-based-attribute-from-excel"></a>작업 5: Excel에서 도메인 기반 특성 만들기
  변환 하면이 태스크에서는 **상태** 특성을 **공급 업체** 엔터티를 **도메인 기반 특성**. State 특성 도메인 기반 단일 하 라는 새로운 엔터티가 MDS에 게시를 구성 하 고 나면 **상태** 열의 모든 값을 사용 하 여 MDS 서버에 만들어집니다 하며 **상태** 특성을 **공급 업체** 엔터티를 값으로 채워집니다 합니다 **상태** 엔터티. 이제는 **공급 업체** 모델에는 두 개의 엔터티가 있어야 합니다. **공급 업체** 및 **상태** 여기서는 **상태** 특성을 **공급 업체** 엔터티가 종속 된 도메인 기반 특성을 **상태** 엔터티.  
  
1.  전환할 **Excel** 포함 된 창을 **Cleansed and Matched Suppliers.xlsx** 엽니다.  
  
2.  클릭 **새로 고침** MDS에서 최신 업데이트를 받도록 리본의 단추입니다. 선택적 수행한 경우 레코드가 두 개 더 표시 됩니다 **작업 4**합니다.  
  
3.  열 이름을 클릭 **상태** (셀 **I1**)에 **머리글 행**합니다.  
  
     ![Excel-특성 속성 단추](../../2014/tutorials/media/et-creatingadomainbasedattributefromexcel-01.jpg "Excel-특성 속성 단추")  
  
4.  클릭 **특성 속성** 리본 메뉴에 있습니다.  
  
5.  에 **특성 속성** 대화 상자에서 **제약 된 목록 (도메인 기반)** 에 대 한 합니다 **특성 유형**합니다.  
  
6.  형식 **상태** 에 대 한 합니다 **새 엔터티 이름** 클릭 **확인**합니다.  
  
     ![Excel-특성 속성 대화 상자](../../2014/tutorials/media/et-creatingadomainbasedattributefromexcel-02.jpg "Excel-특성 속성 대화 상자")  
  
7.  이제 Excel에서 표시 되어야 **아래쪽 화살표** 의 값을 클릭할 때 합니다 **상태** 열입니다. 필요에 따라 드롭 다운 목록을 사용해서 값을 변경할 수 있습니다.  
  
     ![Excel-상태를 사용 하 여 목록 드롭다운](../../2014/tutorials/media/et-creatingadomainbasedattributefromexcel-03.jpg "Excel-상태를 사용 하 여 목록 드롭다운")  
  
## <a name="next-step"></a>다음 단계  
 [태스크 6: 마스터 데이터 관리자를 사용 하 여 도메인 기반 특성이 생성 되었는지 확인](../../2014/tutorials/task-6-verify-domain-based-attribute-master-data-manager.md)  
  
  
