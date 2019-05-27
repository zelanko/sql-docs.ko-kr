---
title: 작업 튜닝 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- workloads [SQL Server], tuning
ms.assetid: 6229bf3f-1182-4bc6-8451-cedc37f4b62e
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3dd87c1e2bd08ce5bb1d05e9d51d92e3f62bcc7a
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66110193"
---
# <a name="tuning-a-workload"></a>작업 튜닝
  데이터베이스 엔진 튜닝 관리자를 사용하여 튜닝하려고 선택한 데이터베이스와 테이블의 쿼리 성능에 가장 적합한 물리적 데이터베이스 디자인을 찾을 수 있습니다.  
  
 이 태스크에서는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 예제 데이터베이스를 사용합니다. 보안을 위해 예제 데이터베이스는 기본적으로 설치되지 않습니다. 예제 데이터베이스를 설치하려면 [SQL Server 예제 및 예제 데이터베이스](http://sqlserversamples.codeplex.com)를 참조하세요.  
  
### <a name="tune-a-workload-transact-sql-script-file"></a>작업 Transact-SQL 스크립트 파일 튜닝  
  
1.  "1. SELECT를 사용하여 행 및 열 검색"([SELECT 예제&#40;Transact-SQL&#41;](/sql/t-sql/queries/select-examples-transact-sql))에서 샘플 SELECT 문을 복사하여 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]의 쿼리 편집기에 붙여넣습니다. 쉽게 찾을 수 있는 디렉터리에 **MyScript.sql**이라는 이름으로 파일을 저장합니다.  
  
2.  데이터베이스 엔진 튜닝 관리자를 시작합니다. [데이터베이스 엔진 튜닝 관리자 시작](../../relational-databases/performance/database-engine-tuning-advisor.md)을 참조하세요.  
  
3.  데이터베이스 엔진 튜닝 관리자 GUI의 오른쪽 창에 있는 **세션 이름** 에 **MySession**을 입력합니다.  
  
4.  **작업** 에 대해 **파일**을 선택하고 **작업 파일을 찾습니다.** 단추를 클릭하여 1단계에서 저장한 **MyScript.sql** 파일을 찾습니다.  
  
5.  [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 작업 분석용 데이터베이스 **목록에서** 를 선택하고, [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 튜닝할 데이터베이스 및 테이블 선택 **표에서** 를 선택하고, **튜닝 로그 저장** 을 선택된 상태로 둡니다. **작업 분석용 데이터베이스** 는 작업 튜닝 시 데이터베이스 엔진 튜닝 관리자가 연결하는 첫 번째 데이터베이스를 지정합니다. 튜닝이 시작된 후 데이터베이스 엔진 튜닝 관리자는 작업에 포함된 `USE DATABASE` 문으로 지정한 데이터베이스에 연결합니다.  
  
6.  **튜닝 옵션** 탭을 클릭합니다. 이 연습에서는 튜닝 옵션을 전혀 설정하지 않지만 잠시 기본 튜닝 옵션을 검토합니다. 이 탭 페이지에 대한 도움말을 보려면 F1 키를 누릅니다. 추가 튜닝 옵션을 보려면 **고급 옵션** 을 클릭합니다. **고급 튜닝 옵션** 대화 상자에서 표시된 튜닝 옵션에 대한 정보를 보려면 **도움말** 을 클릭합니다. 기본 옵션을 선택한 상태에서 **고급 튜닝 옵션** 대화 상자를 닫으려면 **취소** 를 클릭합니다.  
  
7.  도구 모음에서 **분석 시작** 단추를 클릭합니다. 데이터베이스 엔진 튜닝 관리자에서 작업을 분석하는 동안 **진행률** 탭에서 상태를 모니터링할 수 있습니다. 튜닝이 완료되면 **권장 구성** 탭이 표시됩니다.  
  
     튜닝 중지 날짜 및 시간에 대해 오류가 발생하면 주 **튜닝 옵션** 탭에서 **중지 시간** 을 확인합니다. **중지 시간** 날짜 및 시간이 현재 날짜 및 시간 이후인지 확인한 다음 필요한 경우 변경합니다.  
  
8.  분석을 완료한 후 [!INCLUDE[tsql](../../includes/tsql-md.md)] 동작 **메뉴에서** 권장 구성 저장 **을 클릭하여** 스크립트로 권장 구성을 저장합니다. **다른 이름으로 저장** 대화 상자에서 권장 구성 스크립트를 저장할 디렉터리로 이동하고 파일 이름 **MyRecommendations**를 입력합니다.  
  
## <a name="summary"></a>요약  
 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스에서 단순 SELECT 문 작업 튜닝을 완료했습니다. 데이터베이스 엔진 튜닝 관리자에서는 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 추적 파일과 테이블을 튜닝 작업으로 사용할 수도 있습니다. 다음 태스크에서는 연습 튜닝의 결과로 받은 튜닝 권장 구성을 확인하고 해석하는 방법을 보여 줍니다.  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
 [튜닝 권장 구성 보기](lesson-1-2-viewing-tuning-recommendations.md)  
  
  
