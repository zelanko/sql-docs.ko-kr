---
title: '작업 15: SSIS 프로젝트 빌드 및 실행 | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 13adf4e0-216a-4992-b13d-b7b1e1629e77
ms.author: lle
author: lrtoyou1223
ms.openlocfilehash: 50b313f63ae434a96d6c0e38f3c8b600914c806d
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66822996"
---
# <a name="task-15-building-and-running-the-ssis-project"></a>태스크 15: SSIS 프로젝트 빌드 및 실행

  이 작업에서는 SSIS 프로젝트를 빌드하고 실행합니다. 64 비트 버전의 Excel 2010이 컴퓨터에 설치 되어 있는 경우 Excel 원본이 작동 하려면 **Run64BitRuntime** 값을 **False** 로 설정 해야 합니다.  
  
1.  **솔루션 탐색기** 창의 메뉴에서 **프로젝트** 를 클릭 하 고 **CleanseAndCurateSuppliers 속성**을 클릭 합니다.  
  
2.  **속성** 대화 상자에서 왼쪽의 **구성 속성** 을 확장 하 고 **디버깅**을 클릭 합니다.  
  
3.  **Run64BitRuntime** 을 **False**로 설정 합니다.  
  
     ![CleanseAndCurateSuppliers 프로젝트 속성](../../2014/tutorials/media/et-buildingandrunningthessisproject-01.jpg "CleanseAndCurateSuppliers 프로젝트 속성")  
  
4.  **확인**을 클릭하여 **속성** 대화 상자를 닫습니다.  
  
5.  메뉴 모음에서 **빌드** 를 클릭 하 고 **CleanseAndCurateSuppliers 빌드**를 클릭 합니다. 빌드 오류가 없는지 확인합니다.  
  
6.  메뉴 모음에서 **디버그** 를 클릭 하 고 **디버깅 시작**을 클릭 합니다.  
  
7.  **진행률** 창에서 메시지를 검토 하 고 패키지를 실행 하 고 성공적으로 종료 했는지 확인 합니다.  
  
     ![진행률 창의 결과](../../2014/tutorials/media/et-buildingandrunningthessisproject-02.jpg "진행률 창의 결과")  
  
     ![진행률 창의 마지막 상태](../../2014/tutorials/media/et-buildingandrunningthessisproject-03.jpg "진행률 창의 마지막 상태")  
  
8.  메뉴 모음에서 **디버그** 를 클릭 하 고 디버깅 **중지** 를 클릭 하 여 디버깅 세션을 중지 합니다. 패키지가 실패하면 데이터 뷰어를 사용하도록 설정하고 구성 요소 간 데이터 흐름 방식을 확인해야 합니다.  
  
## <a name="next-step"></a>다음 단계  
 [태스크 16: 마스터 데이터 관리자에서 확인](../../2014/tutorials/task-16-verifying-with-master-data-manager.md)  
  
  
