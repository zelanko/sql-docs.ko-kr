---
description: PathName(Transact-SQL)
title: PathName (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/02/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- PathName_TSQL
- PathName
dev_langs:
- TSQL
helpviewer_keywords:
- PathName FILESTREAM [SQL Server]
ms.assetid: 6b95ad90-6c82-4a23-9294-a2adb74934a3
author: rothja
ms.author: jroth
ms.openlocfilehash: fc5b4b67074c85aef7d5d6d0f7c889a02cbb047d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88489744"
---
# <a name="pathname-transact-sql"></a>PathName(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  FILESTREAM BLOB(Binary Large Object)의 경로를 반환합니다. OpenSqlFilestream API는이 경로를 사용 하 여 응용 프로그램이 Win32 Api를 사용 하 여 BLOB 데이터를 작업 하는 데 사용할 수 있는 핸들을 반환 합니다. PathName은 읽기 전용입니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
column_name.PathName ( @option [ , use_replica_computer_name ] )  
```  
  
## <a name="arguments"></a>인수  
 *column_name*  
 **Varbinary (max)** FILESTREAM 열의 열 이름입니다. *column_name* 은 열 이름 이어야 합니다. 식이나 CAST 또는 CONVERT 문의 결과일 수 없습니다.  
  
 FILESTREAM 저장소 특성이 없는 **varbinary (max)** 또는 다른 데이터 형식의 열에 대해 PathName을 요청 하면 쿼리 컴파일 시간 오류가 발생 합니다.  
  
 *\@option*  
 경로의 서버 구성 요소에 형식을 지정 하는 방법을 정의 하는 정수 [식](../../t-sql/language-elements/expressions-transact-sql.md) 입니다. * \@ 옵션* 은 다음 값 중 하나일 수 있습니다. 기본값은 0입니다.  
  
|값|설명|  
|-----------|-----------------|  
|0|BIOS 형식으로 변환 된 서버 이름을 반환 합니다. 예를 들면 다음과 같습니다. `\\SERVERNAME\MSSQLSERVER\v1\Archive\dbo\Records\Chart\A73F19F7-38EA-4AB0-BB89-E6C545DBD3F9`|  
|1|서버 이름을 변환 하지 않고 반환 합니다. 예를 들면 다음과 같습니다. `\\ServerName\MSSQLSERVER\v1\Archive\dbo\Records\Chart\A73F1`|  
|2|전체 서버 경로를 반환 합니다. 예를 들면 다음과 같습니다. `\\ServerName.MyDomain.com\MSSQLSERVER\v1\Archive\dbo\Records\Chart\A73F19F7-38EA-4AB0-BB89-E6C545DBD3F9`|  
  
 *use_replica_computer_name*  
 서버 이름이 Always On 가용성 그룹에서 반환 되는 방법을 정의 하는 비트 값입니다.  
  
 데이터베이스가 Always On 가용성 그룹에 속하지 않을 경우이 인수의 값은 무시 됩니다. 컴퓨터 이름은 항상 경로에 사용됩니다.  
  
 데이터베이스가 Always On 가용성 그룹에 속하는 경우 *use_replica_computer_name* 의 값은 **PathName** 함수의 출력에 다음과 같은 영향을 미칠 수 있습니다.  
  
|값|설명|  
|-----------|-----------------|  
|지정 안 됨|함수가 경로에 VNN(가상 네트워크 이름)을 반환합니다.|  
|0|함수가 경로에 VNN(가상 네트워크 이름)을 반환합니다.|  
|1|함수가 경로에 컴퓨터 이름을 반환합니다.|  
  
## <a name="return-type"></a>반환 형식  
 **nvarchar(max)**  
  
## <a name="return-value"></a>반환 값  
 반환되는 값은 BLOB의 정규화된 논리적 또는 NETBIOS 경로입니다. PathName은 IP 주소를 반환하지 않습니다. FILESTREAM BLOB가 만들어지지 않은 경우 NULL이 반환됩니다.  
  
## <a name="remarks"></a>설명  
 ROWGUID 열은 PathName을 호출하는 모든 쿼리에 표시되어야 합니다.  
  
 FILESTREAM BLOB는 [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용해서만 만들 수 있습니다.  
  
## <a name="examples"></a>예제  
  
### <a name="a-reading-the-path-for-a-filestream-blob"></a>A. FILESTREAM BLOB의 경로 읽기  
 다음 예에서는 `PathName` 변수에 `nvarchar(max)`을 할당합니다.  
  
```sql  
DECLARE @PathName nvarchar(max);  
SET @PathName = (  
    SELECT TOP 1 photo.PathName()  
    FROM dbo.Customer  
    WHERE LastName = 'CustomerName'  
    );  
```  
  
### <a name="b-displaying-the-paths-for-filestream-blobs-in-a-table"></a>B. 테이블에 FILESTREAM BLOB 경로 표시  
 다음 예에서는 3개의 FILESTREAM BLOB에 대한 경로를 만들고 표시합니다.  
  
```sql  
-- Create a FILESTREAM-enabled database.  
-- The c:\data directory must exist.  
CREATE DATABASE PathNameDB  
ON  
PRIMARY ( NAME = ArchX1,  
    FILENAME = 'c:\data\archdatP1.mdf'),  
FILEGROUP FileStreamGroup1 CONTAINS FILESTREAM( NAME = ArchX3,  
    FILENAME = 'c:\data\filestreamP1')  
LOG ON  ( NAME = ArchlogX1,  
    FILENAME = 'c:\data\archlogP1.ldf');  
GO  
  
USE PathNameDB;  
GO  
  
-- Create a table, add some records, and  
-- create the associated FILESTREAM  
-- BLOB files.  
  
CREATE TABLE TABLE1  
    (  
        ID int,  
        RowGuidColumn UNIQUEIDENTIFIER  
                      NOT NULL UNIQUE ROWGUIDCOL,  
        FILESTREAMColumn varbinary(MAX) FILESTREAM  
    );  
GO  
  
INSERT INTO TABLE1 VALUES  
 (1, NEWID(), 0x00)  
,(2, NEWID(), 0x00)  
,(3, NEWID(), 0x00);  
GO  
  
SELECT FILESTREAMColumn.PathName() AS 'PathName' FROM TABLE1;  
  
--Results  
--PathName  
------------------------------------------------------------------------------------------------------------  
--\\SERVER\MSSQLSERVER\v1\PathNameExampleDB\dbo\TABLE1\FILESTREAMColumn\DD67C792-916E-4A76-8C8A-4A85DC5DB908  
--\\SERVER\MSSQLSERVER\v1\PathNameExampleDB\dbo\TABLE1\FILESTREAMColumn\2907122B-2560-4CB9-86DC-FBE7ABA1843B  
--\\SERVER\MSSQLSERVER\v1\PathNameExampleDB\dbo\TABLE1\FILESTREAMColumn\922BE0E0-CAB9-4403-90BF-945BD258E4BC  
--  
--(3 row(s) affected)  
GO  
  
--Drop the database to clean up.  
USE master;  
GO  
DROP DATABASE PathNameDB;  
```  
  
## <a name="see-also"></a>참고 항목  
 [Binary Large Object &#40;Blob&#41; 데이터 &#40;SQL Server&#41;](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md)   
 [Transact-sql&#41;GET_FILESTREAM_TRANSACTION_CONTEXT &#40;](../../t-sql/functions/get-filestream-transaction-context-transact-sql.md)   
 [OpenSqlFilestream을 사용하여 FILESTREAM 데이터 액세스](../../relational-databases/blob/access-filestream-data-with-opensqlfilestream.md)  
  
  
