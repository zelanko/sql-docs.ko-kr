---
title: SQL Server Profiler-원본 테이블-데이터베이스 엔진 튜닝 관리자-작업 테이블 선택 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- sql12.pro.replay.tools.sourcetable.f1
helpviewer_keywords:
- Select Workload Table dialog box
- Source Table dialog box
ms.assetid: 51185be7-7092-480a-a52c-cf7786c4a0a0
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 973680d07c3bd6a304e63f4b3fde0e228f0f7bff
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66088877"
---
# <a name="sql-server-profiler---source-table-database-engine-tuning-advisor---select-workload-table"></a>SQL Server Profiler - Source Table-Database Engine Tuning Advisor - Select Workload Table
  Microsoft [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] 및 [!INCLUDE[ssDE](../includes/ssde-md.md)] 튜닝 관리자는 이 대화 상자를 사용하여 테이블을 선택합니다.  
  
 [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)]에서 추적 테이블의 원본 테이블을 지정하려면 **원본 테이블** 대화 상자를 사용합니다. 추적 테이블은 추적 내용이 로드되는 테이블이고 이 테이블의 내용은 추적 재생을 위해 검토되거나 사용됩니다.  
  
 [!INCLUDE[ssDE](../includes/ssde-md.md)] 튜닝 관리자에서는 **작업 테이블 선택** 대화 상자를 사용하여 튜닝 작업으로 사용할 [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] 추적 정보가 포함된 데이터베이스 테이블을 선택하거나 튜닝 분석 시작 전에 테이블 내용을 미리 볼 수 있습니다.  
  
## <a name="options"></a>옵션  
 **SQL Server**  
 현재 연결된 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스를 지정합니다. 이 필드는 자동으로 채워지며 업데이트할 수 없습니다.  
  
 **Database**  
 추적 테이블이 있는 데이터베이스를 지정합니다.  
  
 **소유자**  
 Specifies the owner of the trace table. 이 필드에는 **dbo**가 자동으로 채워집니다.  
  
 **테이블**  
 추적을 읽어오는 추적 테이블의 이름을 지정합니다.  
  
## <a name="see-also"></a>참고 항목  
 [추적 결과를 테이블 &#40;SQL Server Profiler에 저장&#41;](../tools/sql-server-profiler/save-trace-results-to-a-table-sql-server-profiler.md)   
 [SQL Server Profiler 템플릿 및 권한](../tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md)   
 [Database Engine Tuning Advisor](../relational-databases/performance/database-engine-tuning-advisor.md)  
  
  
