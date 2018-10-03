---
title: 교착 상태 파일 열기, 보기 및 인쇄(SQL Server Management Studio) | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- deadlocks [SQL Server], printing files
- deadlocks [SQL Server], opening files
- opening deadlock files
- printing deadlock files
ms.assetid: 5061b13f-2cb7-457a-b8d0-fbd437b510ab
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 4a45daf3d20da1b431ce31ef5d6756ee17ce264f
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48155493"
---
# <a name="open-view-and-print-a-deadlock-file-sql-server-management-studio"></a>교착 상태 파일 열기, 보기 및 인쇄(SQL Server Management Studio)
  [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 에서 교착 상태가 생성되면 교착 상태 정보를 캡처하여 파일에 저장할 수 있습니다. 교착 상태 파일을 저장한 다음 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 에서 해당 파일을 열어서 보거나 인쇄할 수 있습니다.  
  
### <a name="to-open-and-view-a-deadlock-file"></a>교착 상태 파일을 열고 보려면  
  
1.  **의** 파일 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]메뉴에서 **열기**를 가리킨 다음 **파일**을 클릭합니다.  
  
2.  **파일 열기** 대화 상자의 **파일 유형** 확인란에서 .xdl 파일 유형을 선택합니다. 교착 상태 파일만 필터링한 목록이 남아 있을 것입니다.  
  
### <a name="to-print-a-deadlock-file"></a>교착 상태 파일을 인쇄하려면  
  
1.  **의** 파일 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]메뉴에서 **열기** 를 가리킨 다음 **파일**을 클릭합니다.  
  
2.  **파일 열기** 대화 상자의 **파일 유형** 확인란에서 .xdl 파일 유형을 선택합니다. 교착 상태 파일만 필터링한 목록이 남아 있을 것입니다.  
  
3.  인쇄할 교착 상태 파일을 선택하고 **열기**를 클릭합니다.  
  
4.  **파일** 메뉴에서 **인쇄**를 클릭합니다.  
  
## <a name="see-also"></a>관련 항목  
 [교착 상태 그래프 저장&#40;SQL Server Profiler&#41;](save-deadlock-graphs-sql-server-profiler.md)  
  
  
