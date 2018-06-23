---
title: 0xFFFF 문자는 개체 식별자로 사용할 수 없습니다. | Microsoft Docs
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
- 0xFFFF character [SQL Server]
ms.assetid: b2c9c8cf-9194-45e0-be6b-2d5ec52e8153
caps.latest.revision: 16
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: ded2cd54bced9ae69e207a1b609688c2fcf3b633
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36093224"
---
# <a name="0xffff-character-is-not-valid-as-an-object-identifier"></a>0xFFFF 문자는 개체 식별자로 사용할 수 없습니다.
  업그레이드 관리자가 개체 식별자에서 0xFFFF 문자를 검색했습니다. [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이상 버전에서는 데이터베이스 호환성 모드가 90 이상으로 설정된 경우 해당 식별자에 이 문자가 들어 있는 데이터베이스, 테이블 및 열과 같은 개체를 참조하거나 이름을 바꿀 수 없습니다. [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]로 업그레이드할 때 사용자 데이터베이스는 호환성 모드를 유지합니다. 데이터베이스 호환성 모드를 90 이상으로 변경하기 전에 0xFFFF 문자가 들어 있는 개체의 이름을 바꾸십시오.  
  
 식별자에 대한 자세한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 온라인 설명서에서 "식별자"를 참조하십시오. 데이터베이스 호환성 모드에 대한 자세한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 온라인 설명서에서 "sp_dbcmptlevel"을 참조하십시오.  
  
## <a name="component"></a>구성 요소  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="see-also"></a>관련 항목  
 [데이터베이스 엔진 업그레이드 문제](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 업그레이드 관리자 &#91;new&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
