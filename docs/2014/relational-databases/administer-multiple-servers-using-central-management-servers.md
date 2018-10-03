---
title: 중앙 관리 서버를 사용하여 여러 서버 관리 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- multiserver queries
- central management server
- multiserver administration [SQL Server]
- master servers [SQL Server], central management servers
- target configuration [SQL Server]
- server configuration [SQL Server]
ms.assetid: 427911a7-57d4-4542-8846-47c3267a5d9c
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 62a954706d2e96cc83214df8c532994776b1be3f
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48205313"
---
# <a name="administer-multiple-servers-using-central-management-servers"></a>중앙 관리 서버를 사용하여 여러 서버 관리
  중앙 관리 서버를 지정하고 서버 그룹을 만들어 여러 서버를 관리할 수 있습니다.  
  
## <a name="benefits-of-central-management-servers-and-server-groups"></a>중앙 관리 서버 및 서버 그룹의 이점  
 중앙 관리 서버로 지정된 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스는 하나 이상의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스에 대한 연결 정보를 포함하는 서버 그룹을 유지 관리합니다. 서버 그룹에 대해 [!INCLUDE[tsql](../includes/tsql-md.md)] 문과 정책 기반 관리 정책을 동시에 실행할 수 있습니다. 중앙 관리 서버를 통해 관리되는 인스턴스에서 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 로그 파일을 볼 수도 있습니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 이전의 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] 버전은 중앙 관리 서버로 지정할 수 없습니다.  
  
 [!INCLUDE[tsql](../includes/tsql-md.md)] 문을 실행할 수도 있습니다.  
  
### <a name="related-tasks"></a>관련 작업  
 중앙 관리 서버 및 서버 그룹을 만들려면 **의** 등록된 서버 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]창을 사용합니다. 중앙 관리 서버는 자신이 유지 관리하는 그룹의 멤버가 될 수 없습니다. 중앙 관리 서버 및 서버 그룹을 만드는 방법은 [중앙 관리 서버 및 서버 그룹 만들기&#40;SQL Server Management Studio&#41;](../ssms/register-servers/create-a-central-management-server-and-server-group.md)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [정책 기반 관리를 사용하여 서버 관리](policy-based-management/administer-servers-by-using-policy-based-management.md)  
  
  
