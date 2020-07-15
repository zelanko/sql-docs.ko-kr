---
title: FileTable 스키마 | Microsoft 문서
description: 디렉터리 구조를 사용하여 파일을 저장하는 SQL Server 기능인 사전 정의 및 고정형 FileTable 스키마에 대해 알아봅니다.
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FileTables [SQL Server], table schema
ms.assetid: e1cb3880-cfda-40ac-91fc-d08998287f44
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 49199c617f916413e79a5c6ffc71e6c4f21a69e0
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85767977"
---
# <a name="filetable-schema"></a>FileTable 스키마
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  FileTable의 미리 정의된 고정 스키마에 대해 설명합니다.  
  
|파일 특성 이름|type|크기|기본값|Description|파일 시스템 접근성|  
|-------------------------|----------|----------|-------------|-----------------|-------------------------------|  
|**path_locator**|**hierarchyid**|변수|이 항목의 위치를 식별하는 **hierarchyid** 입니다.|계층적 FileNamespace에서 이 노드의 위치입니다.<br /><br /> 테이블의 기본 키입니다.|Windows 경로 값을 설정하여 만들고 수정할 수 있습니다.|  
|**stream_id**|**[uniqueidentifier] rowguidcol**||**NEWID()** 함수가 반환하는 값|FILESTREAM 데이터의 고유 ID입니다.|해당 사항 없음|  
|**file_stream**|**varbinary(max)**<br /><br /> **filestream**|변수|NULL|FILESTREAM 데이터를 포함합니다.|해당 사항 없음|  
|**file_type**|**nvarchar(255)**|변수|NULL<br /><br /> 파일 시스템에서 만들기 또는 이름 바꾸기 작업을 수행하면 해당 이름에서 파일 확장명 값이 채워집니다.|파일의 유형을 나타냅니다.<br /><br /> 전체 텍스트 인덱스를 만들 때 이 열을 **TYPE COLUMN** 으로 사용할 수 있습니다.<br /><br /> **file_type** 은 지속형 계산 열입니다.|자동으로 계산되며, 수동으로 설정할 수 없습니다.|  
|**이름**|**nvarchar(255)**|변수|GUID 값|파일 또는 디렉터리 이름입니다.|Windows API를 사용하여 만들거나 수정할 수 있습니다.|  
|**parent_path_locator**|**hierarchyid**|변수|이 항목을 포함하는 디렉터리를 식별하는 **hierarchyid** 입니다.|포함 디렉터리의 **hierarchyid** 입니다.<br /><br /> **parent_path_locator** 는 지속형 계산 열입니다.|자동으로 계산되며, 수동으로 설정할 수 없습니다.|  
|**cached_file_size**|**bigint**|||FILESTREAM 데이터의 크기(바이트)입니다.<br /><br /> **cached_file_size** 는 지속형 계산 열입니다.|캐시된 파일 크기는 자동으로 최신 상태로 업데이트되지만 특수한 상황에서는 동기화되지 않을 수 있습니다. 정확한 크기를 계산하려면 **DATALENGTH()** 함수를 사용하세요.|  
|**creation_time**|**datetime2(4)**<br /><br /> **Null이 아님**|8바이트|현재 시간입니다.|파일을 만든 날짜와 시간입니다.|자동으로 계산되며, Windows API를 사용하여 설정할 수도 있습니다.|  
|**last_write_time**|**datetime2(4)**<br /><br /> **Null이 아님**|8바이트|현재 시간입니다.|파일을 마지막으로 업데이트한 날짜와 시간입니다.|자동으로 계산되며, Windows API를 사용하여 설정할 수도 있습니다.|  
|**last_access_time**|**datetime2(4)**<br /><br /> **Null이 아님**|8바이트|현재 시간입니다.|파일에 마지막으로 액세스한 날짜와 시간입니다.|자동으로 계산되며, Windows API를 사용하여 설정할 수도 있습니다.|  
|**is_directory**|**bit**<br /><br /> **Null이 아님**|1바이트|FALSE|행이 디렉터리를 나타내는지 여부를 표시합니다. 이 값은 자동으로 계산되며, 수동으로 설정할 수 없습니다.|자동으로 계산되며, 수동으로 설정할 수 없습니다.|  
|**is_offline**|**bit**<br /><br /> **Null이 아님**|1바이트|FALSE|오프라인 파일 특성입니다.|자동으로 계산되며, Windows API를 사용하여 설정할 수도 있습니다.|  
|**is_hidden**|**bit**<br /><br /> **Null이 아님**|1바이트|FALSE|숨겨진 파일 특성입니다.|자동으로 계산되며, Windows API를 사용하여 설정할 수도 있습니다.|  
|**is_readonly**|**bit**<br /><br /> **Null이 아님**|1바이트|FALSE|읽기 전용 파일 특성입니다.|자동으로 계산되며, Windows API를 사용하여 설정할 수도 있습니다.|  
|**is_archive**|**bit**<br /><br /> **Null이 아님**|1바이트|FALSE|보관 특성입니다.|자동으로 계산되며, Windows API를 사용하여 설정할 수도 있습니다.|  
|**is_system**|**bit**<br /><br /> **Null이 아님**|1바이트|FALSE|시스템 파일 특성입니다.|자동으로 계산되며, Windows API를 사용하여 설정할 수도 있습니다.|  
|**is_temporary**|**bit**<br /><br /> **Null이 아님**|1바이트|FALSE|임시 파일 특성입니다.|자동으로 계산되며, Windows API를 사용하여 설정할 수도 있습니다.|  
  
## <a name="see-also"></a>참고 항목  
 [FileTable 만들기, 변경 및 삭제](../../relational-databases/blob/create-alter-and-drop-filetables.md)  
  
  
