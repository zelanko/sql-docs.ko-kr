---
title: FileTable 스키마 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.technology: filestream
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- FileTables [SQL Server], table schema
ms.assetid: e1cb3880-cfda-40ac-91fc-d08998287f44
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 67578dadba93af562732a6e0152e13a3c180195d
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37425032"
---
# <a name="filetable-schema"></a>FileTable 스키마
  FileTable의 미리 정의된 고정 스키마에 대해 설명합니다.  
  
|파일 특성 이름|유형|크기|Default|Description|파일 시스템 접근성|  
|-------------------------|----------|----------|-------------|-----------------|-------------------------------|  
|**path_locator**|`hierarchyid`|변수|`hierarchyid` 이 항목의 위치를 식별 하는 합니다.|계층적 FileNamespace에서 이 노드의 위치입니다.<br /><br /> 테이블의 기본 키입니다.|Windows 경로 값을 설정하여 만들고 수정할 수 있습니다.|  
|**stream_id**|**[uniqueidentifier] rowguidcol**||반환 된 값을 `NEWID()` 함수입니다.|FILESTREAM 데이터의 고유 ID입니다.|이 오류에는 이 작업을 적용할 수 없습니다.|  
|**file_stream**|`varbinary(max)`<br /><br /> `filestream`|변수|NULL|FILESTREAM 데이터를 포함합니다.|이 오류에는 이 작업을 적용할 수 없습니다.|  
|**file_type**|`nvarchar(255)`|변수|NULL<br /><br /> 파일 시스템에서 만들기 또는 이름 바꾸기 작업을 수행하면 해당 이름에서 파일 확장명 값이 채워집니다.|파일의 유형을 나타냅니다.<br /><br /> 전체 텍스트 인덱스를 만들 때 이 열을 `TYPE COLUMN`으로 사용할 수 있습니다.<br /><br /> **file_type** 은 지속형 계산 열입니다.|자동으로 계산되며, 수동으로 설정할 수 없습니다.|  
|**이름**|`nvarchar(255)`|변수|GUID 값|파일 또는 디렉터리 이름입니다.|Windows API를 사용하여 만들거나 수정할 수 있습니다.|  
|**parent_path_locator**|`hierarchyid`|변수|이 항목을 포함하는 디렉터리를 식별하는 `hierarchyid`입니다.|`hierarchyid` 포함 디렉터리입니다.<br /><br /> **parent_path_locator** 는 지속형 계산 열입니다.|자동으로 계산되며, 수동으로 설정할 수 없습니다.|  
|**cached_file_size**|`bigint`|||FILESTREAM 데이터의 크기(바이트)입니다.<br /><br /> **cached_file_size** 는 지속형 계산 열입니다.|캐시된 파일 크기는 자동으로 최신 상태로 업데이트되지만 특수한 상황에서는 동기화되지 않을 수 있습니다. 정확한 크기를 계산 하려면를 `DATALENGTH()` 함수입니다.|  
|**creation_time**|`datetime2(4)`<br /><br /> `not null`|8바이트|현재 시간입니다.|파일을 만든 날짜와 시간입니다.|자동으로 계산되며, Windows API를 사용하여 설정할 수도 있습니다.|  
|**last_write_time**|`datetime2(4)`<br /><br /> `not null`|8바이트|현재 시간입니다.|파일을 마지막으로 업데이트한 날짜와 시간입니다.|자동으로 계산되며, Windows API를 사용하여 설정할 수도 있습니다.|  
|**last_access_time**|`datetime2(4)`<br /><br /> `not null`|8바이트|현재 시간입니다.|파일에 마지막으로 액세스한 날짜와 시간입니다.|자동으로 계산되며, Windows API를 사용하여 설정할 수도 있습니다.|  
|**is_directory**|`bit`<br /><br /> `not null`|1바이트|FALSE|행이 디렉터리를 나타내는지 여부를 표시합니다. 이 값은 자동으로 계산되며, 수동으로 설정할 수 없습니다.|자동으로 계산되며, 수동으로 설정할 수 없습니다.|  
|**is_offline**|`bit`<br /><br /> `not null`|1바이트|FALSE|오프라인 파일 특성입니다.|자동으로 계산되며, Windows API를 사용하여 설정할 수도 있습니다.|  
|**is_hidden**|`bit`<br /><br /> `not null`|1바이트|FALSE|숨겨진 파일 특성입니다.|자동으로 계산되며, Windows API를 사용하여 설정할 수도 있습니다.|  
|**is_readonly**|`bit`<br /><br /> `not null`|1바이트|FALSE|읽기 전용 파일 특성입니다.|자동으로 계산되며, Windows API를 사용하여 설정할 수도 있습니다.|  
|**is_archive**|`bit`<br /><br /> `not null`|1바이트|FALSE|보관 특성입니다.|자동으로 계산되며, Windows API를 사용하여 설정할 수도 있습니다.|  
|**is_system**|`bit`<br /><br /> `not null`|1바이트|FALSE|시스템 파일 특성입니다.|자동으로 계산되며, Windows API를 사용하여 설정할 수도 있습니다.|  
|**is_temporary**|`bit`<br /><br /> `not null`|1바이트|FALSE|임시 파일 특성입니다.|자동으로 계산되며, Windows API를 사용하여 설정할 수도 있습니다.|  
  
## <a name="see-also"></a>관련 항목  
 [FileTable 만들기, 변경 및 삭제](create-alter-and-drop-filetables.md)  
  
  
