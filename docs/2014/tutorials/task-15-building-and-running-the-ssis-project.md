---
title: '태스크 15: SSIS 프로젝트 작성 및 실행 | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 13adf4e0-216a-4992-b13d-b7b1e1629e77
ms.openlocfilehash: 1dc31f9b3df500e862236d4125fb1de99bc93eda
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56022811"
---
# <a name="task-15-building-and-running-the-ssis-project"></a>태스크 15: SSIS 프로젝트 작성 및 실행
  이 작업에서는 SSIS 프로젝트를 빌드하고 실행합니다. 64 비트 버전의 컴퓨터에 설치 하는 Excel 2010을 사용 하는 경우의 값을 설정 해야 **Run64BitRuntime** 하 **False** Excel 원본이 작동 하려면에 대 한 합니다.  
  
1.  에 **솔루션 탐색기** 창에서 클릭 **프로젝트** 메뉴를 클릭 **CleanseAndCurateSuppliers 속성**합니다.  
  
2.  에 **속성** 대화 상자에서 **구성 속성** 왼쪽에 클릭 **디버깅**합니다.  
  
3.  설정할 **Run64BitRuntime** 하 **False**합니다.  
  
     ![CleanseAndCurateSuppliers 프로젝트 속성](../../2014/tutorials/media/et-buildingandrunningthessisproject-01.jpg "CleanseAndCurateSuppliers 프로젝트 속성")  
  
4.  클릭 **확인** 닫으려면 합니다 **속성** 대화 상자.  
  
5.  클릭 **빌드합니다** 하 고 메뉴 모음에서 **CleanseAndCurateSuppliers 빌드**합니다. 빌드 오류가 없는지 확인합니다.  
  
6.  클릭 **디버깅할** 메뉴 모음에서 클릭 **디버깅 시작**합니다.  
  
7.  메시지를 검토 합니다 **진행률** 창 및 해당 패키지를 실행 하 고 성공적으로 종료를 확인 합니다.  
  
     ![진행률 창의 결과](../../2014/tutorials/media/et-buildingandrunningthessisproject-02.jpg "진행률 창의 결과")  
  
     ![진행률 창의 마지막 상태](../../2014/tutorials/media/et-buildingandrunningthessisproject-03.jpg "진행률 창의 마지막 상태")  
  
8.  클릭 **디버그** 하 고 메뉴 모음에서 **디버깅 중지** 디버깅 세션을 중지 합니다. 패키지가 실패하면 데이터 뷰어를 사용하도록 설정하고 구성 요소 간 데이터 흐름 방식을 확인해야 합니다.  
  
## <a name="next-step"></a>다음 단계  
 [태스크 16: 마스터 데이터 관리자에서 확인](../../2014/tutorials/task-16-verifying-with-master-data-manager.md)  
  
  
