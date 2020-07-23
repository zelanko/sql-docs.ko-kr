---
title: 중앙 관리 서버를 사용하여 여러 서버 관리
description: 중앙 관리 서버를 지정하고 서버 그룹을 만들어 SQL Server에서 여러 서버를 관리하는 방법을 알아봅니다.
ms.date: 08/12/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: supportability
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
ms.custom: seo-lt-2019
ms.openlocfilehash: 9fcf805dc2c4ff9e639b43e0d6ea455d3aa439fe
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86915713"
---
# <a name="administer-multiple-servers-using-central-management-servers"></a>중앙 관리 서버를 사용하여 여러 서버 관리
[!INCLUDE[sqlserver](../includes/applies-to-version/sqlserver.md)]
  중앙 관리 서버를 지정하고 서버 그룹을 만들어 여러 서버를 관리할 수 있습니다.  
  
## <a name="what-is-a-central-management-server-and-server-groups"></a>중앙 관리 서버와 서버 그룹이란?  
 중앙 관리 서버로 지정된 SQL Server 인스턴스는 하나 이상의 인스턴스에 대한 연결 정보를 포함하는 서버 그룹을 유지 관리합니다. [!INCLUDE[tsql](../includes/tsql-md.md)] 문과 정책 기반 관리 정책을 서버 그룹에 대해 동시에 실행할 수 있습니다. 중앙 관리 서버를 통해 관리되는 인스턴스에서 로그 파일을 볼 수도 있습니다. 
 
 기본적으로 중앙 관리 서버는 관리되는 서버 목록을 포함하는 중앙 리포지토리입니다. [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] 이전의 버전은 중앙 관리 서버로 지정할 수 없습니다.  
  
 [!INCLUDE[tsql](../includes/tsql-md.md)] 문을 실행할 수도 있습니다.  
  
## <a name="create-central-management-server-and-server-groups"></a>중앙 관리 서버 및 서버 그룹 만들기 
 중앙 관리 서버 및 서버 그룹을 만들려면 **의** 등록된 서버 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]창을 사용합니다. 중앙 관리 서버는 자신이 유지 관리하는 그룹의 멤버가 될 수 없습니다. 
 
 중앙 관리 서버 및 서버 그룹을 만드는 방법에 대한 자세한 내용은 [중앙 관리 서버 및 서버 그룹 만들기&#40;SQL Server Management Studio&#41;](../tools/sql-server-management-studio/create-a-central-management-server-and-server-group.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [정책 기반 관리를 사용하여 서버 관리](../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)  
  
  
