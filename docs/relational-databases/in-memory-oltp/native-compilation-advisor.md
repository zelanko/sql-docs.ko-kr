---
title: 네이티브 컴파일 관리자 | Microsoft 문서
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
f1_keywords:
- sql13.swb.nativecompilationwizard.f1
- swb.nativecompilationwizard.f1
ms.assetid: d3898a47-2985-4a08-bc70-fd8331a01b7b
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 30d6949d43e0ca3b652953c96625df031d8ddec2
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47787807"
---
# <a name="native-compilation-advisor"></a>네이티브 컴파일 관리자
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  트랜잭션 성능 분석 보고서는 네이티브 컴파일을 사용하도록 변환할 경우 효과적인 해석된 저장 프로시저에 대한 정보를 제공합니다. 자세한 내용은 [메모리 내 OLTP에 테이블 또는 저장 프로시저를 이식해야 하는지 확인](../../relational-databases/in-memory-oltp/determining-if-a-table-or-stored-procedure-should-be-ported-to-in-memory-oltp.md)을 참조하세요.  
  
 네이티브 컴파일을 사용하도록 변환할 저장 프로시저를 식별한 후 네이티브 컴파일 관리자(NCA)를 사용하여 해석된 저장 프로시저를 네이티브 컴파일로 마이그레이션할 수 있습니다. 고유하게 컴파일된 저장 프로시저에 대한 자세한 내용은 [Natively Compiled Stored Procedures](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md)를 참조하세요.  
  
 지정된 해석 저장 프로시저에서 NCA를 통해 네이티브 모듈에서 지원되지 않는 모든 기능을 식별할 수 있습니다. NCA는 해결 방법 또는 솔루션에 대한 설명서 링크를 제공합니다.  
  
 마이그레이션 방법에 대한 자세한 내용은 [메모리 내 OLTP – 일반적인 작업 패턴 및 마이그레이션 고려 사항](http://msdn.microsoft.com/library/dn673538.aspx)을 참조하세요.  
  
## <a name="walkthrough-using-the-native-compilation-advisor"></a>네이티브 컴파일 관리자 사용 연습  
 **개체 탐색기**에서 변환할 저장 프로시저를 마우스 오른쪽 단추로 클릭하고 **네이티브 컴파일 관리자**를 선택합니다. **저장 프로시저 네이티브 컴파일 관리자**시작 페이지가 표시됩니다. 계속하려면 **다음** 을 클릭합니다.  
  
### <a name="stored-procedure-validation"></a>저장 프로시저 유효성 검사  
 이 페이지에는 저장 프로시저에 네이티브 컴파일과 호환되지 않는 구문이 사용되었는지 여부가 표시됩니다. **다음** 을 클릭하여 세부 정보를 볼 수 있습니다. 네이티브 컴파일과 호환되지 않는 구문이 있는 경우 **다음** 을 클릭하여 세부 정보를 볼 수 있습니다.  
  
### <a name="stored-procedure-validation-result"></a>저장 프로시저 유효성 검사 결과  
 네이티브 컴파일과 호환되지 않는 구문이 있는 경우 **저장 프로시저 유효성 검사 결과** 페이지에 세부 정보가 표시됩니다. 보고서를 생성하고( **보고서 생성**클릭), **네이티브 컴파일 관리자**를 종료하고, 코드가 네이티브 컴파일과 호환되도록 업데이트할 수 있습니다.  
  
## <a name="code-sample"></a>코드 예제  
 다음 예에서는 해석된 저장 프로시저와 네이티브 컴파일을 사용했을 때의 *해당* 저장 프로시저를 보여 줍니다. 이 예에서는 c:\data라는 디렉터리를 사용합니다.  
  
> [!NOTE]  
>  일반적으로 **FILEGROUP** 요소 및 **USE** mydatabase 문은 Microsoft SQL Server에 적용되지만 Azure SQL 데이터베이스에는 적용되지 않습니다.  
  
```sql  
CREATE DATABASE Demo  
ON  
PRIMARY(NAME = [Demo_data],  
FILENAME = 'C:\DATA\Demo_data.mdf', size=500MB)  
, FILEGROUP [Demo_fg] CONTAINS MEMORY_OPTIMIZED_DATA(  
NAME = [Demo_dir],  
FILENAME = 'C:\DATA\Demo_dir')  
LOG ON (name = [Demo_log], Filename='C:\DATA\Demo_log.ldf', size=500MB)  
COLLATE Latin1_General_100_BIN2;  
go  
  
USE Demo;  
go  
  
CREATE TABLE [dbo].[SalesOrders]  
(  
     [order_id] [int] NOT NULL,  
     [order_date] [datetime] NOT NULL,  
     [order_status] [tinyint] NOT NULL  
     CONSTRAINT [PK_SalesOrders] PRIMARY KEY NONCLUSTERED HASH   
(  
     [order_id]  
) WITH ( BUCKET_COUNT = 2097152)  
) WITH ( MEMORY_OPTIMIZED = ON )  
go  
  
-- Interpreted.  
CREATE PROCEDURE [dbo].[InsertOrder] @id INT, @date DATETIME2, @status TINYINT  
AS   
BEGIN   
  INSERT dbo.SalesOrders VALUES (@id, @date, @status);  
END  
go  
  
-- Natively Compiled.  
CREATE PROCEDURE [dbo].[InsertOrderXTP]  
      @id INT, @date DATETIME2, @status TINYINT  
  WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
AS   
BEGIN ATOMIC WITH   
     (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english'  
     )  
  INSERT dbo.SalesOrders VALUES (@id, @date, @status);  
END  
go  
  
SELECT * from SalesOrders;  
go  
  
EXECUTE dbo.InsertOrder @id= 10, @date = '1956-01-01 12:00:00', @status = 1;  
EXECUTE dbo.InsertOrderXTP @id= 11, @date = '1956-01-01 12:01:00', @status = 2;  
  
SELECT * from SalesOrders;  
```  
  
## <a name="see-also"></a>참고 항목  
 [메모리 내 OLTP로 마이그레이션](../../relational-databases/in-memory-oltp/migrating-to-in-memory-oltp.md)   
 [메모리 액세스에 최적화된 테이블 사용을 위한 요구 사항](../../relational-databases/in-memory-oltp/requirements-for-using-memory-optimized-tables.md)  
  
  
