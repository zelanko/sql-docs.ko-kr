---
title: MSSQLSERVER_905 | Microsoft 문서
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 905 (Database Engine error)
ms.assetid: c828bb2e-e554-4f81-b76c-2b3740d2b944
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d9b80e93f3df2cdc5623e6f2b31a94d50cd524d7
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48051263"
---
# <a name="mssqlserver905"></a>MSSQLSERVER_905
    
## <a name="details"></a>설명  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|905|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|DBSTARTUP_EE_PARTITIONING|  
|메시지 텍스트|파티션 함수 '%.\*ls'이(가) 포함되어 있기 때문에 이 SQL Server Edition에서는 데이터베이스 '%.*ls'을(를) 시작할 수 없습니다. SQL Server Enterprise Edition에서만 분할을 지원합니다.|  
  
## <a name="explanation"></a>설명  
 데이터베이스에는 하나 이상의 분할된 테이블 또는 인덱스가 포함되어 있습니다. 이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Edition에서는 분할을 사용할 수 없습니다. 따라서 데이터베이스를 올바로 시작할 수 없습니다. 분할된 테이블 및 인덱스는 일부 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전에서만 사용할 수 있습니다. 버전에서 지원 되는 기능 목록은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 참조 하세요 [SQL Server 2014 버전에서 지 원하는 기능](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)합니다.  
  
## <a name="user-action"></a>사용자 동작  
 sp_detach_db 저장 프로시저를 사용하여 데이터베이스를 분리합니다. 필요한 경우 파일을 이동한 다음 CREATE DATABASE와 함께 FOR ATTACH 또는 FOR ATTACH_REBUILD_LOG 옵션을 사용하여 지원되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전의 인스턴스에 데이터베이스를 연결합니다. 모든 테이블에서 분할을 사용할 수 없게 설정하고 파티션 함수를 제거합니다. 데이터베이스를 다시 분리한 다음 현재 서버에 다시 연결합니다.  
  
  
