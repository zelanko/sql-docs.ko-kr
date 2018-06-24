---
title: 활성 작업 대화 상자 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.ssis.ssms.isoperations.executions.f1
- sql12.ssis.ssms.isoperations.general.f1
ms.assetid: 5bb0fcd6-0ce9-488a-85b8-25dddaa03cda
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: adf25cd2194e1a02877c38a15d81d8697427ad76
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36080465"
---
# <a name="active-operations-dialog-box"></a>활성 작업 대화 상자
  **활성 작업** 대화 상자를 사용하여 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 서버에서 현재 실행 중인 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 작업(예: 배포, 유효성 검사 및 패키지 실행)의 상태를 볼 수 있습니다. 이 데이터는 SSISDB 카탈로그에 저장됩니다.  
  
 관련된 [!INCLUDE[tsql](../includes/tsql-md.md)] 뷰에 대한 자세한 내용은 [catalog.operations&#40;SSISDB 데이터베이스&#41;](/sql/integration-services/system-views/catalog-operations-ssisdb-database), [catalog.validations&#40;SSISDB 데이터베이스&#41;](/sql/integration-services/system-views/catalog-validations-ssisdb-database) 및 [catalog.executions&#40;SSISDB 데이터베이스&#41;](/sql/integration-services/system-views/catalog-executions-ssisdb-database)를 참조하세요.  
  
 **수행 작업**  
  
1.  [활성 작업 대화 상자 열기](#open_dialog)  
  
2.  [옵션 구성](#options)  
  
##  <a name="open_dialog"></a> 활성 작업 대화 상자 열기  
  
1.  열기 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]합니다.  
  
2.  Microsoft SQL Server 데이터베이스 엔진 연결  
  
3.  개체 탐색기에서 **Integration Services** 노드를 확장하고 **SSISDB**를 마우스 오른쪽 단추로 클릭한 다음 **활성 작업**을 클릭합니다.  
  
##  <a name="options"></a> 옵션 구성  
  
### <a name="options"></a>변수  
 **형식**  
 작업 유형을 지정합니다. 다음에 대 한 가능한 값은는 **형식** TRANSACT-SQL의 operations_type 열에 해당 값과 필드 `catalog.operations` 보기.  
  
|||  
|-|-|  
|Integration Services 초기화|1|  
|작업 정리(SQL 에이전트 작업)|2|  
|프로젝트 버전 정리(SQL 에이전트 작업)|3|  
|프로젝트 배포|101|  
|프로젝트 복원|106|  
|패키지 실행 생성 및 시작|200|  
|작업 중지(유효성 검사 또는 실행 중지)|202|  
|프로젝트 유효성 검사|300|  
|패키지 유효성 검사|301|  
|카탈로그 구성|1000|  
  
 **중지**  
 현재 실행 중인 작업을 중지하려면 클릭합니다.  
  
  
