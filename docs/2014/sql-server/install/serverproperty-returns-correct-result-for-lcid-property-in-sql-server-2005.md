---
title: SQL Server 2005에서 SERVERPROPERTY LCID 속성에 대해 올바른 결과 반환 합니다. | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- SERVERPROPERTY function
ms.assetid: 833a2fc9-b480-4697-aa7b-9677e78ee0b4
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a05202e19e95e719c8518f785be7ee1a1fbd8fff
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48163103"
---
# <a name="serverproperty-returns-correct-result-for-lcid-property-in-sql-server-2005"></a>SQL Server 2005에서 SERVERPROPERTY는 LCID 속성에 대해 올바른 결과를 반환합니다.
  SERVERPROPERTY('LCID')가 이진 데이터 정렬 서버에서 실행될 경우 이 함수는 서버의 데이터 정렬에 해당하는 Windows LCID(로캘 ID)를 반환합니다.  
  
> [!NOTE]  
>  SERVERPROPERTY('LCID')에 대한 참조를 포함하고 다른 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대해 실행되는 배치 및 추적 파일의 경우 업그레이드 관리자는 다른 인스턴스에 현재 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스와 동일한 데이터 정렬이 있는 경우에만 이 동작 변경을 감지합니다.  
  
## <a name="corrective-action"></a>수정 동작  
 SERVERPROPERTY('LCID')가 서버의 데이터 정렬에 해당하는 Windows LCID를 반환하도록 응용 프로그램을 수정합니다.  
  
## <a name="see-also"></a>관련 항목  
 [데이터베이스 엔진 업그레이드 문제](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 업그레이드 관리자 &#91;새로 만들기&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
