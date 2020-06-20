---
title: '태스크 7: 데이터 흐름에 DQS 정리 변환 추가 | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 0b749c71-dfb6-493a-804f-600290d46eef
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 0978452104eb9a55d49dfa9f851ef7578489db26
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85006478"
---
# <a name="task-7-adding-dqs-cleansing-transform-to-the-data-flow"></a>태스크 7: Data Flow에 DQS 정리 변환 추가
  이 작업에서는 데이터 흐름에 DQS 정리 변환을 추가하여 DQS를 사용해서 입력 공급자 데이터를 정리합니다. 변환에 대 한 자세한 내용은 **[Dqs 정리 변환](https://msdn.microsoft.com/library/ee677619.aspx)** 을 참조 하세요.  
  
1.  **데이터 흐름** 탭에서 **DQS 정리** 를 마우스 오른쪽 단추로 클릭 하 고 **이름 바꾸기**를 클릭 합니다. **정리 공급자 데이터**를 입력 하 고 **enter**키를 누릅니다.  
  
2.  **Excel 파일에서 공급자 데이터 읽기를**선택 합니다. 파란색 커넥터를 끌어 **공급자 데이터를 정리**합니다. 구성 요소가 이제 연결됩니다.  
  
     ![공급자 데이터 읽기-공급자 데이터 > 정리](../../2014/tutorials/media/et-addingdqscleansingtransformtothedataflow-01.jpg "공급자 데이터 읽기 -> 공급자 데이터 정리")  
  
3.  **공급자 데이터 정리**를 두 번 클릭 합니다.  
  
4.  **Dqs 정리 변환 편집기**에서 **데이터 품질 연결 관리자 드롭다운 목록**옆에 있는 **새로 만들기** 를 클릭 합니다.  
  
5.  **Dqs 정리 연결 관리자** 대화 상자에서 **(local)** 또는 **마침표** (.)를 입력 하 여 로컬 서버에 연결 합니다. 이 단원에서는 DQS가 로컬 서버에 설치되어 있다고 가정합니다.  
  
6.  **연결 테스트** 를 클릭 하 여 DQS 서버에 대 한 연결을 테스트 합니다.  
  
7.  **확인** 을 클릭하여 대화 상자를 닫습니다.  
  
8.  **데이터 품질 기술 자료**에 대해 **Suppliers** 를 선택 합니다.  
  
     ![DQS 정리 변환 편집기 - 공급자 KB](../../2014/tutorials/media/et-addingdqscleansingtransformtothedataflow-02.jpg "DQS 정리 변환 편집기 - 공급자 KB")  
  
9. 위쪽의 **매핑** 탭으로 전환 합니다.  
  
10. **사용 가능한 입력 열**에서 확인란을 선택 하 여 **공급자 이름**, **ContactEmailAddress**, **주소 줄**, **구/군/시** **, 시**/도, **국가**및 **우편** 번호를 선택 합니다.  
  
     ![DQS 정리 변환 편집기 - 매핑](../../2014/tutorials/media/et-addingdqscleansingtransformtothedataflow-03.jpg "DQS 정리 변환 편집기 - 매핑")  
  
11. 아래쪽 창에서 **도메인** 열의 드롭다운 목록을 사용 하 여 이러한 열을 매핑합니다.  
  
    |열|도메인|  
    |------------|------------|  
    |Supplier Name|Supplier Name|  
    |ContactEmailAddress|담당자 이메일|  
    |Address Line|Address Line|  
    |City|City|  
    |시스템 상태|시스템 상태|  
    |국가|국가|  
    |Zip Code|Zip|  
  
12. **확인** 을 클릭 하 여 **DQS 정리 변환 편집기** 대화 상자를 닫습니다.  
  
## <a name="next-step"></a>다음 단계  
 [태스크 8: 분할 정리 출력에 조건부 분할 변환 추가](../../2014/tutorials/task-8-adding-conditional-split-transform-to-split-cleansing-output.md)  
  
  
