---
description: Integration Services 테이블(Transact-SQL)
title: Integration Services 테이블 (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- SQL Server Integration Services system tables
- system tables [SQL Server], Integration Services
- system tables [Integration Services]
- SSIS, system tables
ms.assetid: 683b181b-0091-4a9c-86db-bc577af43cec
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 05f7e319dbaec37761eb5488f9d9a33cce09f3a4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88473254"
---
# <a name="integration-services-tables-transact-sql"></a>Integration Services 테이블(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  이 섹션의 항목에서는에서 사용 하는 정보를 저장 하는 msdb 데이터베이스의 시스템 테이블에 대해 설명 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
## <a name="in-this-section"></a>섹션 내용  
 [sysssislog](../../relational-databases/system-tables/sysssislog-transact-sql.md)  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지가 런타임에 생성하는 각 로그 항목에 대해 한 행을 포함합니다.  
  
 이 테이블은 패키지에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그 공급자를 사용할 때만 사용됩니다.  
  
 [sysssispackagefolders](../../relational-databases/system-tables/sysssispackagefolders-transact-sql.md)  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스가 패키지를 구성하기 위해 사용하는 각 논리적 폴더에 대해 한 행을 포함합니다. 열 값은 중첩된 폴더 간의 부모/자식 관계를 정의합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]는 사용자가 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스에 연결할 때 저장된 패키지를 계층 뷰로 표시합니다.  
  
 [sysssispackages](../../relational-databases/system-tables/sysssispackages-transact-sql.md)  
 각 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지에 대해 한 행을 포함합니다.  
  
 이 테이블은 패키지를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 저장할 때만 사용됩니다.  
  
  
