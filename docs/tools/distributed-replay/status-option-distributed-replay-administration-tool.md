---
title: "상태 옵션 (Distributed Replay Administration Tool) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ea89386e-1598-4412-8b37-680d14b2a5b6
caps.latest.revision: 17
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 6831b370359b7540621eb8d69bdf070689edd9a2
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="status-option-distributed-replay-administration-tool"></a>상태 옵션(Distributed Replay Administration Tool)
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay 관리 도구인 **DReplay.exe**는 Distributed Replay Controller와 통신하는 데 사용할 수 있는 명령줄 도구입니다. 이 항목에서는 **status** 명령줄 옵션과 해당 구문에 대해 설명합니다.  
  
 **status** 옵션은 컨트롤러를 쿼리하여 현재 상태를 표시합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") 관리 도구 구문과 함께 사용 되는 구문 표기 규칙에 대 한 자세한 내용은 참조 하십시오. [TRANSACT-SQL 구문 표기 규칙 &#40; Transact SQL &#41; ](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).  
  
## <a name="syntax"></a>구문  
  
```  
  
dreplay status [-m controller] [-f status_interval]  
```  
  
#### <a name="parameters"></a>매개 변수  
 **-m** *controller*  
 컨트롤러의 컴퓨터 이름을 지정합니다. "`localhost`" 또는 "`.`"을 사용하여 로컬 컴퓨터를 참조할 수 있습니다.  
  
 **-m** 매개 변수를 지정하지 않으면 로컬 컴퓨터가 사용됩니다.  
  
 **-f** *status_interval*  
 상태를 표시할 빈도(초)를 지정합니다.  
  
 **-f** 매개 변수를 지정하지 않을 경우 기본 간격은 30초입니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 현재 상태가 60초 간격으로 표시됩니다. `localhost` 값은 컨트롤러 서비스가 관리 도구와 동일한 컴퓨터에서 실행 중임을 나타냅니다.  
  
```  
dreplay status –m localhost -f 60  
```  
  
## <a name="permissions"></a>사용 권한  
 관리 도구는 로컬 사용자 또는 도메인 사용자 등의 대화형 사용자 계정으로 실행해야 합니다. 로컬 사용자 계정을 사용하려면 관리 도구와 컨트롤러가 동일한 컴퓨터에서 실행되고 있어야 합니다.  
  
 자세한 내용은 [Distributed Replay Security](../../tools/distributed-replay/distributed-replay-security.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server Distributed Replay](../../tools/distributed-replay/sql-server-distributed-replay.md)   
 [Transact-SQL 디버거](../../relational-databases/scripting/transact-sql-debugger.md)  
  
  

