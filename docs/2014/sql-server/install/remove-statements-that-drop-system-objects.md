---
title: 시스템 개체를 삭제 하는 문을 제거 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- drop system objects [SQL Server]
ms.assetid: cdfc3c50-c801-4039-a4bf-b35f876f1c61
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 1d420e2dba1dfdb284b0002eca6d8408c4e019e8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66093083"
---
# <a name="remove-statements-that-drop-system-objects"></a>시스템 개체를 삭제하는 문을 제거합니다.
  업그레이드 관리자가 시스템 개체를 삭제하는 문을 검색했습니다. 확장 저장 프로시저를 비롯한 시스템 개체는 읽기 전용 **리소스** 데이터베이스(mssqlsystemresource)에 배포되므로 삭제할 수 없습니다. 애플리케이션을 수정하여 시스템 개체에 대한 EXECUTE 권한을 취소하거나 거부합니다.  
  
## <a name="component"></a>구성 요소  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Description  
 시스템 개체는 읽기 전용 **리소스** 데이터베이스에 배포되므로 DROP TABLE, DROP PROCEDURE 및 **sp_dropextendedproc** 과 같은 문을 사용하여 제거할 수 없습니다.  
  
## <a name="corrective-action"></a>수정 동작  
 애플리케이션에서 시스템 개체를 삭제하는 문을 모두 제거합니다. 애플리케이션을 수정하여 시스템 개체에 대한 EXECUTE 권한을 취소하거나 거부합니다. 또는 SAC(노출 영역 구성) 도구를 사용하여 이러한 개체 중 일부를 비활성화할 수 있습니다. 예를 들어 SAC 도구를 사용하여 **xp_cmdshell** 확장 저장 프로시저를 활성화하거나 비활성화할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [데이터베이스 엔진 업그레이드 문제](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 업그레이드 관리자 &#91;새로 만들기&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
