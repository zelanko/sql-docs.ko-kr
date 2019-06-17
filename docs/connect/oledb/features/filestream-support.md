---
title: FILESTREAM 지원 | Microsoft Docs
description: SQL Server용 OLE DB 드라이버에서 FILESTREAM 지원
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- FILESTREAM [SQL Server], OLE DB Driver for SQL Server
- OLE DB Driver for SQL Server [FILESTREAM support]
author: pmasl
ms.author: pelopes
manager: jroth
ms.openlocfilehash: ebaaf0da2a051106b690f80d4524e675358450c4
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66777786"
---
# <a name="filestream-support"></a>FILESTREAM 지원
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

부터는 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)], OLE DB Driver for SQL Server에서는 향상 된 FILESTREAM 기능을 지원 합니다. 샘플을 보려면 [Filestream 및 OLE DB](../../oledb/ole-db-how-to/filestream/filestream-and-ole-db.md)합니다.  

FILESTREAM은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 또는 Windows 파일 시스템에 대한 직접 액세스를 통해 큰 이진 값을 저장하고 액세스하는 방법을 제공합니다. 큰 이진 값은 2GB보다 큰 값입니다. 향상 된 FILESTREAM 지원에 대 한 자세한 내용은 참조 하세요. [FILESTREAM &#40;SQL Server&#41;](../../../relational-databases/blob/filestream-sql-server.md)합니다.  
  
데이터베이스 연결을 열면 **@@TEXTSIZE** 가 기본적으로 -1("제한 없음")로 설정됩니다.  
  
Windows 파일 시스템 API를 사용하여 FILESTREAM 열에 액세스하고 업데이트할 수도 있습니다.  
  
자세한 내용은 [OpenSqlFilestream을 사용하여 FILESTREAM 데이터 액세스](../../../relational-databases/blob/access-filestream-data-with-opensqlfilestream.md) 참조  
  
## <a name="querying-for-filestream-columns"></a>FILESTREAM 열 쿼리  
OLE DB의 스키마 행 집합은 열이 FILESTREAM 열인지 여부를 보고하지 않습니다. OLE DB의 ITableDefinition을 사용하여 FILESTREAM 열을 만들 수 없습니다.    
  
FILESTREAM 열을 만들거나 FILESTREAM 열인 기존 열을 검색하려면 [sys.columns](../../../relational-databases/system-catalog-views/sys-columns-transact-sql.md) 카탈로그 뷰의 **is_filestream** 열을 사용할 수 있습니다.  
  
다음은 이에 대한 예입니다.  
  
```sql  
-- Create a table with a FILESTREAM column.  
CREATE TABLE Bob_01 (GuidCol1 uniqueidentifier ROWGUIDCOL NOT NULL UNIQUE DEFAULT NEWID(), IntCol2 int, varbinaryCol3 varbinary(max) FILESTREAM);  
  
-- Find FILESTREAM columns.  
SELECT name FROM sys.columns WHERE is_filestream=1;  
  
-- Determine whether a column is a FILESTREAM column.  
SELECT is_filestream FROM sys.columns WHERE name = 'varbinaryCol3' AND object_id IN (SELECT object_id FROM sys.tables WHERE name='Bob_01');  
```  
  
## <a name="down-level-compatibility"></a>하위 수준과의 호환성  
SQL Server 용 OLE DB 드라이버를 사용 하 여 클라이언트가 컴파일 되었으며 응용 프로그램에 연결할 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ( [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 를 통해 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]), 한 다음 **varbinary (max)** 동작 동작과 호환 됩니다. 도입 된 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client에 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]입니다. 즉, 반환되는 데이터의 최대 크기가 2GB로 제한됩니다. 결과 값이 2GB보다 큰 경우 잘림이 발생하고 "문자열 데이터 오른쪽 잘림" 경고가 반환됩니다. 
  
데이터 형식 호환성을 80으로 설정하면 클라이언트 동작이 하위 수준 클라이언트 동작과 일치합니다.  
  
SQLOLEDB 또는 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]보다 먼저 출시된 기타 공급자를 사용하는 클라이언트의 경우 **varbinary(max)** 가 이미지에 매핑됩니다.  
  
## <a name="comments"></a>주석
- 보내고 받을 **varbinary (max)** 2GB 보다 큰 값을 응용 프로그램에서 사용 **DBTYPE_IUNKNOWN** 매개 변수와 결과 바인딩에 있습니다. 매개 변수에 대 한 공급자 ISequentialStream 및 ISequentialStream을 반환 하는 결과 iunknown:: Queryinterface를 호출 해야 합니다.  

-  OLE DB에 대 한 관련 ISequentialStream 값 검사에 완화 될 예정입니다. 때 *wType* 됩니다 **DBTYPE_IUNKNOWN** 에 **DBBINDING** 구조체 길이 검사 수 생략 하거나 사용 하지 않도록 설정 **DBPART_LENGTH** *dwPart* 하거나 데이터의 길이 설정 하 여 (오프셋 *obLength* 데이터 버퍼에서)를 ~ 0입니다. 이렇게 하면 공급자는 값의 길이를 검사하지 않고 스트림을 통해 사용할 수 있는 모든 데이터를 요청하고 반환합니다. 이러한 변경 사항은 모든 LOB(큰 개체) 형식과 XML에 적용되지만, 이는 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 이상의 서버에 연결된 경우에만 해당됩니다. 이 기능은 개발자에게 더 나은 융통성을 제공할 뿐만 아니라 기존 응용 프로그램 및 하위 서버를 위한 일관성과 이전 버전과의 호환성을 유지할 수 있게 도와줍니다.  이 변경 irowset:: Getdata, icommand:: Execute, 및 irowsetfastload:: Insertrow 주로 데이터를 전송 하는 모든 인터페이스에 적용 합니다.
 

## <a name="see-also"></a>참고 항목  
 [SQL Server 기능용 OLE DB 드라이버](../../oledb/features/oledb-driver-for-sql-server-features.md)  
  
  
