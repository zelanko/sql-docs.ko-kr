---
title: dbo.syscategories (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dbo.syscategories_TSQL
- syscategories
- syscategories_TSQL
- dbo.syscategories
dev_langs:
- TSQL
helpviewer_keywords:
- syscategories system table
ms.assetid: eb2cb75c-dc58-4a5b-b329-664e9fe20ce0
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0ee0509469f7a9bddca066a6e05416a13685ad9e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47703521"
---
# <a name="dbosyscategories-transact-sql"></a>dbo.syscategories(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 작업, 경고 및 연산자를 구성하는 데 사용되는 범주를 포함합니다. 이 테이블에 저장 되는 **msdb** 데이터베이스입니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**category_id**|**int**|범주의 ID입니다.|  
|**category_class**|**int**|범주 항목의 유형입니다.<br /><br /> **1** = Job<br /><br /> **2** = 경고<br /><br /> **3** = 연산자|  
|**category_type**|**tinyint**|범주의 유형입니다.<br /><br /> **1** = 로컬<br /><br /> **2** = 다중 서버<br /><br /> **3** = 없음|  
|**name**|**sysname**|범주의 이름입니다.|  
  
  
