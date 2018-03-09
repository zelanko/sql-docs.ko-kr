---
title: "MSSQLSERVER_905 | Microsoft 문서"
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 905 (Database Engine error)
ms.assetid: c828bb2e-e554-4f81-b76c-2b3740d2b944
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 648f373a5e1054ae72a462914072391f5560dce0
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver905"></a>MSSQLSERVER_905
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|905|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|DBSTARTUP_EE_PARTITIONING|  
|메시지 텍스트|파티션 함수 '%.\*ls'이(가) 포함되어 있기 때문에 이 SQL Server Edition에서는 데이터베이스 '%.*ls'을(를) 시작할 수 없습니다. SQL Server Enterprise Edition에서만 분할을 지원합니다.|  
  
## <a name="explanation"></a>설명  
데이터베이스에는 하나 이상의 분할된 테이블 또는 인덱스가 포함되어 있습니다. 이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Edition에서는 분할을 사용할 수 없습니다. 따라서 데이터베이스를 올바로 시작할 수 없습니다. 분할된 테이블 및 인덱스는 일부 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전에서만 사용할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]버전에서 지원되는 기능 목록은 [SQL Server 2016 버전에서 지원하는 기능](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)을 참조하세요.  
  
## <a name="user-action"></a>사용자 동작  
sp_detach_db 저장 프로시저를 사용하여 데이터베이스를 분리합니다. 필요한 경우 파일을 이동한 다음 CREATE DATABASE와 함께 FOR ATTACH 또는 FOR ATTACH_REBUILD_LOG 옵션을 사용하여 지원되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전의 인스턴스에 데이터베이스를 연결합니다. 모든 테이블에서 분할을 사용할 수 없게 설정하고 파티션 함수를 제거합니다. 데이터베이스를 다시 분리한 다음 현재 서버에 다시 연결합니다.  
  
