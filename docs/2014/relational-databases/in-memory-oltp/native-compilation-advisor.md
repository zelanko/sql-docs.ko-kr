---
title: 네이티브 컴파일 관리자 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
f1_keywords:
- sql12.swb.nativecompilationwizard.f1
- swb.nativecompilationwizard.f1
ms.assetid: d3898a47-2985-4a08-bc70-fd8331a01b7b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8b72f500a425b7a55cab285a881c3ff915b9fb82
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53358705"
---
# <a name="native-compilation-advisor"></a>네이티브 컴파일 관리자
  트랜잭션 성능 보고서 도구( [메모리 내 OLTP에 테이블 또는 저장 프로시저를 이식해야 하는지 확인](determining-if-a-table-or-stored-procedure-should-be-ported-to-in-memory-oltp.md)참조)는 네이티브 컴파일을 사용하도록 변환할 경우 효과적인 해석된 저장 프로시저에 대한 정보를 제공합니다. 네이티브 컴파일을 사용하도록 변환할 저장 프로시저를 식별한 후 네이티브 컴파일 관리자를 사용하여 해석된 저장 프로시저를 네이티브 컴파일로 마이그레이션할 수 있습니다. 고유하게 컴파일된 저장 프로시저에 대한 자세한 내용은 [Natively Compiled Stored Procedures](natively-compiled-stored-procedures.md)를 참조하세요.  
  
 먼저 해석된 저장 프로시저가 포함된 인스턴스에 연결합니다. [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]또는 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 인스턴스에 연결할 수 있습니다. 하지만 메모리 최적화 관리자를 사용하여 마이그레이션 작업을 수행하려는 경우에는 메모리 내 OLTP 기능을 사용할 수 있는 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 인스턴스에 연결해야 합니다. 메모리 내 OLTP 요구 사항에 대한 자세한 내용은 [Requirements for Using Memory-Optimized Tables](memory-optimized-tables.md)을 참조하십시오.  
  
 마이그레이션 방법에 대한 자세한 내용은 [메모리 내 OLTP – 일반적인 작업 패턴 및 마이그레이션 고려 사항](https://msdn.microsoft.com/library/dn673538.aspx)을 참조하세요.  
  
## <a name="walkthrough-using-the-native-compilation-advisor"></a>네이티브 컴파일 관리자 사용 연습  
 **개체 탐색기**에서 변환할 저장 프로시저를 마우스 오른쪽 단추로 클릭하고 **네이티브 컴파일 관리자**를 선택합니다. **저장 프로시저 네이티브 컴파일 관리자**시작 페이지가 표시됩니다. 계속하려면 **다음** 을 클릭합니다.  
  
### <a name="stored-procedure-validation"></a>저장 프로시저 유효성 검사  
 이 페이지에는 저장 프로시저에 네이티브 컴파일과 호환되지 않는 구문이 사용되었는지 여부가 표시됩니다. **다음** 을 클릭하여 세부 정보를 볼 수 있습니다. 네이티브 컴파일과 호환되지 않는 구문이 있는 경우 **다음** 을 클릭하여 세부 정보를 볼 수 있습니다.  
  
### <a name="stored-procedure-validation-result"></a>저장 프로시저 유효성 검사 결과  
 네이티브 컴파일과 호환되지 않는 구문이 있는 경우 **저장 프로시저 유효성 검사 결과** 페이지에 세부 정보가 표시됩니다. 보고서를 생성하고( **보고서 생성**클릭), **네이티브 컴파일 관리자**를 종료하고, 코드가 네이티브 컴파일과 호환되도록 업데이트할 수 있습니다.  
  
## <a name="code-sample"></a>코드 예제  
 다음 예에서는 해석된 저장 프로시저와 네이티브 컴파일을 사용했을 때의 해당 저장 프로시저를 보여 줍니다. 이 예에서는 c:\data라는 디렉터리를 사용합니다.  
  
```tsql  
CREATE DATABASE Demo  
ON  
PRIMARY(NAME = [Demo_data],  
FILENAME = 'C:\DATA\Demo_data.mdf', size=500MB)  
, FILEGROUP [Demo_fg] CONTAINS MEMORY_OPTIMIZED_DATA(  
NAME = [Demo_dir],  
FILENAME = 'C:\DATA\Demo_dir')  
LOG ON (name = [Demo_log], Filename='C:\DATA\Demo_log.ldf', size=500MB)  
COLLATE Latin1_General_100_BIN2;  
GO  
USE Demo;  
GO  
  
CREATE TABLE [dbo].[SalesOrders]  
(  
     [order_id] [int] NOT NULL,  
     [order_date] [datetime] NOT NULL,  
     [order_status] [tinyint] NOT NULL  
  
CONSTRAINT [PK_SalesOrders] PRIMARY KEY NONCLUSTERED HASH   
(  
     [order_id]  
)WITH ( BUCKET_COUNT = 2097152)  
)WITH ( MEMORY_OPTIMIZED = ON )  
  
go  
  
CREATE PROCEDURE [dbo].[InsertOrder] @id INT, @date DATETIME2, @status TINYINT  
AS   
BEGIN   
  
  INSERT dbo.SalesOrders VALUES (@id, @date, @status)  
  
END  
  
go  
  
CREATE PROCEDURE [dbo].[InsertOrderXTP] @id INT, @date DATETIME2, @status TINYINT  
  WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
AS   
BEGIN ATOMIC WITH   
(    TRANSACTION ISOLATION LEVEL = SNAPSHOT,  
     LANGUAGE = N'us_english')  
  
  INSERT dbo.SalesOrders VALUES (@id, @date, @status)  
  
END  
go  
  
select * from SalesOrders  
go  
exec dbo.InsertOrder @id= 10, @date = '1956-01-01 12:00:00', @status = 1 ;  
exec dbo.InsertOrderXTP @id= 11, @date = '1956-01-01 12:01:00', @status = 2 ;  
select * from SalesOrders  
```  
  
## <a name="see-also"></a>관련 항목:  
 [메모리 내 OLTP로 마이그레이션](migrating-to-in-memory-oltp.md)  
  
  
