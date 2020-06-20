---
title: '태스크 5: Excel에서 도메인 기반 특성 만들기 | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 07cbc624-2c6b-4568-96e4-f18663a05d80
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 6f7287091ddd64ef9df1c63706a2f562feed4a5d
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "84999672"
---
# <a name="task-5-creating-a-domain-based-attribute-from-excel"></a>태스크 5: Excel에서 도메인 기반 특성 만들기
  이 태스크에서는 **공급자** 엔터티의 **State** 특성을 **도메인 기반 특성**으로 변환 합니다. State 특성을 도메인 기반으로 구성한 후 MDS에 게시 하면 **상태** 라는 새 엔터티가 열의 모든 값을 사용 하 여 mds 서버에 생성 되 고 **공급자** 엔터티의 **state** 특성은 **state** 엔터티의 값으로 채워집니다. 이제 **Suppliers** **모델에** **는 공급자 엔터티의** **state** 특성과 **state 엔터티에 종속** 된 도메인 기반 **특성이 있는 두** 개의 엔터티가 있어야 합니다.  
  
1.  **정리 하 고 일치** 하는 Suppliers.xlsx열어 놓은 **Excel** 창으로 전환 합니다.  
  
2.  리본에서 **새로 고침** 단추를 클릭 하 여 MDS에서 최신 업데이트를 가져옵니다. 선택적 **작업 4**를 수행한 경우에는 두 개 이상의 레코드가 표시 됩니다.  
  
3.  **머리글 행**에서 열 이름 **상태** ( **I1**셀)를 클릭 합니다.  
  
     ![Excel - 특성 속성 단추](../../2014/tutorials/media/et-creatingadomainbasedattributefromexcel-01.jpg "Excel - 특성 속성 단추")  
  
4.  리본에서 **특성 속성** 을 클릭 합니다.  
  
5.  **특성 속성** 대화 상자에서 **특성 유형에**대 한 **제한 목록 (도메인 기반)** 을 선택 합니다.  
  
6.  **새 엔터티 이름** 에 **상태** 를 입력 하 고 **확인**을 클릭 합니다.  
  
     ![Excel - 특성 속성 대화 상자](../../2014/tutorials/media/et-creatingadomainbasedattributefromexcel-02.jpg "Excel - 특성 속성 대화 상자")  
  
7.  이제 Excel에서는 **상태** 열에서 값을 클릭 하면 **아래쪽 화살표가** 표시 됩니다. 필요에 따라 드롭 다운 목록을 사용해서 값을 변경할 수 있습니다.  
  
     ![Excel - 상태가 있는 드롭다운 목록](../../2014/tutorials/media/et-creatingadomainbasedattributefromexcel-03.jpg "Excel - 상태가 있는 드롭다운 목록")  
  
## <a name="next-step"></a>다음 단계  
 [태스크 6: 마스터 데이터 관리자를 사용하여 도메인 기반 특성이 생성되었는지 확인](../../2014/tutorials/task-6-verify-domain-based-attribute-master-data-manager.md)  
  
  
