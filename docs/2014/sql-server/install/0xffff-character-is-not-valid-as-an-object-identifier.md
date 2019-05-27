---
title: 0xFFFF 문자는 개체 식별자 올바르지 않습니다. | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- 0xFFFF character [SQL Server]
ms.assetid: b2c9c8cf-9194-45e0-be6b-2d5ec52e8153
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c35c7c65bc312cd20c057b5e2603e7a8f77ce8c8
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66096915"
---
# <a name="0xffff-character-is-not-valid-as-an-object-identifier"></a>0xFFFF 문자는 개체 식별자로 사용할 수 없습니다.
  업그레이드 관리자가 개체 식별자에서 0xFFFF 문자를 검색했습니다. [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이상 버전에서는 데이터베이스 호환성 모드가 90 이상으로 설정된 경우 해당 식별자에 이 문자가 들어 있는 데이터베이스, 테이블 및 열과 같은 개체를 참조하거나 이름을 바꿀 수 없습니다. [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]로 업그레이드할 때 사용자 데이터베이스는 호환성 모드를 유지합니다. 데이터베이스 호환성 모드를 90 이상으로 변경하기 전에 0xFFFF 문자가 들어 있는 개체의 이름을 바꾸십시오.  
  
 식별자에 대한 자세한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 온라인 설명서에서 "식별자"를 참조하십시오. 데이터베이스 호환성 모드에 대한 자세한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 온라인 설명서에서 "sp_dbcmptlevel"을 참조하십시오.  
  
## <a name="component"></a>구성 요소  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="see-also"></a>관련 항목  
 [데이터베이스 엔진 업그레이드 문제](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 업그레이드 관리자 &#91;새로 만들기&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
