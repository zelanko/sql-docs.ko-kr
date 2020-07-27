---
title: 교착 상태 파일 열기, 보기, 인쇄(SSMS)
description: SQL Server Profiler가 생성하는 교착 상태 정보를 캡처하여 SQL Server Management Studio에서 보는 방법을 알아봅니다.
ms.custom: seo-dt-2019
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- deadlocks [SQL Server], printing files
- deadlocks [SQL Server], opening files
- opening deadlock files
- printing deadlock files
ms.assetid: 5061b13f-2cb7-457a-b8d0-fbd437b510ab
author: julieMSFT
ms.author: jrasnick
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 3c55ad170e9d6a9fe58865ab28ac75f018b6905b
ms.sourcegitcommit: 9470c4d1fc8d2d9d08525c4f811282999d765e6e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/17/2020
ms.locfileid: "86458477"
---
# <a name="open-view-and-print-a-deadlock-file-in-sql-server-management-studio-ssms"></a>SSMS(SQL Server Management Studio)에서 교착 상태 파일 열기, 보기 및 인쇄

[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 에서 교착 상태가 생성되면 교착 상태 정보를 캡처하여 파일에 저장할 수 있습니다. 교착 상태 파일을 저장한 다음 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 해당 파일을 열어서 보거나 인쇄할 수 있습니다.  
  
## <a name="open-and-view-a-deadlock-file"></a>교착 상태 파일 열기 및 보기  
  
1. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]의 **파일** 메뉴에서 **열기**를 가리킨 다음 **파일**을 선택합니다.  
  
2. **파일 열기** 대화 상자의 **파일 유형** 확인란에서 .xdl 파일 유형을 선택합니다. 교착 상태 파일만 필터링한 목록이 남아 있을 것입니다.  
  
## <a name="print-a-deadlock-file"></a>교착 상태 파일 인쇄  
  
1. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]의 **파일** 메뉴에서 **열기**를 가리킨 다음 **파일**을 선택합니다.  
  
2. **파일 열기** 대화 상자의 **파일 유형** 확인란에서 .xdl 파일 유형을 선택합니다. 교착 상태 파일만 필터링한 목록이 남아 있을 것입니다.  
  
3. 인쇄할 교착 상태 파일을 선택하고 **열기**를 선택합니다.  
  
4. **파일** 메뉴에서 **인쇄**를 선택합니다.  
  
## <a name="see-also"></a>참고 항목  
 [교착 상태 그래프 저장&#40;SQL Server Profiler&#41;](../../relational-databases/performance/save-deadlock-graphs-sql-server-profiler.md)  
  
  
