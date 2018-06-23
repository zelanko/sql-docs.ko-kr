---
title: '태스크 2 (선택 사항): 마스터 데이터 관리자를 사용 하 여 MDS 구독 뷰 만들기 | Microsoft Docs'
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
ms.assetid: f3da8219-e0cb-4848-95ca-285a76ec1ba9
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 4883d4f5c7bef05de9625c2fcb7bac235c0306e7
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36186211"
---
# <a name="task-2-optional-creating-a-mds-subscription-view-using-master-data-manager"></a>태스크 2(선택 사항): 마스터 데이터 관리자를 사용하여 MDS 구독 뷰 만들기
  이 태스크에서는 노출 하는 구독 뷰를 만든는 **공급 업체** 의 엔터티에 **공급 업체** 를 다른 응용 프로그램 모델입니다. 현재 버전의 자습서에서는 이 뷰를 사용하지 않습니다.  
  
1.  기본 페이지로 전환 **마스터 데이터 관리자** ([http://localhost/MDS](http://localhost/MDS))를 클릭 하 여 **SQL Server 2012 Master Data Services** 위쪽에 있습니다.  
  
2.  클릭 **통합 관리**합니다.  
  
3.  클릭 **뷰 만들기** 메뉴 모음에서 합니다.  
  
     ![새 구독 보기 단추 추가](../../2014/tutorials/media/et-creatingamdssubscriptionviewusingmdm-01.jpg "새 구독 보기 단추 추가")  
  
4.  클릭 **+ (더하기)** 구독 뷰를 만들려면 도구 모음의 아이콘을 합니다.  
  
5.  에 **구독 뷰 만들기** 창, 형식 **Suppliers** 에 대 한 **구독 뷰 이름**합니다.  
  
6.  **모델** 에 대해 **Suppliers**를 선택합니다.  
  
7.  **버전** 에 대해 **VERSION_1**을 선택합니다.  
  
8.  선택 **공급 업체** 에 대 한 **엔터티**합니다.  
  
9. 선택 **리프 멤버** 에 대 한 **형식**합니다.  
  
     ![구독 뷰 저장 단추](../../2014/tutorials/media/et-creatingamdssubscriptionviewusingmdm-02.jpg "구독 뷰 저장 단추")  
  
10. 클릭 **저장** 구독 뷰를 저장 하려면 도구 모음에 있습니다. 이 작업에서 SQL Server 명명 된 뷰를 만듭니다 **Suppliers**합니다. 이 뷰는 SSMS(SQL Server Management Studio)를 사용하여 확인할 수 있습니다.  
  
## <a name="next-step"></a>다음 단계  
 [작업 3 &#40;선택적&#41;: 구독 뷰 검토](task-3-optional-reviewing-the-subscription-views.md)  
  
  