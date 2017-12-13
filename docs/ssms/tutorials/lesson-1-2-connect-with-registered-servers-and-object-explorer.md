---
title: "등록된 서버 및 개체 탐색기와 연결 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssms-tutorial
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
ms.assetid: d6b3911f-68b4-4483-831b-df89d6400add
caps.latest.revision: "50"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: f280ca05701c1497843a1dd8caf78e166a1b98f5
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/05/2017
---
# <a name="lesson-1-2---connect-with-registered-servers-and-object-explorer"></a>1-2단원 - 등록된 서버 및 개체 탐색기와 연결
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] 이 자습서에서는 등록된 서버와 개체 탐색기를 사용하는 방법을 보여 줍니다.  
  
이 자습서에서는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스를 사용합니다. 보안을 위해 예제 데이터베이스는 기본적으로 설치되지 않습니다. 자세한 정보는 [SQL Server 예제 및 예제 데이터베이스 설치](http://sqlserversamples.codeplex.com)를 참조하십시오.  
  
## <a name="connecting-to-servers"></a>서버에 연결  
등록된 서버 구성 요소의 도구 모음에는 [!INCLUDE[ssDE](../../includes/ssde-md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]및 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]에 대한 단추가 있습니다. 이들 중 하나 이상의 서버 유형을 등록하여 쉽게 관리할 수 있습니다. 이 연습에서는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스를 등록합니다.  
  
#### <a name="to-register-the-database"></a>데이터베이스를 등록하려면  
  
1.  필요한 경우 등록된 서버 도구 모음에서 **데이터베이스 엔진** 을 클릭합니다. 이미 선택되어 있을 수도 있습니다.  
  
2.  **데이터베이스 엔진**을 확장합니다.  
  
3.  **로컬 서버 그룹**을 마우스 오른쪽 단추로 클릭한 다음 **새 서버 등록**을 클릭합니다.  
  
4.  **새 서버 등록** 대화 상자의 **서버 이름** 입력란에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스 이름을 입력합니다.  
  
5.  **등록된 서버 이름** 입력란에 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]를 입력합니다.  
  
6.  **연결 속성** 탭의 **연결할 데이터베이스** 목록에서 **\<서버 찾아보기…>**를 클릭합니다.  
  
7.  **데이터베이스 찾아보기** 대화 상자에서 **예**를 클릭합니다.  
  
8.  **서버에서 데이터베이스 찾아보기** 대화 상자에서 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]를 선택한 다음 **확인**을 클릭합니다.  
  
9. 서버가 제대로 등록되었는지 확인하려면 **테스트**를 클릭합니다.  
  
10. **새 서버 등록** 대화 상자에서 **저장**을 클릭합니다.  
  
## <a name="connecting-with-object-explorer"></a>개체 탐색기와 연결  
등록된 서버와 마찬가지로 개체 탐색기에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]및 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에 연결할 수 있습니다.  
  
#### <a name="to-connect-with-object-explorer"></a>개체 탐색기와 연결하려면  
  
1.  개체 탐색기의 도구 모음에서 **연결** 을 클릭하여 가능한 연결 유형 목록을 표시한 다음 **데이터베이스 엔진**을 선택합니다.  
  
2.  **서버에 연결** 대화 상자의 **서버 이름** 입력란에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스 이름을 입력합니다.  
  
3.  **옵션** 을 클릭하고 원하는 옵션을 탐색합니다.  
  
4.  서버에 연결하려면 **연결**을 클릭합니다. 이미 연결된 경우 개체 탐색기로 돌아가고 해당 서버에 포커스가 설정됩니다.  
  
    개체 탐색기를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 보안, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트, 복제 및 데이터베이스 메일을 관리할 수 있습니다. 개체 탐색기에서는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]및 [!INCLUDE[ssIS](../../includes/ssis-md.md)]의 일부 기능만 관리할 수 있습니다. 이러한 각 구성 요소에는 특별한 도구가 포함되어 있습니다.  
  
5.  개체 탐색기에서 **데이터베이스** 폴더를 확장하고 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]를 선택합니다.  
  
    [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 에서는 시스템 데이터베이스를 별개의 폴더에 표시합니다.  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
[환경 레이아웃 변경](../../tools/sql-server-management-studio/lesson-1-3-change-the-environment-layout.md)  
  
  
  
