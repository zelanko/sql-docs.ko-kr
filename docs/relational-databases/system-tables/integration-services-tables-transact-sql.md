---
title: Integration Services 테이블 (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- SQL Server Integration Services system tables
- system tables [SQL Server], Integration Services
- system tables [Integration Services]
- SSIS, system tables
ms.assetid: 683b181b-0091-4a9c-86db-bc577af43cec
caps.latest.revision: 21
author: douglasl
ms.author: douglasl
manager: craigg
ms.openlocfilehash: fc5df46211b3de92b054fea4120d9b7c884a0ccb
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
---
# <a name="integration-services-tables-transact-sql"></a>Integration Services 테이블(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  이 섹션의 항목에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]에서 사용하는 정보를 저장하는 msdb 데이터베이스의 시스템 테이블에 대해 설명합니다.  
  
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
  
  
