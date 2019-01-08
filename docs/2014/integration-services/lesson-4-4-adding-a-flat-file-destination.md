---
title: '4단계: 플랫 파일 대상 추가 | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: f4088de3-16d8-419c-96a1-a2cd005d0a5b
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: c43885de9e2a6945a8a24263765df8ee8e26920a
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52823377"
---
# <a name="step-4-adding-a-flat-file-destination"></a>4단계: 플랫 파일 대상 추가
  Lookup Currency Key 변환의 오류 출력은 조회 작업에 실패한 모든 데이터 행을 스크립트 변환으로 리디렉션합니다. 발생한 오류에 대한 정보를 보강하기 위해 스크립트 변환은 오류에 대한 설명을 가져오는 스크립트를 실행합니다.  
  
 이 태스크에서는 나중에 처리할 수 있도록 실패한 행에 대한 이러한 모든 정보를 구분된 파일에 저장합니다. 실패한 행을 저장하려면 오류 데이터를 포함할 텍스트 파일에 대해 플랫 파일 연결 관리자를 추가 및 구성하고 플랫 파일 대상을 추가 및 구성해야 합니다. 플랫 파일 대상에서 사용되는 플랫 파일 연결 관리자에 속성을 설정하여 플랫 파일 대상에서 텍스트 파일을 기록하고 형식을 지정하는 방식을 지정할 수 있습니다. 자세한 내용은 [Flat File Connection Manager](connection-manager/file-connection-manager.md) 및 [Flat File Destination](data-flow/flat-file-destination.md)를 참조하세요.  
  
### <a name="to-add-and-configure-a-flat-file-destination"></a>플랫 파일 대상을 추가하고 구성하려면  
  
1.  **데이터 흐름** 탭을 클릭합니다.  
  
2.  **SSIS 도구 상자**에서 **기타**를 확장하고 **플랫 파일 대상** 을 데이터 흐름 디자인 화면에 끌어 놓습니다. **플랫 파일 대상** 을 **Get Error Description** 변환 바로 아래에 배치합니다.  
  
3.  **Get Error Description** 변환을 클릭한 다음 녹색 화살표를 새 **플랫 파일 대상**에 끌어 놓습니다.  
  
4.  **데이터 흐름** 디자인 화면에서 새로 추가한 **플랫 파일 대상** 변환의 **플랫 파일 대상** 을 클릭한 다음 이름을 **Failed Rows**로 변경합니다.  
  
5.  **Failed Rows** 변환을 마우스 오른쪽 단추로 클릭하고 **편집**을 클릭한 다음 **플랫 파일 대상 편집기**에서 **새로 만들기**를 클릭합니다.  
  
6.  **플랫 파일 형식** 대화 상자에서 **구분 기호로 분리됨** 을 선택했는지 확인한 다음 **확인**을 클릭합니다.  
  
7.  에 **플랫 파일 연결 관리자 편집기**를 **연결 관리자 이름** 상자에 입력 `Error Data`합니다.  
  
8.  **플랫 파일 연결 관리자 편집기** 대화 상자에서 **찾아보기**를 클릭한 다음 파일을 저장할 폴더를 찾습니다.  
  
9. 에 **열기** 대화 상자에 대 한 **파일 이름**, 형식 `ErrorOutput.txt`, 클릭 하 고 **열기**합니다.  
  
10. **플랫 파일 연결 관리자 편집기** 대화 상자에서 **로캘** 상자에 영어(미국), **코드 페이지** 에 1252(ANSI - 라틴어 I)가 포함되어 있는지 확인합니다.  
  
11. 옵션 창에서 **열**을 클릭합니다.  
  
     원본 데이터 파일의 열 외에 새로운 열인 ErrorCode, ErrorColumn 및 ErrorDescription이 있는 것을 볼 수 있습니다. 이러한 열은 Lookup Currency Key 변환의 오류 출력 및 Get Error Description 변환의 스크립트에 의해 생성되었으며 해당 열을 사용하여 실패한 행의 원인에 따라 문제를 해결할 수 있습니다.  
  
12. **확인**을 클릭합니다.  
  
13. **플랫 파일 대상 편집기**에서 **파일의 데이터 덮어쓰기** 확인란의 선택을 취소합니다.  
  
     이 확인란의 선택을 취소하면 여러 패키지 실행 시 오류가 계속 발생합니다.  
  
14. **플랫 파일 대상 편집기**에서 **매핑** 을 클릭하여 모든 열이 올바른지 확인합니다. 대상의 열 이름을 바꿀 수도 있습니다.  
  
15. **확인**을 클릭합니다.  
  
## <a name="next-steps"></a>다음 단계  
 [5 단계: 4 단원 자습서 패키지 테스트](../integration-services/lesson-4-5-testing-the-lesson-4-tutorial-package.md)  
  
  
