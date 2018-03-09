---
title: "MSSQLSERVER_17204 | Microsoft 문서"
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 17204 (Database Engine error)
ms.assetid: 40db66f9-dd5e-478c-891e-a06d363a2552
caps.latest.revision: "14"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: befada4a3c2b5ea56fbe8c6ec6b14f6d5a558886
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver17204"></a>MSSQLSERVER_17204
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|17204|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|DBLKIO_DEVOPENFAILED|  
|메시지 텍스트|%ls: 파일 번호 %d에 대한 파일 %ls을(를) 열 수 없습니다.  OS 오류: '%ls'.|  
  
## <a name="explanation"></a>설명  
SQL Server에서 특정 오류로 인해 지정한 파일을 열 수 없습니다.  
  
## <a name="user-action"></a>사용자 동작  
운영 체제 문제를 진단하고 해결한 다음 작업을 다시 합니다.  
  
