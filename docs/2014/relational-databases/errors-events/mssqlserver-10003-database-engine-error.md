---
title: MSSQLSERVER_10003 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 10003 (Database Engine error)
ms.assetid: 9e2cb199-f077-4d88-8117-1b7550afc696
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 2253fc0db73583d3e8f5e5fb97767557ec47d49e
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84969898"
---
# <a name="mssqlserver_10003"></a>MSSQLSERVER_10003
    
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|10003|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|HR_E_OUTOFMEMORY|  
|메시지 텍스트|공급자의 메모리가 부족합니다.|  
  
## <a name="explanation"></a>설명  
 부족한 시스템 메모리 때문에 OLE DB 공급자의 메모리가 부족합니다.  
  
## <a name="user-action"></a>사용자 동작  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스를 다시 시작합니다. 그래도 도움이 되지 않으면 컴퓨터를 다시 시작합니다. 문제가 지속되면 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]를 사용하여 OLE DB 추적 이벤트를 수집하고 이 데이터를 OLE DB 공급자에 대한 제품 지원에 제공합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server Profiler 템플릿 및 권한](../../tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md)   
 [SQL Server Native Client&#40;OLE DB&#41;](../native-client/ole-db/sql-server-native-client-ole-db.md)  
  
  
