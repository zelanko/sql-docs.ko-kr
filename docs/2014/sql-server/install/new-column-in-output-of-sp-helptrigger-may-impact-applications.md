---
title: Sp_helptrigger의 출력에 나타나는 새 열에는 응용 프로그램 영향을 줄 수 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- sp_helptrigger
ms.assetid: b7c42a8f-f2e0-4fa3-b046-3cf39c854c47
caps.latest.revision: 18
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 2d62b9b9546fa113557bf962d68876d8c55a71ef
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36088306"
---
# <a name="new-column-in-output-of-sphelptrigger-may-impact-applications"></a>sp_helptrigger의 출력에 나타나는 새 열은 응용 프로그램에 영향을 줍니다.
  sp_helptrigger 시스템에서 반환 된 결과 집합의 마지막 열 trigger_schemaias 저장 프로시저입니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 특정 테이블에 정의된 트리거에 대한 정보를 보려면 sys.triggers 카탈로그 뷰를 쿼리하십시오.  
  
## <a name="component"></a>구성 요소  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>수정 동작  
 응용 프로그램에서 sp_helptrigger의 사용을 검토합니다. 추가 열을 포함하려면 응용 프로그램을 수정해야 할 수 있습니다. 또는 sys.triggers 카탈로그 뷰를 대신 사용할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [데이터베이스 엔진 업그레이드 문제](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 업그레이드 관리자 &#91;new&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
