---
title: sysssispackagefolders (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysdtspackagefolders90
- sysdtspackagefolders90_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysssispackagefolders system table
ms.assetid: ddc4833f-27bf-4610-b739-d257961d17ac
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 7c1a5e117ee1c79b918f9785310b9b7c97671729
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56025824"
---
# <a name="sysssispackagefolders-transact-sql"></a>sysssispackagefolders(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  폴더 계층 구조에서 각 논리적 폴더에 대 한 하나의 행을 포함 하는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 사용 합니다. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에 연결하면 이 폴더가 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]의 개체 탐색기에 나열됩니다. 폴더에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 파일 시스템에 저장된 패키지가 나열됩니다.  
  
 합니다 **parentfolderid** 열은 폴더 계층 구조에 설명 합니다. 폴더 계층의 맨 위에 있는 폴더에 null 값을 포함 **parentfolderid**합니다.  
  
 합니다 **foldername** 열 개체 탐색기에 표시 되는 폴더의 이름을 포함 합니다.  
  
 이 테이블에 저장 되는 **msdb** 데이터베이스입니다.  

  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**folderid**|**uniqueidentifier**|폴더의 GUID입니다.|  
|**parentfolderid**|**uniqueidentifier**|부모 폴더의 GUID입니다.|  
|**foldername**|**sysname**|폴더 이름입니다. 이 이름은 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]의 폴더 계층 구조에 나타납니다.|  
  
  
