---
title: SERVERPROPERTY SQL Server 2005에서 LCID 속성에 대해 올바른 결과를 반환 합니다. Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- SERVERPROPERTY function
ms.assetid: 833a2fc9-b480-4697-aa7b-9677e78ee0b4
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 24bb31759ba520f26b8e9af3a6533d8f0feebbe0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66092236"
---
# <a name="serverproperty-returns-correct-result-for-lcid-property-in-sql-server-2005"></a>SQL Server 2005에서 SERVERPROPERTY는 LCID 속성에 대해 올바른 결과를 반환합니다.
  SERVERPROPERTY('LCID')가 이진 데이터 정렬 서버에서 실행될 경우 이 함수는 서버의 데이터 정렬에 해당하는 Windows LCID(로캘 ID)를 반환합니다.  
  
> [!NOTE]  
>  SERVERPROPERTY('LCID')에 대한 참조를 포함하고 다른 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 대해 실행되는 배치 및 추적 파일의 경우 업그레이드 관리자는 다른 인스턴스에 현재 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스와 동일한 데이터 정렬이 있는 경우에만 이 동작 변경을 감지합니다.  
  
## <a name="corrective-action"></a>수정 동작  
 SERVERPROPERTY('LCID')가 서버의 데이터 정렬에 해당하는 Windows LCID를 반환하도록 애플리케이션을 수정합니다.  
  
## <a name="see-also"></a>참고 항목  
 [업그레이드 문제 데이터베이스 엔진](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 업그레이드 관리자 &#91;새&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
