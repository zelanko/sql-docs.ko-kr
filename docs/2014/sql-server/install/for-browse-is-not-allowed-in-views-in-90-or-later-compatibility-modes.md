---
title: 90 이상 호환성 모드의 뷰에서는 FOR BROWSE를 사용할 수 없습니다. | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- views [SQL Server], FOR BROWSE clause
- FOR BROWSE clause
ms.assetid: 8f49b1c1-d877-4c46-b988-f8cdd8ac0925
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 4811a3df80257b1e2d0e903fad562568eeec4ea2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66095182"
---
# <a name="for-browse-is-not-allowed-in-views-in-90-or-later-compatibility-modes"></a>FOR BROWSE는 90 이상 호환성 모드의 뷰에서 허용되지 않습니다.
  업그레이드 관리자가 뷰에서 FOR BROWSE 절이 사용되는 것을 감지했습니다. 데이터베이스 호환성 모드가 80으로 설정되어 있는 경우 FOR BROWSE 절은 뷰에서 허용 및 무시됩니다. 데이터베이스 호환성 모드가 90 이상으로 설정된 경우에는 뷰에 FOR BROWSE 절이 허용되지 않습니다.  
  
## <a name="component"></a>구성 요소  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>수정 동작  
 업그레이드할 때 사용자 데이터베이스는 호환성 모드를 유지합니다. 데이터베이스 호환성 모드를 90 이상으로 변경하기 전에 뷰 정의에서 FOR BROWSE 절을 제거합니다. 자세한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 온라인 설명서에서 "sp_dbcmptlevel"을 참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [업그레이드 문제 데이터베이스 엔진](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 업그레이드 관리자 &#91;새&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
