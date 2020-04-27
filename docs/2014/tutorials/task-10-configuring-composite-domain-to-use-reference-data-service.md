---
title: '작업 10: 참조 데이터 서비스를 사용 하도록 복합 도메인 구성 | Microsoft Docs'
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 752eefde-8b87-4f54-878e-9963ccbadc8e
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 525e0286d8d82f501981c9e936caca581886b9b4
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "65481234"
---
# <a name="task-10-configuring-composite-domain-to-use-reference-data-service"></a>태스크 10: 참조 데이터 서비스를 사용하도록 복합 도메인 구성
  이 작업에서는 **Melissa 데이터 주소 검사** 서비스를 사용 하도록 **Address Validation** 복합 도메인을 구성 합니다. 런타임에 정리 작업을 수행하는 동안 DQS는 Address Validation 도메인에 있는 도메인 값을 정리하도록 이 서비스에 전달합니다. 자세한 내용은 [참조 데이터에 도메인/복합 도메인 매핑을](https://msdn.microsoft.com/library/hh213030.aspx) 참조 하세요.  
  
1.  **DQS 클라이언트**의 기본 페이지에서 **최근 기술 자료** 아래에 있는 **Suppliers (도메인 관리)** 를 클릭 하 여 **도메인 관리** 페이지를 시작 합니다.  
  
2.  **도메인 목록**에서 **Address Validation** 복합 도메인을 선택 합니다.  
  
3.  오른쪽 창에서 **참조 데이터** 탭으로 전환 합니다.  
  
     ![참조 데이터 탭](../../2014/tutorials/media/et-configuringcdtouserds-01.jpg "참조 데이터 탭")  
  
4.  도구 모음에서 **찾아보기** 단추를 클릭 합니다.  
  
5.  **온라인 참조 데이터 공급자 카탈로그** 대화 상자에서 **Melissa (데이터 주소 확인)** 옆의 **확인란** 을 선택 합니다.  
  
     ![Melissa Data - Address Check 선택](../../2014/tutorials/media/et-configuringcdtouserds-02.jpg "Melissa Data - Address Check 선택")  
  
6.  오른쪽 창의 **스키마** 섹션에서 드롭다운 목록을 사용 하 여 address **Line** 도메인을 **address line (M)** 스키마 항목에 매핑합니다.  
  
     ![도메인에 RDS 스키마 항목 매핑](../../2014/tutorials/media/et-configuringcdtouserds-03.jpg "도메인에 RDS 스키마 항목 매핑")  
  
7.  도구 모음에서 **스키마 항목 추가 (+)** 단추를 클릭 하 여 목록에 항목을 만듭니다.  
  
     ![스키마 항목 추가 도구 모음 단추](../../2014/tutorials/media/et-configuringcdtouserds-04.jpg "스키마 항목 추가 도구 모음 단추")  
  
8.  다음 그림에 표시된 것처럼 드롭 다운 목록을 사용해서 다음 DQS 도메인을 매핑합니다.  
  
     ![도메인에 RDS 스키마 항목 매핑](../../2014/tutorials/media/et-configuringcdtouserds-05.jpg "도메인에 RDS 스키마 항목 매핑")  
  
9. **확인**을 클릭하여 대화 상자를 닫습니다.  
  
## <a name="next-step"></a>다음 단계  
 [태스크 11: 기술 자료 게시](../../2014/tutorials/task-11-publishing-the-knowledge-base.md)  
  
  
