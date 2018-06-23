---
title: '태스크 5: Excel에서 도메인 기반 특성 만들기 | Microsoft Docs'
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
ms.topic: article
ms.assetid: 07cbc624-2c6b-4568-96e4-f18663a05d80
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 5e7a8dda16d8f513b2c4b07b9f41712be806b8a9
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36172073"
---
# <a name="task-5-creating-a-domain-based-attribute-from-excel"></a>태스크 5: Excel에서 도메인 기반 특성 만들기
  변환 하면이 작업에서는 **상태** 특성에는 **공급 업체** 엔터티는 **도메인 기반 특성**합니다. 도메인 기반 하나의 라는 새로운 엔터티가 MDS에 게시 하는 State 특성을 구성 하 고 나면 **상태** 열의 모든 값을 사용해 서 MDS 서버에 생성 됩니다 및 **상태** 특성에는 **공급 업체** 엔터티의 값으로 채워집니다는 **상태** 엔터티. 이제는 **Suppliers** 모델에 두 개의 엔터티가 있어야 합니다.: **공급 업체** 및 **상태** 여기서는 **상태** 특성에는  **공급 업체** 엔터티는 도메인 기반 특성에 따라 달라 지 **상태** 엔터티.  
  
1.  로 전환 **Excel** 있는 창의 **Cleansed and Matched Suppliers.xlsx** 엽니다.  
  
2.  클릭 **새로 고침** MDS에서 최신 업데이트를 리본에서 단추입니다. 선택적 수행한 경우 레코드가 두 개 더 나타납니다 **작업 4**합니다.  
  
3.  열 이름을 클릭 **상태** (셀 **I1**)에 **머리글 행**합니다.  
  
     ![Excel-특성 속성 단추](../../2014/tutorials/media/et-creatingadomainbasedattributefromexcel-01.jpg "Excel-특성 속성 단추")  
  
4.  클릭 **특성 속성** 리본 메뉴에 있습니다.  
  
5.  에 **특성 속성** 대화 상자에서 **제약 된 목록 (도메인 기반)** 에 대 한는 **특성 유형**합니다.  
  
6.  형식 **상태** 에 대 한는 **새 엔터티 이름** 클릭 **확인**합니다.  
  
     ![Excel-특성 속성 대화 상자](../../2014/tutorials/media/et-creatingadomainbasedattributefromexcel-02.jpg "Excel-특성 속성 대화 상자")  
  
7.  이제 Excel에서 표시 되어야 **아래쪽 화살표** 에 있는 값을 클릭할 때는 **상태** 열입니다. 필요에 따라 드롭 다운 목록을 사용해서 값을 변경할 수 있습니다.  
  
     ![Excel-드롭다운 목록 상태와](../../2014/tutorials/media/et-creatingadomainbasedattributefromexcel-03.jpg "Excel-드롭다운 목록 상태는")  
  
## <a name="next-step"></a>다음 단계  
 [태스크 6: 마스터 데이터 관리자를 사용하여 도메인 기반 특성이 생성되었는지 확인](../../2014/tutorials/task-6-verify-domain-based-attribute-master-data-manager.md)  
  
  