---
title: '작업 1: 기술 자료 및 도메인 만들기 | Microsoft Docs'
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
ms.assetid: 7d74a60b-8933-4038-bcbb-4e9dcc4f70e9
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: beec636f9137802c6651f0c08889acf73000b063
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36181674"
---
# <a name="task-1-creating-a-knowledge-base-and-domains"></a>태스크 1: 기술 자료 및 도메인 만들기
  이 작업을 만듭니다는 **Suppliers** 기술 자료 및 데이터를 정리 및 데이터 일치에 대 한 중복을 제거 하는 데 사용 되는 도메인을 만듭니다.  
  
1.  시작 **데이터 품질 클라이언트**합니다. 클릭 **시작**, 가리킨 **모든 프로그램**, 클릭 **Microsoft SQL Server 2012**, 클릭 **Data Quality Services**, 를클릭한다음 **데이터 품질 클라이언트**합니다.  
  
2.  에 **서버에 연결** 대화 상자에서 데이터베이스 서버 인스턴스는 DQS 설치 되어 있고 클릭 **연결**합니다.  
  
     ![서버에 연결 대화 상자](../../2014/tutorials/media/et-creatingaknowledgebaseanddomains-01.jpg "서버에 연결 대화 상자")  
  
3.  데이터 품질 클라이언트에서 홈 페이지에는 **기술 자료 관리** 창에서 클릭 **새 기술 자료**합니다.  
  
     ![기술 자료 관리-새 KB](../../2014/tutorials/media/et-creatingaknowledgebaseanddomains-02.jpg "기술 자료 관리-새 KB")  
  
4.  입력 **Suppliers** 에 대 한 **이름** 기술 자료의 합니다.  
  
     ![새 기술 자료-도메인 관리](../../2014/tutorials/media/et-creatingaknowledgebaseanddomains-03.jpg "새 기술 자료-도메인 관리")  
  
5.  확인 **기술 자료 만들기** 필드가로 설정 된 **없음** 만드는 것 이므로 **공급 업체** 기술 자료를 처음부터 합니다.  
  
6.  확인 **도메인 관리** 에 대해 선택 된는 **활동** 클릭 **다음**합니다. 도메인 관리 작업에서는 기술 자료에 도메인을 만들고 관리할 수 있습니다.  
  
7.  에 **도메인 관리** 창 클릭 **도메인 만들기** 도메인을 만들려면 도구 모음 단추입니다.  
  
     ![도메인 만들기 도구 모음 단추](../../2014/tutorials/media/et-creatingaknowledgebaseanddomains-04.jpg "도메인 만들기 도구 모음 단추")  
  
8.  에 **도메인 만들기** 대화 상자에서 **Supplier ID** 에 대 한는 **도메인 이름**를 클릭 하 고 **확인**합니다.  
  
     ![도메인 만들기 대화 상자](../../2014/tutorials/media/et-creatingaknowledgebaseanddomains-05.jpg "도메인 만들기 대화 상자")  
  
9. 이전 단계를 반복해서 다음 도메인을 모두 기본 설정으로 만듭니다. 자습서를 간단히 유지 하기 위해 설정 된 **데이터 형식** 으로 모든 도메인의 **문자열**합니다. 허용되는 다른 데이터 형식은 Integer, Decimal 및 Date입니다. 경우는 **선행 값 사용** 옵션을 선택된 (기본값), 모든 동의어 출력 동의어 그룹의 선행 값으로 대체 됩니다. 설정 **문자열 정규화** 도메인 값의 특수 문자를 제거 하는 옵션 (기본값). **출력 형식** 옵션을 사용 하면 도메인의 데이터 값이 출력 될 때 적용 되는 서식을 선택 합니다. 선택 **맞춤법 검사기 사용** (기본값) 도메인을 채울 때 모든 문자열 값에서 맞춤법 검사기를 실행 하도록 합니다. **언어** 설정은의 언어 버전을 지정 된 **맞춤법 검사기** 적용할 합니다. 선택 **구문 오류 알고리즘 사용 안 함** 구문 오류에 대 한 문자열 값을 검사 하지 않고 도메인을 채우는 합니다. 참조 [도메인 만들기](http://msdn.microsoft.com/library/hh510401.aspx) 자세한 내용은 MSDN library의 항목입니다.  
  
    -   Supplier Name  
  
    -   Contact Email  
  
    -   Address Line  
  
    -   City  
  
    -   State  
  
    -   Country  
  
    -   Zip  
  
## <a name="next-step"></a>다음 단계  
 [태스크 2: 도메인 값을 수동으로 추가](../../2014/tutorials/task-2-adding-domain-values-manually.md)  
  
  