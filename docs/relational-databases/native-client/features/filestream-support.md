---
title: FILESTREAM 지원 | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- FILESTREAM [SQL Server], SQL Server Native Client
- SQL Server Native Client [FILESTREAM support]
ms.assetid: 1ad3400d-7fcd-40c9-87ae-f5afc61e0374
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1c0c4b28542b6389608eb9272e21bc45ae178d88
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37408603"
---
# <a name="filestream-support"></a>FILESTREAM 지원
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  FILESTREAM은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 또는 Windows 파일 시스템에 대한 직접 액세스를 통해 큰 이진 값을 저장하고 액세스하는 방법을 제공합니다. 큰 이진 값은 2GB보다 큰 값입니다. 향상 된 FILESTREAM 지원에 대 한 자세한 내용은 참조 하세요. [FILESTREAM &#40;SQL Server&#41;](../../../relational-databases/blob/filestream-sql-server.md)합니다.  
  
 데이터베이스 연결을 열면 **@@TEXTSIZE**  에 설정할-1 ("제한 없음"), 기본적으로 합니다.  
  
 Windows 파일 시스템 API를 사용하여 FILESTREAM 열에 액세스하고 업데이트할 수도 있습니다.  
  
 자세한 내용은 다음 항목을 참조하십시오.  
  
-   [FILESTREAM 지원 &#40;OLE DB&#41;](../../../relational-databases/native-client/ole-db/filestream-support-ole-db.md)  
  
-   [FILESTREAM 지원 &#40;ODBC&#41;](../../../relational-databases/native-client/odbc/filestream-support-odbc.md)  
  
-   [OpenSqlFilestream을 사용하여 FILESTREAM 데이터 액세스](../../../relational-databases/blob/access-filestream-data-with-opensqlfilestream.md)  
  
## <a name="querying-for-filestream-columns"></a>FILESTREAM 열 쿼리  
 OLE DB의 스키마 행 집합은 열이 FILESTREAM 열인지 여부를 보고하지 않습니다. FILESTREAM 열을 만들려면 ITableDefinition OLE DB에서 사용할 수 없습니다.  
  
 Odbc에서 SQLColumns 같은 카탈로그 함수는 열이 FILESTREAM 열인지 여부를 보고 하지 않습니다.  
  
 FILESTREAM 열을 만드는 또는 FILESTREAM 열이 되는 기존 열을 검색 하려면 사용할 수 있습니다 합니다 **is_filestream** 열을 [sys.columns](../../../relational-databases/system-catalog-views/sys-columns-transact-sql.md) 카탈로그 뷰.  
  
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
 클라이언트의 버전을 사용 하 여 컴파일된 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 포함 된 네이티브 클라이언트 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], 응용 프로그램에 연결 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]합니다 **varbinary (max)** 동작 와호환됩니다[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]. 즉, 반환되는 데이터의 최대 크기가 2GB로 제한됩니다. 큰 결과 값에 대 한 2GB, 잘림이 발생 하 고 "문자열 데이터 오른쪽 잘림" 경고가 반환 됩니다.  
  
 데이터 형식 호환성을 80으로 설정하면 클라이언트 동작이 하위 수준 클라이언트 동작과 일치합니다.  
  
 SQLOLEDB 또는 이전에 출시 된 기타 공급자를 사용 하는 클라이언트에 대 한 합니다 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 버전의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client **varbinary (max)** 매핑될 이미지입니다.  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server Native Client 기능](../../../relational-databases/native-client/features/sql-server-native-client-features.md)  
  
  
