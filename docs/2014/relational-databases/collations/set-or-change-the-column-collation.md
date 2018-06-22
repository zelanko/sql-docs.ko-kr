---
title: 열 데이터 정렬 설정 또는 변경 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- tempdb database [SQL Server], collations
- collations [SQL Server], column
ms.assetid: d7a9638b-717c-4680-9b98-8849081e08be
caps.latest.revision: 29
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 3de84f26e894f00760a45d5e65769c0db8d4b009
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36079529"
---
# <a name="set-or-change-the-column-collation"></a>열 데이터 정렬 설정 또는 변경
  에 대 한 데이터베이스 데이터 정렬을 재정의할 수 `char`, `varchar`, `text`, `nchar`, `nvarchar`, 및 `ntext` 특정 테이블의 열에 대 한 다른 데이터 정렬을 지정 하 고 다음 중 하나를 사용 하 여 데이터:  
  
-   [CREATE TABLE](/sql/t-sql/statements/create-table-transact-sql) 및 [ALTER TABLE](/sql/t-sql/statements/alter-table-transact-sql)의 COLLATE 절 예를 들어:  
  
    ```  
    CREATE TABLE dbo.MyTable  
      (PrimaryKey   int PRIMARY KEY,  
       CharCol      varchar(10) COLLATE French_CI_AS NOT NULL  
      );  
    GO  
    ALTER TABLE dbo.MyTable ALTER COLUMN CharCol  
                varchar(10)COLLATE Latin1_General_CI_AS NOT NULL;  
    GO  
    ```  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]의 COLLATE 절 자세한 내용은 [Collation and Unicode Support](collation-and-unicode-support.md)을 참조하십시오.  
  
-   사용 하는 `Column.Collation` 속성 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Objects (SMO).  
  
 다음 중 하나가 현재 참조하고 있는 열의 데이터 정렬은 변경할 수 없습니다.  
  
-   계산 열  
  
-   인덱스  
  
-   자동으로 또는 CREATE STATISTICS 문에 의해 생성된 배포 통계  
  
-   CHECK 제약 조건  
  
-   FOREIGN KEY 제약 조건  
  
 **tempdb**를 사용할 때 [COLLATE](/sql/t-sql/statements/collations) 절은 *database_default* 옵션을 포함하여 임시 테이블에 있는 열이 **tempdb**의 데이터 정렬 대신 현재 사용자 데이터베이스의 데이터 정렬 기본값을 연결에 사용하도록 지정합니다.  
  
## <a name="collations-and-text-columns"></a>데이터 정렬 및 텍스트 열  
 삽입 하거나 열의 값을 업데이트할 수 있습니다는 `text` 는 데이터 정렬이 데이터베이스 기본 데이터 정렬의 코드 페이지와에서 다른 열입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 값을 열의 데이터 정렬로 암시적으로 변환합니다.  
  
## <a name="collations-and-tempdb"></a>데이터 정렬 및 tempdb  
 **tempdb** 데이터베이스는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 시작될 때마다 작성되며 **model** 데이터베이스와 같은 기본 데이터 정렬을 사용합니다. 이는 일반적으로 인스턴스의 기본 데이터 정렬과 같습니다. 사용자 데이터베이스를 만들고 **model**과 다른 기본 데이터 정렬을 지정하면 사용자 데이터베이스는 **tempdb**와 다른 기본 데이터 정렬을 사용합니다. 모든 임시 저장 프로시저나 임시 테이블은 **tempdb**에서 생성되고 저장됩니다. 즉, 임시 테이블의 모든 암시적 열과 임시 저장 프로시저의 모든 강제 기본 상수, 변수 및 매개 변수는 영구 테이블 및 저장 프로시저에서 만들어진 유사 개체와는 다른 데이터 정렬을 사용합니다.  
  
 이로 인해 사용자 정의 데이터베이스와 시스템 데이터베이스 개체 간에 데이터 정렬 불일치 문제가 발생할 수 있습니다. 예를 들어 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서는 Latin1_General_CS_AS 데이터 정렬을 사용하는데 다음 문을 실행합니다.  
  
```  
CREATE DATABASE TestDB COLLATE Estonian_CS_AS;  
USE TestDB;  
CREATE TABLE TestPermTab (PrimaryKey int PRIMARY KEY, Col1 nchar );  
```  
  
 이 시스템에서 **tempdb** 데이터베이스는 코드 페이지 1252를 포함하는 Latin1_General_CS_AS 데이터 정렬을 사용하고 `TestDB` 및 `TestPermTab.Col1` 은 코드 페이지 1257을 포함하는 `Estonian_CS_AS` 데이터 정렬을 사용합니다. 예를 들어:  
  
```  
USE TestDB;  
GO  
-- Create a temporary table with the same column declarations  
-- as TestPermTab  
CREATE TABLE #TestTempTab (PrimaryKey int PRIMARY KEY, Col1 nchar );  
INSERT INTO #TestTempTab  
         SELECT * FROM TestPermTab;  
GO  
```  
  
 이전 예에서 **tempdb** 데이터베이스는 Latin1_General_CS_AS 데이터 정렬을 사용하고 `TestDB` 및 `TestTab.Col1` 은 `Estonian_CS_AS` 데이터 정렬을 사용합니다. 예를 들어:  
  
```  
SELECT * FROM TestPermTab AS a INNER JOIN #TestTempTab on a.Col1 = #TestTempTab.Col1;  
```  
  
 **tempdb** 는 기본 서버 데이터 정렬을 사용하고 `TestPermTab.Col1` 은 다른 데이터 정렬을 사용하므로 SQL Server는 "같음 작업에서 'Latin1_General_CI_AS_KS_WS'과(와) 'Estonian_CS_AS' 간의 데이터 정렬 충돌을 해결할 수 없습니다"라는 오류를 반환합니다.  
  
 이 오류를 방지하는 데 사용할 수 있는 방법은 다음과 같습니다.  
  
-   임시 테이블 열이 **tempdb**가 아닌 사용자 데이터베이스의 기본 데이터 정렬을 사용하도록 지정합니다. 이렇게 하면 시스템에서 요구할 경우 임시 테이블은 여러 데이터베이스에 있는 유사한 형식의 테이블로 작업할 수 있습니다.  
  
    ```  
    CREATE TABLE #TestTempTab  
       (PrimaryKey int PRIMARY KEY,  
        Col1 nchar COLLATE database_default  
       );  
    ```  
  
-   `#TestTempTab` 열에 대해 올바른 데이터 정렬을 지정합니다.  
  
    ```  
    CREATE TABLE #TestTempTab  
       (PrimaryKey int PRIMARY KEY,  
        Col1 nchar COLLATE Estonian_CS_AS  
       );  
    ```  
  
## <a name="see-also"></a>관련 항목  
 [서버 데이터 정렬 설정 또는 변경](set-or-change-the-server-collation.md)   
 [데이터베이스 데이터 정렬 설정 또는 변경](set-or-change-the-database-collation.md)   
 [Collation and Unicode Support](collation-and-unicode-support.md)  
  
  
