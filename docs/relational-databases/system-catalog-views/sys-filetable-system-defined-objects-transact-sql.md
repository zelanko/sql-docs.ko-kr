---
title: sys.filetable_system_defined_objects (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.filetable_system_defined_objects_TSQL
- filetable_system_defined_objects
- filetable_system_defined_objects_TSQL
- sys.filetable_system_defined_objects
dev_langs: TSQL
helpviewer_keywords: sys.filetable_system_defined_objects catalog view
ms.assetid: 62022e6b-46f6-495f-b14b-53f41e040361
caps.latest.revision: "9"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c3bd6bd8368525c94ce0d999af921c76c2cade96
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="sysfiletablesystemdefinedobjects-transact-sql"></a>sys.filetable_system_defined_objects(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  FileTable과 관련된 시스템 정의 개체의 목록을 표시합니다. 시스템 정의 개체마다 하나의 행을 포함합니다.  
  
 FileTable을 만들면 제약 조건 및 인덱스와 같은 관련 개체가 동시에 만들어집니다. 이러한 개체는 변경하거나 삭제할 수 없으며, FileTable 자체가 삭제된 경우에만 사라집니다.  
  
 Filetable에 대 한 자세한 내용은 참조 [Filetable &#40; SQL Server &#41; ](../../relational-databases/blob/filetables-sql-server.md).  
  
|열|데이터 형식|Description|  
|------------|---------------|-----------------|  
|**object_id**|**int**|FileTable과 관련된 시스템 정의 개체의 개체 ID입니다.<br /><br /> 개체를 참조 **sys.objects**합니다.|  
|**parent_object_id**|**int**|부모 FileTable의 개체 ID입니다.<br /><br /> 개체를 참조 **sys.objects**합니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [FileTable 만들기, 변경 및 삭제](../../relational-databases/blob/create-alter-and-drop-filetables.md)   
 [FileTable 관리](../../relational-databases/blob/manage-filetables.md)  
  
  
