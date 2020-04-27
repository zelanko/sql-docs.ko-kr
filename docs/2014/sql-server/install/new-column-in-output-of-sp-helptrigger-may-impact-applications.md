---
title: Sp_helptrigger 출력의 새 열은 응용 프로그램에 영향을 줄 수 있습니다. | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- sp_helptrigger
ms.assetid: b7c42a8f-f2e0-4fa3-b046-3cf39c854c47
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 33d47c858a03766260e8ed8c098fef79e9e4a82f
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66093734"
---
# <a name="new-column-in-output-of-sp_helptrigger-may-impact-applications"></a>sp_helptrigger의 출력에 나타나는 새 열은 애플리케이션에 영향을 줍니다.
  sp_helptrigger 시스템 저장 프로시저에서 반환한 결과 집합의 마지막 열을 trigger_schemaias 합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 특정 테이블에 정의된 트리거에 대한 정보를 보려면 sys.triggers 카탈로그 뷰를 쿼리하십시오.  
  
## <a name="component"></a>구성 요소  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>수정 동작  
 애플리케이션에서 sp_helptrigger의 사용을 검토합니다. 추가 열을 포함하려면 애플리케이션을 수정해야 할 수 있습니다. 또는 sys.triggers 카탈로그 뷰를 대신 사용할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [업그레이드 문제 데이터베이스 엔진](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 업그레이드 관리자 &#91;새&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
