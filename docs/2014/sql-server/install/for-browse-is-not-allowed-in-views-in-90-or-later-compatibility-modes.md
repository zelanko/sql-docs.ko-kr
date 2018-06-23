---
title: 호환성 모드 90 이상에서 보기 찾아보기에서 허용 되지 않습니다는 | Microsoft Docs
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
- views [SQL Server], FOR BROWSE clause
- FOR BROWSE clause
ms.assetid: 8f49b1c1-d877-4c46-b988-f8cdd8ac0925
caps.latest.revision: 13
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 87a937dafea15fdc9eca3bbbafbacc17275374b1
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36093441"
---
# <a name="for-browse-is-not-allowed-in-views-in-90-or-later-compatibility-modes"></a>FOR BROWSE는 90 이상 호환성 모드의 뷰에서 허용되지 않습니다.
  업그레이드 관리자가 뷰에서 FOR BROWSE 절이 사용되는 것을 감지했습니다. 데이터베이스 호환성 모드가 80으로 설정되어 있는 경우 FOR BROWSE 절은 뷰에서 허용 및 무시됩니다. 데이터베이스 호환성 모드가 90 이상으로 설정된 경우에는 뷰에 FOR BROWSE 절이 허용되지 않습니다.  
  
## <a name="component"></a>구성 요소  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>수정 동작  
 업그레이드할 때 사용자 데이터베이스는 호환성 모드를 유지합니다. 데이터베이스 호환성 모드를 90 이상으로 변경하기 전에 뷰 정의에서 FOR BROWSE 절을 제거합니다. 자세한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 온라인 설명서에서 "sp_dbcmptlevel"을 참조하십시오.  
  
## <a name="see-also"></a>관련 항목  
 [데이터베이스 엔진 업그레이드 문제](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 업그레이드 관리자 &#91;new&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
