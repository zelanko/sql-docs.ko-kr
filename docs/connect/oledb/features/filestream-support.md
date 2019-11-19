---
title: FILESTREAM 지원 | Microsoft Docs
description: SQL Server용 OLE DB 드라이버에서 FILESTREAM 지원
ms.custom: ''
ms.date: 09/13/2019
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
ms.openlocfilehash: da67f050eba24ecf040124533c9d98c3f3f6bfec
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 11/13/2019
ms.locfileid: "74056728"
---
# <a name="filestream-support"></a>FILESTREAM 지원
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

[!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]부터 SQL Server 용 OLE DB Driver는 향상 된 FILESTREAM 기능을 지원 합니다. 샘플은 [Filestream 및 OLE DB](../../oledb/ole-db-how-to/filestream/filestream-and-ole-db.md)을 참조 하세요.  

FILESTREAM은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 또는 Windows 파일 시스템에 대한 직접 액세스를 통해 큰 이진 값을 저장하고 액세스하는 방법을 제공합니다. 큰 이진 값은 2GB보다 큰 값입니다. 향상 된 FILESTREAM 지원에 대 한 자세한 내용은 [filestream &#40;SQL Server&#41;](../../../relational-databases/blob/filestream-sql-server.md)를 참조 하세요.  
  
데이터베이스 연결을 열면 **\@\@TEXTSIZE**가 기본적으로 -1("제한 없음")로 설정됩니다.  
  
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
클라이언트가 SQL Server에 대 한 OLE DB 드라이버를 사용 하 여 컴파일 되었으며 응용 프로그램이 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ([!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]를 통해 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)])에 연결 되는 경우 **varbinary (max)** 동작은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native client에서 도입 된 동작과 호환 됩니다[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]. 즉, 반환되는 데이터의 최대 크기가 2GB로 제한됩니다. 결과 값이 2GB보다 큰 경우 잘림이 발생하고 "문자열 데이터 오른쪽 잘림" 경고가 반환됩니다. 
  
데이터 형식 호환성을 80으로 설정하면 클라이언트 동작이 하위 수준 클라이언트 동작과 일치합니다.  
  
SQLOLEDB 또는 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]보다 먼저 출시된 기타 공급자를 사용하는 클라이언트의 경우 **varbinary(max)** 가 이미지에 매핑됩니다.  
  
## <a name="comments"></a>주석
- **Varbinary (max)** 값을 2gb 보다 크게 보내고 받으려면 응용 프로그램은 매개 변수 및 결과 바인딩에서 **DBTYPE_IUNKNOWN** 를 사용 합니다. 매개 변수의 경우 공급자는 ISequentialStream에 대해 IUnknown:: QueryInterface를 호출 하 고 ISequentialStream를 반환 하는 결과에 대해를 호출 해야 합니다.  

-  OLE DB의 경우 ISequentialStream 값과 관련 된 검사가 완화 됩니다. *Wtype* 이 **DBBINDING** 구조체에서 **DBTYPE_IUNKNOWN** 경우 *dwpart* 에서 **DBPART_LENGTH** 생략 하거나 데이터의 길이 (데이터 버퍼의 오프셋 *oblength* )를 ~ 0으로 설정 하 여 길이 검사를 사용 하지 않도록 설정할 수 있습니다. 이렇게 하면 공급자는 값의 길이를 검사하지 않고 스트림을 통해 사용할 수 있는 모든 데이터를 요청하고 반환합니다. 이러한 변경 사항은 모든 LOB(큰 개체) 형식과 XML에 적용되지만, 이는 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 이상의 서버에 연결된 경우에만 해당됩니다. 이 기능은 개발자에게 더 나은 융통성을 제공할 뿐만 아니라 기존 애플리케이션 및 하위 서버를 위한 일관성과 이전 버전과의 호환성을 유지할 수 있게 도와줍니다.  이 변경 내용은 데이터를 전송 하는 모든 인터페이스 (주로 IRowset:: GetData, ICommand:: Execute 및 IRowsetFastLoad:: InsertRow)에 영향을 줍니다.
 

## <a name="see-also"></a>참고 항목  
 [SQL Server 기능용 OLE DB 드라이버](../../oledb/features/oledb-driver-for-sql-server-features.md)  
  
  
