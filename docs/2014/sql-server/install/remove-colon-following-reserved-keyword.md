---
title: 제거 콜론 다음 예약 키워드 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- reserved keywords
ms.assetid: 4f23f7e4-7b4d-4e19-86c9-7527bb8b107d
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ce2cfce6e35a95b7a07c17c4d3a2fd8a1b1c2610
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66093178"
---
# <a name="remove-colon-following-reserved-keyword"></a>예약 키워드 다음에 나오는 콜론을 제거합니다.
  업그레이드 관리자가 예약 키워드 뒤에서 콜론(:)이 포함된 스크립트를 감지했습니다. 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 이 구문이 무시되고 문이 성공적으로 실행되지만 이제는 데이터베이스 호환성 모드가 100 이상으로 설정된 경우 이 구문 때문에 문이 실패합니다.  
  
 사용자 데이터베이스는 호환성 모드를 유지합니다.  
  
## <a name="component"></a>구성 요소  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>수정 동작  
 데이터베이스 호환성 모드를 100 이상으로 설정하기 전에 예약 키워드 뒤에 있는 콜론을 제거하여 스크립트를 수정합니다. 자세한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 온라인 설명서에서 "sp_dbcmptlevel"을 참조하십시오.  
  
## <a name="see-also"></a>관련 항목  
 [데이터베이스 엔진 업그레이드 문제](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 업그레이드 관리자 &#91;새로 만들기&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
