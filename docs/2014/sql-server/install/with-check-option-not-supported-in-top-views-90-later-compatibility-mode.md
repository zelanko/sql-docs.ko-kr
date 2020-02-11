---
title: 90 이상 호환성 모드의 TOP이 포함 된 뷰에서는 WITH CHECK OPTION이 지원 되지 않습니다. | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- TOP clause
- WITH CHECK OPTION clause
ms.assetid: 1b9581d0-bad9-43e0-b8fc-f32d8a8a04ca
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 254969e6201795e2f4ae512e03be26419b71d866
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66090999"
---
# <a name="with-check-option-is-not-supported-in-views-that-contain-top-in-90-or-later-compatibility-modes"></a>호환성 모드 90 이상의 TOP이 포함된 뷰에서는 WITH CHECK OPTION이 지원되지 않습니다.
  업그레이드 관리자가 뷰의 SELECT 문이나 참조된 뷰에서 WITH CHECK OPTION 및 TOP 절을 사용하는 뷰를 검색했습니다. 데이터베이스 호환성 모드를 80 이하 모드로 설정한 상태에서 뷰를 이러한 방식으로 정의하면 해당 뷰를 통해 데이터가 잘못 수정될 수 있으며 부정확한 결과가 나올 수 있습니다. 뷰 또는 참조된 뷰가 TOP 절을 사용하고 데이터베이스 호환성 모드가 90 이상으로 설정된 경우에는 뷰를 통해 데이터를 삽입하거나 업데이트할 수 없습니다.  
  
## <a name="component"></a>구성 요소  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>수정 동작  
 업그레이드할 때 사용자 데이터베이스는 호환성 모드를 유지합니다. 뷰를 통해 데이터를 수정해야 하는 경우 데이터베이스 호환성 모드를 100 이상으로 변경하기 전에 WITH CHECK OPTION과 TOP를 둘 다 사용하는 뷰를 수정합니다. 자세한 내용은 [sp_dbcmptlevel &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-dbcmptlevel-transact-sql)를 참조 하세요.  
  
## <a name="see-also"></a>참고 항목  
 [업그레이드 문제 데이터베이스 엔진](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 업그레이드 관리자 &#91;새&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
