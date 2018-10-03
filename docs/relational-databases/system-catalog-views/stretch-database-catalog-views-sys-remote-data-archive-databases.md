---
title: sys.remote_data_archive_databases (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: language-reference
f1_keywords:
- sys.remote_data_archive_databases
- sys.remote_data_archive_databases_TSQL
- remote_data_archive_databases
- remote_data_archive_databases_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.remote_data_archive_databases catalog view
ms.assetid: 25bffb0c-9821-40b4-88cf-75f854891a09
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 0dbf0566239b6434bb25c707ff2bb3142dbc2b15
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47607221"
---
# <a name="stretch-database-catalog-views---sysremotedataarchivedatabases"></a>카탈로그 뷰-Stretch Database sys.remote_data_archive_databases
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  스트레치가 활성화 된 로컬 데이터베이스에서 데이터를 저장 하는 각 원격 데이터베이스에 대해 하나의 행을 포함 합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**remote_database_id**|**int**|자동으로 생성 된 로컬 식별자 원격 데이터베이스의 합니다.|  
|**remote_database_name**|**sysname**|원격 데이터베이스의 이름입니다.|  
|**data_source_id**|**int**|원격 서버에 연결할 때 사용할 데이터 원본|  
  
## <a name="see-also"></a>관련 항목  
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  
