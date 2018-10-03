---
title: '작업 1: 기술 자료 및 도메인 만들기 | Microsoft Docs'
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.topic: conceptual
ms.assetid: 7d74a60b-8933-4038-bcbb-4e9dcc4f70e9
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 1222d6d217c004790336a6a234d7f52154e148ba
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48132442"
---
# <a name="task-1-creating-a-knowledge-base-and-domains"></a>태스크 1: 기술 자료 및 도메인 만들기
  이 작업을 만듭니다는 **공급 업체** 기술 자료 및 데이터 정리 및 일치 하는 데이터가 중복 제거 하는 데 사용 되는 도메인을 만듭니다.  
  
1.  시작할 **Data Quality 클라이언트**합니다. 클릭 **시작**를 가리키고 **모든 프로그램**, 클릭 **Microsoft SQL Server 2012**, 클릭 **Data Quality Services**, 클릭하고 **Data Quality 클라이언트**합니다.  
  
2.  에 **서버에 연결** 대화 상자에서 DQS 설치 되 고 클릭 하는 데이터베이스 서버 인스턴스를 선택 **Connect**합니다.  
  
     ![서버에 연결 대화 상자](../../2014/tutorials/media/et-creatingaknowledgebaseanddomains-01.jpg "서버에 연결 대화 상자")  
  
3.  Data Quality 클라이언트에서 홈 페이지에는 **기술 자료 관리** 창 클릭 **새 기술 자료**합니다.  
  
     ![기술 자료 관리-새 KB](../../2014/tutorials/media/et-creatingaknowledgebaseanddomains-02.jpg "기술 자료 관리-새 KB")  
  
4.  입력 **공급 업체** 에 대 한 **이름** 기술 자료입니다.  
  
     ![새 기술 자료-도메인 관리](../../2014/tutorials/media/et-creatingaknowledgebaseanddomains-03.jpg "새 기술 자료-도메인 관리")  
  
5.  있는지 확인 **기술 자료 만들기** 필드 설정 됩니다 **None** 만드는 것 이므로 합니다 **공급 업체** 부터 기술 자료.  
  
6.  확인 **도메인 관리** 가 선택 합니다 **활동** 클릭 **다음**합니다. 도메인 관리 작업에서는 기술 자료에 도메인을 만들고 관리할 수 있습니다.  
  
7.  에 **도메인 관리** 창에서 클릭 **도메인 만들기** 도메인을 만들려면 도구 모음 단추입니다.  
  
     ![도메인 만들기 도구 모음 단추](../../2014/tutorials/media/et-creatingaknowledgebaseanddomains-04.jpg "도메인 만들기 도구 모음 단추")  
  
8.  에 **도메인 만들기** 대화 상자에서 **Supplier ID** 에 대 한 합니다 **도메인 이름**, 클릭 **확인**합니다.  
  
     ![도메인 만들기 대화 상자](../../2014/tutorials/media/et-creatingaknowledgebaseanddomains-05.jpg "도메인 만들기 대화 상자")  
  
9. 이전 단계를 반복해서 다음 도메인을 모두 기본 설정으로 만듭니다. 자습서를 단순하게 유지 하려면 설정 합니다 **데이터 형식** 으로 모든 도메인의 **문자열**. 허용되는 다른 데이터 형식은 Integer, Decimal 및 Date입니다. 경우는 **선행 값 사용** 옵션을 선택된 하면 (기본값), 모든 동의어 출력 동의어 그룹의 선행 값으로 바뀝니다. 설정 **문자열 정규화** 옵션 (기본값) 도메인 값의 특수 문자를 제거 합니다. 합니다 **출력 형식** 옵션을 사용 하면 도메인의 데이터 값이 출력 될 때 적용 되는 서식을 선택 합니다. 선택 **맞춤법 검사기 사용** (기본값) 도메인을 채울 때 모든 문자열 값에 대해 맞춤법 검사기를 실행 합니다. 합니다 **언어** 설정의 언어 버전을 지정 합니다 **맞춤법 검사기** 적용 하려는. 선택 **구문 오류 알고리즘 사용 안 함** 문자열 값의 구문 오류를 확인 하지 않고 도메인을 채우는 합니다. 참조 [도메인 만들기](http://msdn.microsoft.com/library/hh510401.aspx) 대 한 자세한 내용은 MSDN 라이브러리의 항목입니다.  
  
    -   Supplier Name  
  
    -   Contact Email  
  
    -   Address Line  
  
    -   City  
  
    -   State  
  
    -   Country  
  
    -   Zip  
  
## <a name="next-step"></a>다음 단계  
 [태스크 2: 도메인 값을 수동으로 추가](../../2014/tutorials/task-2-adding-domain-values-manually.md)  
  
  
