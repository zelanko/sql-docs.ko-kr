---
title: '작업 2(선택 사항): 마스터 데이터 관리자를 사용하여 MDS 구독 보기 만들기 | 마이크로 소프트 문서'
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
ms.openlocfilehash: cc923792adc3fefb5ebaab9e225169648394c71f
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2020
ms.locfileid: "81484713"
---
# <a name="task-2-optional-creating-a-mds-subscription-view-using-master-data-manager"></a>태스크 2(선택 사항): 마스터 데이터 관리자를 사용하여 MDS 구독 뷰 만들기
  이 작업에서는 **공급자** 모델의 **공급자** 엔터티를 다른 응용 프로그램에 노출하는 구독 보기를 만듭니다. 현재 버전의 자습서에서는 이 뷰를 사용하지 않습니다.  
  
1.  상단에 있는 **SQL Server 2012 마스터 데이터 서비스를** 클릭하여 마스터 데이터 **관리자()** `http://localhost/MDS`의 기본 페이지로 전환합니다.  
  
2.  **통합 관리를 클릭합니다.**  
  
3.  메뉴 모음에서 **보기 만들기를** 클릭합니다.  
  
     ![새 구독 뷰 추가 단추](../../2014/tutorials/media/et-creatingamdssubscriptionviewusingmdm-01.jpg "새 구독 뷰 추가 단추")  
  
4.  도구 모음에서 **+(플러스)** 아이콘을 클릭하여 구독 보기를 만듭니다.  
  
5.  구독 **만들기 보기** 창에서 구독 보기 이름에 대한 **공급자를** **입력합니다.**  
  
6.  **모델** 에 대해 **Suppliers**를 선택합니다.  
  
7.  **버전** 에 대해 **VERSION_1**을 선택합니다.  
  
8.  **엔터티에**대한 **공급자를** 선택합니다.  
  
9. **형식에**대한 **리프 멤버를** 선택합니다.  
  
     ![구독 뷰 저장 단추](../../2014/tutorials/media/et-creatingamdssubscriptionviewusingmdm-02.jpg "구독 뷰 저장 단추")  
  
10. 도구 모음에서 **저장을** 클릭하여 구독 보기를 저장합니다. 이 작업은 **공급자라는**SQL Server에서 보기를 만듭니다. 이 뷰는 SSMS(SQL Server Management Studio)를 사용하여 확인할 수 있습니다.  
  
## <a name="next-step"></a>다음 단계  
 [작업 3 &#40;선택적&#41;: 구독 보기 검토](task-3-optional-reviewing-the-subscription-views.md)  
  
  
