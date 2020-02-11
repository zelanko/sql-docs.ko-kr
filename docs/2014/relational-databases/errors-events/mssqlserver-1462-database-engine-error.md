---
title: MSSQLSERVER_1462 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 1462 (Database Engine error)
ms.assetid: 680e9c1c-a9d6-4765-b601-956d0a83324c
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 1a9740287c211ac6fec7414ef05dd422a28a926b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62869918"
---
# <a name="mssqlserver_1462"></a>MSSQLSERVER_1462
    
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|1462|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|DBM_DISABLED_DUE_TO_FAILED_REDO|  
|메시지 텍스트|실패한 다시 실행 작업으로 인해 데이터베이스 미러링이 비활성화되었습니다. 재개할 수 없습니다.|  
  
## <a name="explanation"></a>설명  
 데이터베이스 미러링이 미러의 로그 레코드를 다시 실행하지 못했습니다.  
  
### <a name="possible-causes"></a>가능한 원인  
 주 데이터베이스에서는 파일 추가 작업을 완료했지만 파일 이름 또는 디렉터리 구조가 주 서버 및 미러 서버와 다르기 때문에 미러 데이터베이스에서는 파일 추가 작업에 실패했을 수 있습니다.  
  
## <a name="user-action"></a>사용자 동작  
 이 오류의 원인에 대한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 로그를 확인합니다. 원인을 해결하고 데이터베이스의 미러링을 재개합니다.  
  
## <a name="see-also"></a>참고 항목  
 [데이터베이스 미러링 구성 문제 해결&#40;SQL Server&#41;](../../database-engine/database-mirroring/troubleshoot-database-mirroring-configuration-sql-server.md)  
  
  
