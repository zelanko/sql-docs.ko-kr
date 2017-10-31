---
title: "MSSQLSERVER_10001 | Microsoft 문서"
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 10001 (Database Engine error)
ms.assetid: f8fd2d8d-a4af-4b6a-ba51-9123b7e4c9bf
caps.latest.revision: 16
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 6db18eb8805eef626a72332bf6190c39fda97981
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver10001"></a>MSSQLSERVER_10001
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|10001|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|HR_E_UNEXPECTED|  
|메시지 텍스트|공급자에서 예기치 않은 치명적인 오류가 보고되었습니다.|  
  
## <a name="explanation"></a>설명  
OLE DB 공급자를 호출하는 동안 분산 쿼리 처리에서 일반 오류가 발생했습니다.  
  
## <a name="user-action"></a>사용자 동작  
[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]를 사용하여 OLE DB 추적 이벤트를 수집하고 이 데이터를 OLE DB 공급자에 대한 제품 지원에 제공합니다.  
  
## <a name="see-also"></a>참고 항목  
[SQL Server Profiler 템플릿 및 권한](~/tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md)  
[SQL Server Native Client&#40;OLE DB&#41;](~/relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)  
  

