---
title: sys. filetable_system_defined_objects (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.filetable_system_defined_objects_TSQL
- filetable_system_defined_objects
- filetable_system_defined_objects_TSQL
- sys.filetable_system_defined_objects
dev_langs:
- TSQL
helpviewer_keywords:
- sys.filetable_system_defined_objects catalog view
ms.assetid: 62022e6b-46f6-495f-b14b-53f41e040361
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 0232a635267dc97f53f67309fb59d06651d918ce
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85786433"
---
# <a name="sysfiletable_system_defined_objects-transact-sql"></a>sys.filetable_system_defined_objects(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  FileTable과 관련된 시스템 정의 개체의 목록을 표시합니다. 시스템 정의 개체마다 하나의 행을 포함합니다.  
  
 FileTable을 만들면 제약 조건 및 인덱스와 같은 관련 개체가 동시에 만들어집니다. 이러한 개체는 변경하거나 삭제할 수 없으며, FileTable 자체가 삭제된 경우에만 사라집니다.  
  
 FileTables 기능에 대한 자세한 내용은 [FileTables &#40;SQL Server&#41;](../../relational-databases/blob/filetables-sql-server.md)를 참조하세요.  
  
|열|데이터 형식|Description|  
|------------|---------------|-----------------|  
|**object_id**|**int**|FileTable과 관련된 시스템 정의 개체의 개체 ID입니다.<br /><br /> **Sys. 개체**의 개체를 참조 합니다.|  
|**parent_object_id**|**int**|부모 FileTable의 개체 ID입니다.<br /><br /> **Sys. 개체**의 개체를 참조 합니다.|  
  
## <a name="see-also"></a>참고 항목  
 [FileTable 만들기, 변경 및 삭제](../../relational-databases/blob/create-alter-and-drop-filetables.md)   
 [FileTable 관리](../../relational-databases/blob/manage-filetables.md)  
  
  
