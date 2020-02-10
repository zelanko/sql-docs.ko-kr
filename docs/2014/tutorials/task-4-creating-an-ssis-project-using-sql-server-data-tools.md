---
title: '작업 4: SQL Server Data Tools을 사용 하 여 SSIS 프로젝트 만들기 | Microsoft Docs'
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 8603ea91-2ec4-40b6-8070-4f824332f5d3
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 8fb38cb068aca480756db7d962540137c8d4bfac
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "65489200"
---
# <a name="task-4-creating-an-ssis-project-using-sql-server-data-tools"></a>작업 4: SQL Server Data Tools를 사용하여 SSIS 프로젝트 만들기
  이 작업에서는 공급자 데이터 정리 및 일치를 자동화하기 위해 **SQL Server Data Tools** 를 사용해서 SSIS 프로젝트를 만듭니다.  
  
1.  
  **SQL Server Data Tools**를 실행합니다. 시작을 클릭하고, **모든 프로그램**을 가리킨 후 **Microsoft SQL Server 2012**를 확장하고 **SQL Server Data Tools**를 클릭합니다.  
  
2.  
  **파일** 메뉴에서 **새로 만들기**를 가리키고 **프로젝트**를 클릭합니다.  
  
3.  
  **설치된 템플릿** 창에서 **비즈니스 인텔리전스** 를 확장하고 **Integration Services**를 선택합니다.  
  
     ![Visual Studio - 새 프로젝트 대화 상자](../../2014/tutorials/media/et-creatinganssisprojectusingsqlsdt-01.jpg "Visual Studio - 새 프로젝트 대화 상자")  
  
4.  
  **프로젝트 형식 목록** 에서 **Integration Services 프로젝트**를 선택합니다.  
  
5.  
  **이름** 에 **CleanseAndCurateSuppliers** 를 입력하고 **확인**을 클릭합니다.  
  
6.  
  **솔루션 탐색기** 창에서 **Package.dtsx** 를 마우스 오른쪽 단추로 클릭하고 **이름 바꾸기**를 선택합니다. **솔루션 탐색기** 창이 표시 되지 않으면 메뉴 모음에서 **보기** 를 클릭 하 고 **솔루션 탐색기**을 클릭 합니다.  
  
     ![Package.dtsx - 이름 바꾸기 메뉴](../../2014/tutorials/media/et-creatinganssisprojectusingsqlsdt-02.jpg "Package.dtsx - 이름 바꾸기 메뉴")  
  
7.  
  **CleanseAndCurate.dtsx** 를 입력하고 **Enter**키를 누릅니다. 
  **확장명** 이 **.dtsx**인지 확인합니다.  
  
## <a name="next-step"></a>다음 단계  
 [태스크 5: 데이터 흐름 태스크 추가](task-5-adding-data-flow-task.md)  
  
  
