---
title: Integration Services 테이블 (TRANSACT-SQL) | Microsoft Docs
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
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: d622158b639c912028144ab5003faef91a2030f7
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62719427"
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
  
  
