---
title: sys. database_filestream_options (Transact-sql) | Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 4c9ec7c14bf192891e547c68ca85b5b055eb6815
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82823507"
---
# <a name="sysdatabase_filestream_options-transact-sql"></a>sys.database_filestream_options(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  사용하도록 설정된 FileTable의 FILESTREAM 데이터에 대한 비트랜잭션 액세스 수준과 관련된 정보를 표시합니다. SQL Server 인스턴스의 각 데이터베이스마다 하나씩의 행을 포함합니다.  
  
 FileTables 기능에 대한 자세한 내용은 [FileTables &#40;SQL Server&#41;](../../relational-databases/blob/filetables-sql-server.md)를 참조하세요.  
  
  
|Column|형식|설명|  
|------------|----------|-----------------|  
|**database_id**|**int**|데이터베이스의 ID입니다. 이 값은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 내에서 고유합니다.|  
|**directory_name**|**nvarchar(255)**|모든 FileTable 네임스페이스에 대한 데이터베이스 수준 디렉터리입니다.|  
|**non_transacted_access**|**tinyint**|사용하도록 설정된 FILESTREAM 데이터에 대한 비트랜잭션 액세스 수준입니다. 액세스 수준은 **CREATE database** 또는 **ALTER database** 문의 NON_TRANSACTED_ACCESS 옵션으로 설정 됩니다.<br /><br /> 이 설정에는 다음 값 중 하나를 사용할 수 있습니다.<br /><br /> 0-사용 안 함 이것은 기본값입니다. 이 수준은 **NON_TRANSACTED_ACCESS** 옵션의 값을 **OFF** 로 설정 하 여 설정 합니다.<br /><br /> 1-읽기 전용 액세스입니다. 이 수준은 **NON_TRANSACTED_ACCESS** 옵션에 **READ_ONLY** 값을 제공 하 여 설정 합니다.<br /><br /> 3-모든 권한 이 수준은 **NON_TRANSACTED_ACCESS** 옵션에 **FULL** 값을 제공 하 여 설정 합니다.<br /><br /> 5 - READONLY로 전환 중<br /><br /> 6-OFF로 전환|  
|**non_transacted_access_desc**|**nvarchar(60)**|Non_transacted_access에서 식별 된 비트랜잭션 액세스 수준에 대 한 설명입니다.<br /><br /> 이 설정에는 다음 값 중 하나를 사용할 수 있습니다.<br /><br /> NONE-기본값입니다.<br /><br /> READ_ONLY<br /><br /> FULL<br /><br /> IN_TRANSITION_TO_READ_ONLY<br /><br /> IN_TRANSITION_TO_OFF|  
  
## <a name="see-also"></a>참고 항목  
 [FileTable의 필수 구성 요소를 사용하도록 설정](../../relational-databases/blob/enable-the-prerequisites-for-filetable.md)  
  
  
