---
title: '태스크 10: 참조 데이터 서비스를 사용 하도록 복합 도메인 구성 | Microsoft Docs'
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.topic: conceptual
ms.assetid: 752eefde-8b87-4f54-878e-9963ccbadc8e
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 8541ea7446fe80bf6bb0fd5f1bc3e80285912ffe
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53370025"
---
# <a name="task-10-configuring-composite-domain-to-use-reference-data-service"></a>태스크 10: 참조 데이터 서비스를 사용하도록 복합 도메인 구성
  이 태스크에서는 구성 합니다 **Address Validation** 사용 하도록 복합 도메인의 **Melissa Data-Address Check** 서비스. 런타임에 정리 작업을 수행하는 동안 DQS는 Address Validation 도메인에 있는 도메인 값을 정리하도록 이 서비스에 전달합니다. 참조 [참조 데이터에 도메인/복합 도메인 매핑](https://msdn.microsoft.com/library/hh213030.aspx) 대 한 자세한 내용은 합니다.  
  
1.  기본 페이지에서 **DQS 클라이언트**, 클릭 **Suppliers (Domain Management)** 아래의 **최근 기술 자료** 시작 하는 **도메인 관리**페이지.  
  
2.  선택 합니다 **Address Validation** 복합 도메인에는 **도메인 목록을**합니다.  
  
3.  오른쪽 창에서 전환 하는 **참조 데이터** 탭 합니다.  
  
     ![참조 데이터 탭](../../2014/tutorials/media/et-configuringcdtouserds-01.jpg "참조 데이터 탭")  
  
4.  클릭 **찾아보기** 도구 모음 단추입니다.  
  
5.  에 **온라인 참조 데이터 공급자 카탈로그** 대화 상자에서 **확인란** 옆에 **Melissa Data-Address Check**합니다.  
  
     ![Melissa Data-Address Check 선택](../../2014/tutorials/media/et-configuringcdtouserds-02.jpg "Melissa Data-Address Check 선택")  
  
6.  오른쪽 창에서에 **스키마** 섹션에서 **Address Line** 도메인에는 **Address Line (M)** 드롭 다운 목록을 사용 하 여 스키마 항목.  
  
     ![도메인에 RDS 스키마 항목 매핑](../../2014/tutorials/media/et-configuringcdtouserds-03.jpg "도메인에 RDS 스키마 항목 매핑")  
  
7.  클릭 **스키마 항목 추가 (+)** 목록의 항목을 만들려면 도구 모음의 단추입니다.  
  
     ![스키마 항목 도구 모음 단추 추가](../../2014/tutorials/media/et-configuringcdtouserds-04.jpg "스키마 항목 도구 모음 단추를 추가 합니다.")  
  
8.  다음 그림에 표시된 것처럼 드롭 다운 목록을 사용해서 다음 DQS 도메인을 매핑합니다.  
  
     ![도메인에 RDS 스키마 항목 매핑](../../2014/tutorials/media/et-configuringcdtouserds-05.jpg "도메인에 RDS 스키마 항목 매핑")  
  
9. **확인** 을 클릭하여 대화 상자를 닫습니다.  
  
## <a name="next-step"></a>다음 단계  
 [태스크 11: 기술 자료 게시](../../2014/tutorials/task-11-publishing-the-knowledge-base.md)  
  
  
