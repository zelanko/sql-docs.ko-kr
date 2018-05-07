---
title: FILESTREAM 지원 | Microsoft Docs
description: SQL Server 용 OLE DB 드라이버에서 FILESTREAM 지원
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|features
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- FILESTREAM [SQL Server], OLE DB Driver for SQL Server
- OLE DB Driver for SQL Server [FILESTREAM support]
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: d9774e55a9366f99ad96fb5c2165abb3992f6e03
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="filestream-support"></a>FILESTREAM 지원
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

부터는 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)], OLE DB Driver for SQL Server의 향상 된 FILESTREAM 기능을 지원 합니다. 샘플을 보려면 [Filestream 및 OLE DB](../../oledb/ole-db-how-to/filestream/filestream-and-ole-db.md)합니다.  

FILESTREAM은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 또는 Windows 파일 시스템에 대한 직접 액세스를 통해 큰 이진 값을 저장하고 액세스하는 방법을 제공합니다. 큰 이진 값은 2GB보다 큰 값입니다. 향상 된 FILESTREAM 지원에 대 한 자세한 내용은 참조 [FILESTREAM &#40;SQL Server&#41;](../../../relational-databases/blob/filestream-sql-server.md)합니다.  
  
데이터베이스 연결이 열릴 때 **@@TEXTSIZE**  로 설정 됩니다-1 (""), 기본적으로 제한이 없습니다.  
  
Windows 파일 시스템 API를 사용하여 FILESTREAM 열에 액세스하고 업데이트할 수도 있습니다.  
  
자세한 내용은 참조 [opensqlfilestream FILESTREAM 데이터 액세스](../../../relational-databases/blob/access-filestream-data-with-opensqlfilestream.md)  
  
## <a name="querying-for-filestream-columns"></a>FILESTREAM 열 쿼리  
OLE DB의 스키마 행 집합은 열이 FILESTREAM 열인지 여부를 보고하지 않습니다. FILESTREAM 열을 만들 ITableDefinition OLE DB에서 사용할 수 없습니다.    
  
사용할 수 있습니다 FILESTREAM 열을 만들 하거나 FILESTREAM 열이 되는 기존 열을 검색 하는 **is_filestream** 의 열은 [sys.columns](../../../relational-databases/system-catalog-views/sys-columns-transact-sql.md) 카탈로그 뷰.  
  
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
SQL Server 용 OLE DB 드라이버를 사용 하 여 클라이언트가 컴파일 되었으며 응용 프로그램에 연결 하는 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 통해 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]), 다음 **varbinary (max)** 동작이 동작과 호환 됩니다. 에 의해 도입 된 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client에 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]합니다. 즉, 반환되는 데이터의 최대 크기가 2GB로 제한됩니다. 큰 결과 값에 대 한 해당 2GB 잘림이 발생 하 고 "문자열 데이터 오른쪽 잘림" 경고가 반환 됩니다. 
  
데이터 형식 호환성을 80으로 설정하면 클라이언트 동작이 하위 수준 클라이언트 동작과 일치합니다.  
  
SQLOLEDB 또는 보다 먼저 발표 된 다른 공급자를 사용 하는 클라이언트는 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], **varbinary (max)** 매핑됩니다 이미지에 있습니다.  
  
## <a name="comments"></a>설명
- 보내고 받을 **varbinary (max)** 2GB 보다 큰 값을 응용 프로그램에서 사용 **DBTYPE_IUNKNOWN** 매개 변수와 결과 바인딩에 있습니다. 매개 변수에 대 한 공급자 및 ISequentialStream을 반환 하는 결과에 ISequentialStream 대 iunknown:: Queryinterface를 호출 해야 합니다.  

-  OLE DB에 대 한 검사 ISequentialStream 값에 관련 완화 될 것입니다. 때 *wType* 은 **DBTYPE_IUNKNOWN** 에 **DBBINDING** 구조체 수 길이 검사 생략 하거나 사용 하지 않도록 설정 **DBPART_LENGTH** *dwPart* 또는 데이터의 길이 설정 하 여 (오프셋 *obLength* 데이터 버퍼에)를 ~ 0입니다. 이렇게 하면 공급자는 값의 길이를 검사하지 않고 스트림을 통해 사용할 수 있는 모든 데이터를 요청하고 반환합니다. 이러한 변경 사항은 모든 LOB(큰 개체) 형식과 XML에 적용되지만, 이는 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 이상의 서버에 연결된 경우에만 해당됩니다. 이 기능은 개발자에게 더 나은 융통성을 제공할 뿐만 아니라 기존 응용 프로그램 및 하위 서버를 위한 일관성과 이전 버전과의 호환성을 유지할 수 있게 도와줍니다.  이 변경 사항은 irowset:: Getdata, icommand:: Execute, 및 irowsetfastload:: Insertrow 주로 데이터를 전송 하는 모든 인터페이스에 적용 합니다.
 

## <a name="see-also"></a>관련 항목:  
 [SQL Server 기능용 OLE DB 드라이버](../../oledb/features/oledb-driver-for-sql-server-features.md)  
  
  
