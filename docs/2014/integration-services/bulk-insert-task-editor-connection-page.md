---
title: 대량 삽입 태스크 편집기 (연결 페이지) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.bulkinserttask.connection.f1
helpviewer_keywords:
- Bulk Insert Task Editor
ms.assetid: 51252c20-8865-4ede-a3fd-bd73a968f47d
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 72b150ecf09dcf2c96c05ac690a366c6d2711586
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48226863"
---
# <a name="bulk-insert-task-editor-connection-page"></a>대량 삽입 태스크 편집기(연결 페이지)
  **대량 삽입 태스크 편집기** 대화 상자의 **연결** 페이지를 사용하여 대량 삽입 태스크의 원본 및 대상과 사용할 서식을 지정할 수 있습니다.  
  
 대량 삽입 작업에 대해 알아보려면 [대량 삽입 태스크](control-flow/bulk-insert-task.md) 및 [데이터를 가져오거나 내보내기 위한 서식 파일&#40;SQL Server&#41;](../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md)을 참조하세요.  
  
## <a name="options"></a>변수  
 **대량 삽입 태스크 편집기**  
 목록에서 OLE DB 연결 관리자를 선택하거나 \<**새 연결...**>을 클릭하여 새 연결을 만듭니다.  
  
 **관련 항목:** [OLE DB 연결 관리자](connection-manager/ole-db-connection-manager.md), [OLE DB 연결 관리자 구성](../../2014/integration-services/configure-ole-db-connection-manager.md)  
  
 **DestinationTable**  
 대상 테이블 또는 뷰의 이름을 입력하거나 목록에서 테이블 또는 뷰를 선택합니다.  
  
 **형식**  
 대량 삽입을 위한 서식의 원본을 선택합니다. 이 속성의 옵션은 다음 표에 나열되어 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**파일 사용**|서식 지정을 포함하는 파일을 선택합니다. 이 옵션을 선택하면 동적 옵션 **FormatFile**이 표시됩니다.|  
|**지정**|서식을 지정합니다. 이 옵션을 선택 하면 동적 옵션을 표시 `RowDelimiter` 고 `ColumnDelimiter`입니다.|  
  
 **최근에 사용한 파일**  
 목록에서 파일 또는 플랫 파일 연결 관리자를 선택하거나 \<**새 연결...**>을 클릭하여 새 연결을 만듭니다.  
  
 파일 위치는 이 태스크를 위해 연결 관리자에 지정된 SQL Server 데이터베이스 엔진의 상대적 위치입니다. 텍스트 파일은 서버의 로컬 하드 드라이브에서 또는 SQL Server에 매핑된 드라이브 또는 공유 드라이브를 통해 SQL Server 데이터베이스 엔진이 액세스할 수 있어야 합니다. 이 파일은 SSIS 런타임으로 액세스되지 않습니다.  
  
 플랫 파일 연결 관리자를 사용하여 원본 파일에 액세스할 경우 대량 삽입 태스크에서는 플랫 파일 연결 관리자에서 지정한 서식을 사용하지 않습니다. 대신 대량 삽입 태스크에서는 서식 파일에 지정된 서식이나 태스크의 RowDelimiter 및 ColumnDelimiter 속성 값을 사용합니다.  
  
 **관련 항목:** [파일 연결 관리자](connection-manager/file-connection-manager.md), [파일 연결 관리자 편집기](../../2014/integration-services/file-connection-manager-editor.md), [플랫 파일 연결 관리자](connection-manager/flat-file-connection-manager.md), [플랫 파일 연결 관리자 편집기&#40;일반 페이지&#41;](general-page-of-integration-services-designers-options.md), [플랫 파일 연결 관리자 편집기&#40;열 페이지&#41;](../../2014/integration-services/flat-file-connection-manager-editor-columns-page.md), [플랫 파일 연결 관리자 편집기&#40;고급 페이지&#41;](../../2014/integration-services/flat-file-connection-manager-editor-advanced-page.md)  
  
 **테이블 새로 고침**  
 테이블 및 뷰 목록을 새로 고칩니다.  
  
## <a name="format-dynamic-options"></a>Format 동적 옵션  
  
### <a name="format--use-file"></a>Format = 파일 사용  
 **FormatFile**  
 서식 파일의 경로를 입력하거나 줄임표 단추 **(...)** 를 클릭하여 서식 파일을 찾습니다.  
  
### <a name="format--specify"></a>Format = 지정  
 `RowDelimiter`  
 원본 파일의 행 구분 기호를 지정합니다. 기본값은 **{CR}{LF}** 입니다.  
  
 `ColumnDelimiter`  
 원본 파일의 열 구분 기호를 지정합니다. 기본값은 **탭**입니다.  
  
## <a name="see-also"></a>관련 항목  
 [Integration Services 오류 및 메시지 참조](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [대량 삽입 태스크 편집기 &#40;일반 페이지&#41;](../../2014/integration-services/bulk-insert-task-editor-general-page.md)   
 [대량 삽입 태스크 편집기 &#40;옵션 페이지&#41;](../../2014/integration-services/bulk-insert-task-editor-options-page.md)   
 [식 페이지](expressions/expressions-page.md)   
 [BULK INSERT&#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)   
 [제어 흐름](control-flow/control-flow.md)  
  
  
