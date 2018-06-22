---
title: '태스크 10: 참조 데이터 서비스를 사용 하도록 복합 도메인을 구성 | Microsoft Docs'
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 752eefde-8b87-4f54-878e-9963ccbadc8e
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 2a5d37578ac8336b67201161ef4de59baf90649c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36088740"
---
# <a name="task-10-configuring-composite-domain-to-use-reference-data-service"></a>태스크 10: 참조 데이터 서비스를 사용하도록 복합 도메인 구성
  이 태스크에서는 구성에서 **Address Validation** 사용 하도록 복합 도메인의 **Melissa Data – Address Check** 서비스입니다. 런타임에 정리 작업을 수행하는 동안 DQS는 Address Validation 도메인에 있는 도메인 값을 정리하도록 이 서비스에 전달합니다. 참조 [참조 데이터에 도메인/복합 도메인 지도](http://msdn.microsoft.com/library/hh213030.aspx) 자세한 세부 정보에 대 한 합니다.  
  
1.  기본 페이지에서 **DQS 클라이언트**, 클릭 **Suppliers (Domain Management)** 아래 **최근 기술 자료** 시작 하는 **도메인 관리**페이지.  
  
2.  선택은 **Address Validation** 복합 도메인에는 **도메인 목록이**합니다.  
  
3.  오른쪽 창에서로 전환 하는 **참조 데이터** 탭 합니다.  
  
     ![참조 데이터 탭](../../2014/tutorials/media/et-configuringcdtouserds-01.jpg "참조 데이터 탭")  
  
4.  클릭 **찾아보기** 도구 모음 단추입니다.  
  
5.  에 **온라인 참조 데이터 공급자 카탈로그** 대화 상자에서 **확인란** 옆에 **Melissa Data – Address Check**합니다.  
  
     ![Melissa Data-Address Check 선택](../../2014/tutorials/media/et-configuringcdtouserds-02.jpg "Melissa Data-Address Check 선택")  
  
6.  오른쪽 창에서에 **스키마** 섹션, 지도 **Address Line** 도메인에는 **Address Line (M)** 드롭 다운 목록을 사용 하 여 스키마 항목입니다.  
  
     ![도메인에 RDS 스키마 항목 매핑](../../2014/tutorials/media/et-configuringcdtouserds-03.jpg "도메인에 RDS 스키마 항목 매핑")  
  
7.  클릭 **스키마 항목 추가 (+)** 목록에서 항목을 만들려면 도구 모음 단추입니다.  
  
     ![스키마 항목 도구 모음 단추 추가](../../2014/tutorials/media/et-configuringcdtouserds-04.jpg "스키마 항목 도구 모음 단추 추가")  
  
8.  다음 그림에 표시된 것처럼 드롭 다운 목록을 사용해서 다음 DQS 도메인을 매핑합니다.  
  
     ![도메인에 RDS 스키마 항목 매핑](../../2014/tutorials/media/et-configuringcdtouserds-05.jpg "도메인에 RDS 스키마 항목 매핑")  
  
9. **확인** 을 클릭하여 대화 상자를 닫습니다.  
  
## <a name="next-step"></a>다음 단계  
 [태스크 11: 기술 자료 게시](../../2014/tutorials/task-11-publishing-the-knowledge-base.md)  
  
  