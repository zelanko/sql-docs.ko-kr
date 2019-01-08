---
title: sys.database_filestream_options (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- database_filestream_options
- sys.database_filestream_options_TSQL
- database_filestream_options_TSQL
- sys.database_filestream_options
dev_langs:
- TSQL
helpviewer_keywords:
- sys.database_filestream_options catalog view
ms.assetid: 3383c607-0bbc-456a-ab37-7230f4cbf0e9
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3038b27084dce6a84436e658c66b77dc61ead49e
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52543021"
---
# <a name="sysdatabasefilestreamoptions-transact-sql"></a>sys.database_filestream_options(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  사용하도록 설정된 FileTable의 FILESTREAM 데이터에 대한 비트랜잭션 액세스 수준과 관련된 정보를 표시합니다. SQL Server 인스턴스의 각 데이터베이스마다 하나씩의 행을 포함합니다.  
  
 FileTables 기능에 대한 자세한 내용은 [FileTables &#40;SQL Server&#41;](../../relational-databases/blob/filetables-sql-server.md)를 참조하세요.  
  
  
|Column|형식|Description|  
|------------|----------|-----------------|  
|**database_id**|**int**|데이터베이스의 ID입니다. 이 값은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 내에서 고유합니다.|  
|**directory_name**|**nvarchar(255)**|모든 FileTable 네임스페이스에 대한 데이터베이스 수준 디렉터리입니다.|  
|**non_transacted_access**|**tinyint**|사용하도록 설정된 FILESTREAM 데이터에 대한 비트랜잭션 액세스 수준입니다. 액세스 수준은 NON_TRANSACTED_ACCESS 옵션으로 설정 됩니다는 **CREATE DATABASE** 하거나 **ALTER DATABASE** 문.<br /><br /> 이 설정에는 다음 값 중 하나를 사용할 수 있습니다.<br /><br /> 0-사용할 수 없습니다. 이것은 기본값입니다. 이 수준은 값을 제공 하 여 설정 됩니다 **OFF** 에 대 한 합니다 **NON_TRANSACTED_ACCESS** 옵션입니다.<br /><br /> 1-읽기 전용 액세스 합니다. 이 수준은 값을 제공 하 여 설정 됩니다 **READ_ONLY** 에 대 한 합니다 **NON_TRANSACTED_ACCESS** 옵션입니다.<br /><br /> 3-전체 액세스 합니다. 이 수준은 값을 제공 하 여 설정 됩니다 **전체** 에 대 한 합니다 **NON_TRANSACTED_ACCESS** 옵션입니다.<br /><br /> 5 - READONLY로 전환 중<br /><br /> 6-OFF로 전환 중|  
|**non_transacted_access_desc**|**nvarchar(60)**|Non_transacted_access에서 식별 된 비트랜잭션 액세스 수준 설명입니다.<br /><br /> 이 설정에는 다음 값 중 하나를 사용할 수 있습니다.<br /><br /> 없음-이 값은 기본값입니다.<br /><br /> READ_ONLY<br /><br /> FULL<br /><br /> IN_TRANSITION_TO_READ_ONLY<br /><br /> IN_TRANSITION_TO_OFF|  
  
## <a name="see-also"></a>관련 항목  
 [FileTable의 필수 구성 요소를 사용하도록 설정](../../relational-databases/blob/enable-the-prerequisites-for-filetable.md)  
  
  
