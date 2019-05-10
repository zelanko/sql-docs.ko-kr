---
title: '태스크 2(선택 사항): 마스터 데이터 관리자를 사용 하 여 MDS 구독 뷰 만들기 | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: f3da8219-e0cb-4848-95ca-285a76ec1ba9
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: e6cbed42d059714dde1c82dbb50edf8ccc1dd65b
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65484720"
---
# <a name="task-2-optional-creating-a-mds-subscription-view-using-master-data-manager"></a>태스크 2(선택 사항): 마스터 데이터 관리자를 사용하여 MDS 구독 뷰 만들기
  이 태스크에서는 노출 구독 뷰를 만든 합니다 **공급 업체** 에서 엔터티를 **공급 업체** 다른 응용 프로그램에 모델. 현재 버전의 자습서에서는 이 뷰를 사용하지 않습니다.  
  
1.  기본 페이지로 전환 **마스터 데이터 관리자** ([http://localhost/MDS](http://localhost/MDS))를 클릭 하 여 **SQL Server 2012 Master Data Services** 맨 위에 있는 합니다.  
  
2.  클릭 **통합 관리**합니다.  
  
3.  클릭 **뷰 만들기** 메뉴 모음에서.  
  
     ![새 구독 뷰 단추 추가](../../2014/tutorials/media/et-creatingamdssubscriptionviewusingmdm-01.jpg "새 구독 뷰 단추 추가")  
  
4.  클릭 **+ (더하기)** 구독 뷰를 만들어 도구 모음에서 아이콘입니다.  
  
5.  에 **구독 뷰 만들기** 창, 형식 **Suppliers** 에 대 한 **구독 뷰 이름이**합니다.  
  
6.  **모델** 에 대해 **Suppliers**를 선택합니다.  
  
7.  **버전** 에 대해 **VERSION_1**을 선택합니다.  
  
8.  선택 **공급 업체** 에 대 한 **엔터티**합니다.  
  
9. 선택 **리프 멤버** 에 대 한 **형식**합니다.  
  
     ![구독 뷰 저장 단추](../../2014/tutorials/media/et-creatingamdssubscriptionviewusingmdm-02.jpg "구독 뷰 저장 단추")  
  
10. 클릭 **저장할** 구독 뷰를 저장 하려면 도구 모음에서. 이 작업에서 SQL Server 명명 된 뷰를 만듭니다 **공급 업체**합니다. 이 뷰는 SSMS(SQL Server Management Studio)를 사용하여 확인할 수 있습니다.  
  
## <a name="next-step"></a>다음 단계  
 [작업 3 &#40;선택적&#41;: 구독 뷰 검토](task-3-optional-reviewing-the-subscription-views.md)  
  
  
