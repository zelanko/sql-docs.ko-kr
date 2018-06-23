---
title: '태스크 15: 빌드 및 SSIS 프로젝트를 실행 합니다. | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 13adf4e0-216a-4992-b13d-b7b1e1629e77
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 9a63fcf03591626d5b4c1351d5ce868ef7a9fb65
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36090979"
---
# <a name="task-15-building-and-running-the-ssis-project"></a>태스크 15: SSIS 프로젝트 작성 및 실행
  이 작업에서는 SSIS 프로젝트를 빌드하고 실행합니다. 값을 설정 해야 64 비트 버전의 Excel 2010이 컴퓨터에 설치 되어 있는 경우 **Run64BitRuntime** 를 **False** Excel 원본이 작동 하려면에 대 한 합니다.  
  
1.  에 **솔루션 탐색기** 창 클릭 **프로젝트** 메뉴에서을 클릭 하 여 **CleanseAndCurateSuppliers 속성**합니다.  
  
2.  에 **속성** 대화 상자에서 **구성 속성** 를 클릭 한 왼쪽 **디버깅**합니다.  
  
3.  설정 **Run64BitRuntime** 를 **False**합니다.  
  
     ![CleanseAndCurateSuppliers 프로젝트 속성](../../2014/tutorials/media/et-buildingandrunningthessisproject-01.jpg "CleanseAndCurateSuppliers 프로젝트 속성")  
  
4.  클릭 **확인** 를 닫으려면는 **속성** 대화 상자.  
  
5.  클릭 **빌드** 클릭 메뉴 모음에서 **CleanseAndCurateSuppliers 빌드**합니다. 빌드 오류가 없는지 확인합니다.  
  
6.  클릭 **디버그** 클릭 메뉴 모음에서 **디버깅 시작**합니다.  
  
7.  메시지를 검토는 **진행률** 창 고 해당 패키지 실행 및 종료를 성공적으로 확인 합니다.  
  
     ![진행률 창의 결과](../../2014/tutorials/media/et-buildingandrunningthessisproject-02.jpg "진행률 창의 결과")  
  
     ![진행률 창의 마지막 상태](../../2014/tutorials/media/et-buildingandrunningthessisproject-03.jpg "진행률 창의 마지막 상태")  
  
8.  클릭 **디버그** 클릭 메뉴 모음에서 **디버깅 중지** 디버깅 세션을 중지 합니다. 패키지가 실패하면 데이터 뷰어를 사용하도록 설정하고 구성 요소 간 데이터 흐름 방식을 확인해야 합니다.  
  
## <a name="next-step"></a>다음 단계  
 [태스크 16: 마스터 데이터 관리자에서 확인](../../2014/tutorials/task-16-verifying-with-master-data-manager.md)  
  
  