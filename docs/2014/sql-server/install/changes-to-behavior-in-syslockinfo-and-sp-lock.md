---
title: Syslockinfo 및 sp_lock의 동작 변경 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- syslockinfo
- sp_lock
ms.assetid: b9892ae3-ac15-48be-8b52-78dbed6467ed
caps.latest.revision: 27
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: eb410a4c65d9b626290297fce85ddf2fe20c08d6
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37295863"
---
# <a name="changes-to-behavior-in-syslockinfo-and-splock"></a>syslockinfo 및 sp_lock의 동작에 대한 변경입니다.
  **syslockinfo** 및 **sp_lock** 이 예기치 않은 값을 반환할 수 있으며 추가 행을 반환할 수도 있습니다. 반면에 이전 버전에서는 **syslockinfo** 및 **sp_lock** 이 잠금 리소스당 최대 두 개의 행을 반환했습니다.  
  
 **syslockinfo** 의 정보에 액세스하거나 **sp_lock** 을 실행하려면 서버에 대해 VIEW SERVER STATE 권한이 필요합니다.  
  
## <a name="component"></a>구성 요소  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Description  
 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)], **rsc_objid** 하 고 **rsc_indid** 에서 열 **syslockinfo** 와 **objid** 및 **indid ** 열에서 **sp_lock** 개체 ID를 반환 하는 일관 되 고 인덱스 id입니다. [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]에서는 값 0이 반환될 수 있습니다.  
  
 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)], **syslockinfo** 하 고 **sp_lock** 단일 트랜잭션에서 지정한 잠금 리소스에 대해 두 행의 최대값을 반환 합니다. [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]부터 잠금 분할을 사용할 경우 한 트랜잭션에서 실행 중인 동일한 리소스에 대해 여러 개의 행이 반환될 수 있습니다. 있습니다 최대 N + 1 개 행을 반환할 수 있으며 여기서 N은 Cpu 수입니다. 또한 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]에서는 가능하지 않았지만 이제는 동일한 리소스에 대해 GRANTED 및 WAITING 요청을 표시할 수 있습니다.  
  
## <a name="permissions"></a>사용 권한  
 을 실행하려면 서버에 대해 VIEW SERVER STATE 권한이 필요합니다.  
  
## <a name="see-also"></a>관련 항목  
 [데이터베이스 엔진 업그레이드 문제](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 업그레이드 관리자 &#91;새로 만들기&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
