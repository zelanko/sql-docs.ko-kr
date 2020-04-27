---
title: '작업 1: 기술 자료 및 도메인 만들기 | Microsoft Docs'
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 7d74a60b-8933-4038-bcbb-4e9dcc4f70e9
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 79edd8566f2b3c9b586bc8c8815e1d9bc586fb05
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "65481243"
---
# <a name="task-1-creating-a-knowledge-base-and-domains"></a>태스크 1: 기술 자료 및 도메인 만들기
  이 태스크에서는 **Suppliers** 기술 자료를 만들고 데이터를 정리 하 고 데이터를 일치 시켜 중복 항목을 제거 하는 데 사용 되는 도메인을 만듭니다.  
  
1.  **Data Quality Client**를 시작 합니다. **시작**을 클릭 하 고 **모든 프로그램**을 가리킨 다음 **Microsoft SQL Server 2012**를 클릭 하 고 **Data Quality Services**를 클릭 한 다음 **Data Quality Client**를 클릭 합니다.  
  
2.  **서버에 연결** 대화 상자에서 DQS가 설치 된 데이터베이스 서버 인스턴스를 선택 하 고 **연결**을 클릭 합니다.  
  
     ![서버에 연결 대화 상자](../../2014/tutorials/media/et-creatingaknowledgebaseanddomains-01.jpg "서버에 연결 대화 상자")  
  
3.  Data Quality Client 홈 페이지의 **기술 자료 관리** 창에서 **새 기술 자료**를 클릭 합니다.  
  
     ![기술 자료 관리 - 새 KB](../../2014/tutorials/media/et-creatingaknowledgebaseanddomains-02.jpg "기술 자료 관리 - 새 KB")  
  
4.  기술 자료의 **이름** 으로 **Suppliers** 를 입력 합니다.  
  
     ![새 기술 자료 - 도메인 관리](../../2014/tutorials/media/et-creatingaknowledgebaseanddomains-03.jpg "새 기술 자료 - 도메인 관리")  
  
5.  **Suppliers** 기술 자료를 처음부터 만들기 때문에 **기술 자료 만들기** 필드가 **없음** 으로 설정 되어 있는지 확인 합니다.  
  
6.  **활동** 에 대해 **도메인 관리** 가 선택 되어 있는지 확인 하 고 **다음**을 클릭 합니다. 도메인 관리 작업에서는 기술 자료에 도메인을 만들고 관리할 수 있습니다.  
  
7.  도메인 **관리** 창 **에서 도메인 만들기 도구 모음** 단추를 클릭 하 여 도메인을 만듭니다.  
  
     ![도메인 만들기 도구 모음 단추](../../2014/tutorials/media/et-creatingaknowledgebaseanddomains-04.jpg "도메인 만들기 도구 모음 단추")  
  
8.  **도메인 만들기** 대화 상자에서 **도메인 이름**에 대 한 **공급자 ID** 를 입력 하 고 **확인**을 클릭 합니다.  
  
     ![도메인 만들기 대화 상자](../../2014/tutorials/media/et-creatingaknowledgebaseanddomains-05.jpg "도메인 만들기 대화 상자")  
  
9. 이전 단계를 반복해서 다음 도메인을 모두 기본 설정으로 만듭니다. 자습서를 간단 하 게 유지 하려면 모든 도메인의 **데이터 형식을** **문자열로**설정 합니다. 허용되는 다른 데이터 형식은 Integer, Decimal 및 Date입니다. **선행 값 사용** 옵션을 선택 하면 (기본값) 모든 동의어가 출력에서 동의어 그룹의 선행 값으로 바뀝니다. **문자열 정규화** 옵션 (기본값)을 설정 하면 도메인 값에서 모든 특수 문자를 제거 합니다. **출력 형식** 옵션을 사용 하 여 도메인의 데이터 값이 출력 될 때 적용 되는 서식을 선택할 수 있습니다. 도메인을 채울 때 모든 문자열 값에 대해 맞춤법 검사기를 실행 하려면 **맞춤법 검사기 사용** (기본값)을 선택 합니다. **언어** 설정은 적용 하려는 **맞춤법 검사기** 의 언어 버전을 지정 합니다. 구문 오류에 대 한 문자열 값을 검사 하지 않고 도메인을 채우려면 **구문 오류 알고리즘 사용 안 함** 을 선택 합니다. 자세한 내용은 MSDN 라이브러리에서 [도메인 만들기](https://msdn.microsoft.com/library/hh510401.aspx) 항목을 참조 하세요.  
  
    -   Supplier Name  
  
    -   담당자 이메일  
  
    -   Address Line  
  
    -   City  
  
    -   시스템 상태  
  
    -   국가  
  
    -   Zip  
  
## <a name="next-step"></a>다음 단계  
 [태스크 2: 도메인 값을 수동으로 추가](../../2014/tutorials/task-2-adding-domain-values-manually.md)  
  
  
