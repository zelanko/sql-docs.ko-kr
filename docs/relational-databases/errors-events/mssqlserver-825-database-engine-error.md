---
title: "MSSQLSERVER_825 | Microsoft 문서"
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 825 (Database Engine error)
ms.assetid: f69f8214-5af1-4769-878b-117ad6eaff52
caps.latest.revision: "16"
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.openlocfilehash: eca90fd222c819fe9b57d26a24d86e85e4806ae5
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="mssqlserver825"></a>MSSQLSERVER_825
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|825|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|B_RETRYWORKED|  
|메시지 텍스트|오류로 인해 읽기 시도를 %d번 실패한 후 오프셋 %#016I64x에서 파일 '%ls'의 읽기 작업이 성공했습니다: %ls. SQL Server 오류 로그 및 시스템 이벤트 로그의 추가 메시지에서 더 자세한 정보를 얻을 수 있습니다. 이 오류 조건은 데이터베이스 무결성을 침해할 수 있으므로 수정되어야 합니다. 전체 데이터베이스 일관성 확인(DBCC CHECKDB)을 완료하십시오. 이 오류는 여러 요인으로 인해 발생할 수 있습니다. 자세한 내용은 SQL Server 온라인 설명서를 참조하십시오.|  
  
## <a name="explanation"></a>설명  
이 메시지는 읽기 작업이 적어도 한 번 이상 다시 실행되어야 했음을 나타내며 디스크 하드웨어에 중요한 문제가 있음을 나타냅니다. 현재 이 메시지는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 문제를 나타내고 있지 않지만 문제가 해결되지 않을 경우 데이터 손실 또는 데이터베이스 손상을 일으킬 수 있습니다. 시스템 이벤트 로그에 문제의 진단에 도움이 되는 관련 이벤트가 포함되어 있을 수 있습니다. I/O 오류에 대한 자세한 내용은 [Microsoft SQL Server I/O Basics, Chapter 2](http://go.microsoft.com/fwlink/?LinkId=69370)(Microsoft SQL Server I/O 기본 사항, 2장)를 참조하세요.  
  
## <a name="user-action"></a>사용자 동작  
다음은 기본 문제를 확인하고 해결하는 데 도움이 되는 동작입니다.  
  
-   이 메시지의 오류 로그 및 변수 텍스트를 검토하여 문제를 파악합니다.  
  
-   디스크 시스템을 확인합니다. 디스크, 디스크 컨트롤러, 배열 카드 또는 디스크 드라이버에 관련된 문제일 수 있습니다.  
  
-   최신 유틸리티의 디스크 제조업체에 문의하여 사용자의 디스크 시스템 상태를 확인합니다.  
  
-   최신 드라이버 업데이트에 대해 디스크 제조업체에 문의합니다.  
  
