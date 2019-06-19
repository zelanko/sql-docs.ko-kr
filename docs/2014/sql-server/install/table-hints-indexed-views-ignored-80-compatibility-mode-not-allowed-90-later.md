---
title: 인덱싱된 뷰 정의 호환성 모드 80에서는 무시 되 고 모드를 90 이상에서는 허용 되지 않습니다의 테이블 힌트 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- query hints [SQL Server]
- indexed views [SQL Server], query hints
ms.assetid: 405dfcff-a3a6-4e6d-a53a-ed77bbacdd13
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 69a6bae06b1cb5d7a727ff2582f10bccf1e21ca8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66091813"
---
# <a name="table-hints-in-indexed-view-definitions-are-ignored-in-80-compatibility-mode-and-are-not-allowed-in-90-mode-or-later"></a>인덱싱된 뷰 정의의 테이블 힌트는 호환성 모드 80에서는 무시되고 호환성 모드 90 이상에서는 허용되지 않습니다.
  인덱싱된 뷰 정의에서 테이블 힌트는 호환성 모드 90 이상에서 허용되지 않습니다. 자세한 내용은의 다음 항목을 참조 하세요. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Books Onl 온라인 설명서: "인덱싱된 뷰 디자인" 인덱싱된 뷰 만들기"," 및 "쿼리 힌트 ([!INCLUDE[tsql](../../includes/tsql-md.md)])."  
  
## <a name="component"></a>구성 요소  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>수정 동작  
 인덱싱된 뷰 정의에서 테이블 힌트를 제거해야 합니다. 사용하는 호환성 모드에 관계없이 응용 프로그램을 테스트하는 것이 좋습니다. 응용 프로그램을 테스트하면 인덱싱된 뷰가 쿼리와 일치될 때를 비롯하여 인덱싱된 뷰가 작성, 업데이트 및 액세스될 때 응용 프로그램이 예상대로 실행되는지 여부를 확인할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [데이터베이스 엔진 업그레이드 문제](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 업그레이드 관리자 &#91;새로 만들기&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
