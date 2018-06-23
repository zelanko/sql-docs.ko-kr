---
title: FILESTREAM 지원 | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- FILESTREAM [SQL Server], SQL Server Native Client
- SQL Server Native Client [FILESTREAM support]
ms.assetid: 1ad3400d-7fcd-40c9-87ae-f5afc61e0374
caps.latest.revision: 22
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 407bf9e6816a08af989b18cfeed3a52ee7fa8465
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36186966"
---
# <a name="filestream-support"></a>FILESTREAM 지원
  FILESTREAM은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 또는 Windows 파일 시스템에 대한 직접 액세스를 통해 큰 이진 값을 저장하고 액세스하는 방법을 제공합니다. 큰 이진 값은 2GB보다 큰 값입니다. 향상 된 FILESTREAM 지원에 대 한 자세한 내용은 참조 [FILESTREAM &#40;SQL Server&#41;](../../blob/filestream-sql-server.md)합니다.  
  
 데이터베이스 연결을 열면 `@@TEXTSIZE`가 기본적으로 -1("제한 없음")로 설정됩니다.  
  
 Windows 파일 시스템 API를 사용하여 FILESTREAM 열에 액세스하고 업데이트할 수도 있습니다.  
  
 자세한 내용은 다음 항목을 참조하십시오.  
  
-   [FILESTREAM 지원 &#40;OLE DB&#41;](../ole-db/filestream-support-ole-db.md)  
  
-   [FILESTREAM 지원 &#40;ODBC&#41;](../odbc/filestream-support-odbc.md)  
  
-   [OpenSqlFilestream을 사용하여 FILESTREAM 데이터 액세스](../../blob/access-filestream-data-with-opensqlfilestream.md)  
  
## <a name="querying-for-filestream-columns"></a>FILESTREAM 열 쿼리  
 OLE DB의 스키마 행 집합은 열이 FILESTREAM 열인지 여부를 보고하지 않습니다. FILESTREAM 열을 만들 ITableDefinition OLE DB에서 사용할 수 없습니다.  
  
 Odbc에서 SQLColumns 같은 카탈로그 함수는 열이 FILESTREAM 열인지 여부를 보고 하지 않습니다.  
  
 사용할 수 있습니다 FILESTREAM 열을 만들 하거나 FILESTREAM 열이 되는 기존 열을 검색 하는 `is_filestream` 의 열은 [sys.columns](/sql/relational-databases/system-catalog-views/sys-columns-transact-sql) 카탈로그 뷰.  
  
 다음은 이에 대한 예입니다.  
  
```  
-- Create a table with a FILESTREAM column.  
CREATE TABLE Bob_01 (GuidCol1 uniqueidentifier ROWGUIDCOL NOT NULL UNIQUE DEFAULT NEWID(), IntCol2 int, varbinaryCol3 varbinary(max) FILESTREAM);  
  
-- Find FILESTREAM columns.  
SELECT name FROM sys.columns WHERE is_filestream=1;  
  
-- Determine whether a column is a FILESTREAM column.  
SELECT is_filestream FROM sys.columns WHERE name = 'varbinaryCol3' AND object_id IN (SELECT object_id FROM sys.tables WHERE name='Bob_01');  
```  
  
## <a name="down-level-compatibility"></a>하위 수준과의 호환성  
 버전을 사용 하 여 클라이언트가 컴파일 되었으며 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client와 함께 포함 된 [!INCLUDE[ssVersion2005](../../../includes/sscurrent-md.md)], `varbinary(max)` 동작이 호환 될 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]합니다. 즉, 반환되는 데이터의 최대 크기가 2GB로 제한됩니다. 큰 결과 값에 대 한 해당 2GB 잘림이 발생 하 고 "문자열 데이터 오른쪽 잘림" 경고가 반환 됩니다.  
  
 데이터 형식 호환성을 80으로 설정하면 클라이언트 동작이 하위 수준 클라이언트 동작과 일치합니다.  
  
 SQLOLEDB 또는 보다 먼저 발표 된 다른 공급자를 사용 하는 클라이언트는 [!INCLUDE[ssVersion2005](../../../includes/ssnoversion-md.md)] Native Client `varbinary(max)` 매핑됩니다 이미지에 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server Native Client 기능](sql-server-native-client-features.md)  
  
  
