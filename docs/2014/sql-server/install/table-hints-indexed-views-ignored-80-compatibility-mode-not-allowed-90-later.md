---
title: 테이블 힌트에 인덱싱된 뷰 정의 호환성 모드 80에서는 무시 되 고 이상 90 이상의 모드에서 허용 되지 않습니다 | Microsoft Docs
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
- query hints [SQL Server]
- indexed views [SQL Server], query hints
ms.assetid: 405dfcff-a3a6-4e6d-a53a-ed77bbacdd13
caps.latest.revision: 22
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: b56e965ecfcfc802457bfa3b5a78118afae5c531
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36093673"
---
# <a name="table-hints-in-indexed-view-definitions-are-ignored-in-80-compatibility-mode-and-are-not-allowed-in-90-mode-or-later"></a>인덱싱된 뷰 정의의 테이블 힌트는 호환성 모드 80에서는 무시되고 호환성 모드 90 이상에서는 허용되지 않습니다.
  인덱싱된 뷰 정의에서 테이블 힌트는 호환성 모드 90 이상에서 허용되지 않습니다. 자세한 내용은의 다음 항목을 참조 하십시오. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 온라인 설명서: "디자인 인덱싱된 뷰," 인덱싱된 뷰 만들기, "및" 쿼리 힌트 ([!INCLUDE[tsql](../../includes/tsql-md.md)]). "  
  
## <a name="component"></a>구성 요소  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>수정 동작  
 인덱싱된 뷰 정의에서 테이블 힌트를 제거해야 합니다. 사용하는 호환성 모드에 관계없이 응용 프로그램을 테스트하는 것이 좋습니다. 응용 프로그램을 테스트하면 인덱싱된 뷰가 쿼리와 일치될 때를 비롯하여 인덱싱된 뷰가 작성, 업데이트 및 액세스될 때 응용 프로그램이 예상대로 실행되는지 여부를 확인할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [데이터베이스 엔진 업그레이드 문제](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 업그레이드 관리자 &#91;new&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
