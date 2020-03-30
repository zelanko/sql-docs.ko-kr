---
title: ADO.NET에서 큰 값(최대) 데이터 수정
description: 큰 값 데이터 형식을 사용하는 방법을 설명합니다.
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: 8aca5f00-d80e-4320-81b3-016d0466f7ee
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: 9acbd8fb795fe1a14e77e5d746f729d37c11cc8d
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "78896682"
---
# <a name="modifying-large-value-max-data-in-adonet"></a>ADO.NET에서 큰 값(최대) 데이터 수정

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

LOB(Large Object) 데이터 형식은 최대 행 크기가 8KB를 초과하는 형식입니다. SQL Server는 `max`, `varchar` 및 `nvarchar` 데이터 형식에 사용할 수 있는 `varbinary` 지정자를 도입하여 2^32바이트에 이르는 큰 값도 저장할 수 있습니다. 테이블 열과 Transact-SQL 변수는 `varchar(max)`, `nvarchar(max)` 또는 `varbinary(max)` 데이터 형식을 지정할 수 있습니다. .NET에서는 `max`를 사용하여 새로운 `DataReader` 데이터 형식을 가져올 수 있을 뿐 아니라 특별한 처리 없이도 입력 및 출력 매개 변수 값을 모두 지정할 수 있습니다. 큰 `varchar` 데이터 형식의 경우 데이터를 증분 방식으로 검색하고 업데이트할 수 있습니다.  
  
`max` 데이터 형식을 사용하여 비교 및 연결 작업을 수행할 수 있으며, 비교를 수행할 경우에는 Transact-SQL 변수로 사용합니다. SELECT 문의 DISTINCT, ORDER BY, GROUP BY 절에서뿐 아니라 집계, 조인 및 하위 쿼리에도 사용할 수 있습니다.

큰 값 데이터 형식에 대한 자세한 내용은 SQL Server 온라인 설명서의 [큰 값 데이터 형식 사용](https://go.microsoft.com/fwlink/?LinkId=120498)을 참조하세요.
  
## <a name="large-value-type-restrictions"></a>큰 값 형식 제한 사항  
`max` 데이터 형식에는 더 작은 데이터 형식에서는 존재하지 않는 다음 제한 사항이 적용됩니다.  
  
- `sql_variant`는 큰 `varchar` 데이터 형식을 포함할 수 없습니다.  
  
- 긴 `varchar` 열을 인덱스의 키 열로 지정할 수 없습니다. 비클러스터형 인덱스의 포괄 열에는 허용됩니다.  
  
- 큰 `varchar` 열을 분할 키 열로 사용할 수 없습니다.  
  
## <a name="working-with-large-value-types-in-transact-sql"></a>Transact-SQL에서의 큰 값 형식 사용  
Transact-SQL `OPENROWSET` 함수는 원격 데이터에 연결하고 액세스하는 일회성 방법입니다. `OPENROWSET`는 테이블 이름처럼 쿼리의 FROM 절에서 참조될 수 있습니다. 또한 INSERT, UPDATE 또는 DELETE 문의 대상 테이블로 참조될 수도 있습니다.  
  
`OPENROWSET` 함수에는 `BULK` 행 집합 공급자가 포함되어 있어 데이터를 대상 테이블에 로드하지 않고 파일에서 직접 데이터를 읽을 수 있습니다. 따라서 간단한 INSERT SELECT 문에서도 `OPENROWSET`를 사용할 수 있습니다.  
  
`OPENROWSET BULK` 선택적 인수를 사용하면 데이터 읽기의 시작 및 종료 지점, 오류 처리 방법 및 데이터 해석 방법을 효과적으로 제어할 수 있습니다. 예를 들어 `varbinary`, `varchar` 또는 `nvarchar` 형식의 단일 행 및 단일 열로 된 행 집합으로 데이터 파일을 읽도록 지정할 수 있습니다. 전체 구문 및 옵션에 대한 자세한 내용은 SQL Server 온라인 설명서를 참조하세요.  
  
다음 예제에서는 AdventureWorks 샘플 데이터베이스의 ProductPhoto 테이블에 사진을 삽입합니다. `BULK OPENROWSET` 공급자를 사용하는 경우 모든 열에 값을 삽입하지 않더라도 명명된 열 목록을 제공해야 합니다. 이 경우 기본 키는 ID 열로 정의되며 열 목록에서 생략될 수 있습니다. 또한 `OPENROWSET` 문의 끝에 상관 관계 이름을 제공해야 합니다. 이 경우에는 ThumbnailPhoto입니다. 이는 파일이 로드되는 `ProductPhoto` 테이블의 열과 관련이 있습니다.  
  
```sql
INSERT Production.ProductPhoto (  
    ThumbnailPhoto,   
    ThumbnailPhotoFilePath,   
    LargePhoto,   
    LargePhotoFilePath)  
SELECT ThumbnailPhoto.*, null, null, N'tricycle_pink.gif'  
FROM OPENROWSET   
    (BULK 'c:\images\tricycle.jpg', SINGLE_BLOB) ThumbnailPhoto  
```  
  
## <a name="updating-data-using-update-write"></a>UPDATE .WRITE를 사용하여 데이터 업데이트  
Transact-SQL UPDATE 문에는 `varchar(max)`, `nvarchar(max)` 또는 `varbinary(max)` 열의 내용을 수정하기 위한 새로운 WRITE 구문이 있습니다. 이 구문을 사용하면 데이터 부분 업데이트를 수행할 수 있습니다. UPDATE .WRITE 구문은 다음과 같이 축약된 형식으로 표시됩니다.  
  
UPDATE  
  
{ *\<object>* }  
  
SET  
  
{ *column_name* = { .WRITE ( *expression* , @Offset , @Length ) }  
  
WRITE 메서드에서는 *column_name* 값의 일정 부분이 수정되도록 지정합니다. 식은 *column_name*에 복사되는 값이고, `@Offset`은 식이 작성되는 시작점이며, `@Length` 인수는 열에 있는 일정 부분의 길이입니다.  
  
|다음과 같은 경우|작업|  
|--------|----------|  
|식이 NULL로 설정되었습니다.|`@Length`가 무시되고 *column_name*의 값은 지정된 `@Offset`에서 잘립니다.|  
|`@Offset`은 NULL입니다.|업데이트 작업을 통해 기존 *column_name* 값의 끝에 식이 추가되고 `@Length`는 무시됩니다.|  
|`@Offset`이 column_name 값의 길이 보다 큰 경우|SQL Server에서 오류를 반환합니다.|  
|`@Length`은 NULL입니다.|업데이트 작업 시 `@Offset`에서부터 `column_name` 값의 끝까지 모든 데이터를 제거합니다.|  
  
> [!NOTE]
>  `@Offset` 및 `@Length` 모두 음수일 수 없습니다.  
  
## <a name="example"></a>예제  
이 Transact-SQL 예제는 AdventureWorks 데이터베이스의 Document 테이블에 있는 `nvarchar(max)` 열인 DocumentSummary에서 부분 값을 업데이트합니다. 대체 단어, 기존 데이터에서 대체할 단어의 시작 위치(오프셋), 그리고 대체할 문자 수(길이)를 지정함으로써 ‘구성 요소’가 로 ‘기능’으로 대체됩니다. 예제에는 결과를 비교하기 위해 UPDATE 문 앞뒤에 SELECT 문이 포함되어 있습니다.  
  
```sql
USE AdventureWorks;  
GO  
--View the existing value.  
SELECT DocumentSummary  
FROM Production.Document  
WHERE DocumentID = 3;  
GO  
-- The first sentence of the results will be:  
-- Reflectors are vital safety components of your bicycle.  
  
--Modify a single word in the DocumentSummary column  
UPDATE Production.Document  
SET DocumentSummary .WRITE (N'features',28,10)  
WHERE DocumentID = 3 ;  
GO   
--View the modified value.  
SELECT DocumentSummary  
FROM Production.Document  
WHERE DocumentID = 3;  
GO  
-- The first sentence of the results will be:  
-- Reflectors are vital safety features of your bicycle.  
```  
  
## <a name="working-with-large-value-types-in-adonet"></a>ADO.NET에서의 큰 값 형식 사용  
ADO.NET에서는 <xref:Microsoft.Data.SqlClient.SqlParameter>에서 <xref:Microsoft.Data.SqlClient.SqlDataReader> 개체로 지정하여 결과 집합을 반환하거나 <xref:Microsoft.Data.SqlClient.SqlDataAdapter>를 사용하여 `DataSet`/`DataTable`을 채우는 방식으로 큰 값 형식을 사용할 수 있습니다. 큰 값 형식을 사용하는 방식과 이와 관련된 작은 값 데이터 형식을 사용하는 방법에는 차이가 없습니다.  
  
### <a name="using-getsqlbytes-to-retrieve-data"></a>GetSqlBytes를 사용하여 데이터 검색  
`GetSqlBytes`의 <xref:Microsoft.Data.SqlClient.SqlDataReader> 메서드를 사용하여 `varbinary(max)` 열의 내용을 검색할 수 있습니다. 다음 코드 조각에서는 테이블에서 <xref:Microsoft.Data.SqlClient.SqlCommand> 데이터를 선택하는 `cmd`라는 `varbinary(max)` 개체와 <xref:Microsoft.Data.SqlClient.SqlDataReader>로 데이터를 검색하는 `reader`라는 <xref:System.Data.SqlTypes.SqlBytes> 개체를 가정합니다.  
  
```csharp  
reader = cmd.ExecuteReader(CommandBehavior.CloseConnection);  
while (reader.Read())  
    {  
        SqlBytes bytes = reader.GetSqlBytes(0);  
    }  
```  
  
### <a name="using-getsqlchars-to-retrieve-data"></a>GetSqlChars를 사용하여 데이터 검색  
`GetSqlChars`의 <xref:Microsoft.Data.SqlClient.SqlDataReader> 메서드를 사용하여 `varchar(max)` 또는 `nvarchar(max)` 열의 내용을 검색할 수 있습니다. 다음 코드 조각에서는 테이블에서 <xref:Microsoft.Data.SqlClient.SqlCommand> 데이터를 선택하는 `cmd`라는 `nvarchar(max)` 개체와 데이터를 검색하는 <xref:Microsoft.Data.SqlClient.SqlDataReader>라는 `reader` 개체를 가정합니다.   
  
```csharp  
reader = cmd.ExecuteReader(CommandBehavior.CloseConnection);  
while (reader.Read())  
{  
    SqlChars buffer = reader.GetSqlChars(0);  
}  
```  
  
### <a name="using-getsqlbinary-to-retrieve-data"></a>GetSqlBinary를 사용하여 데이터 검색  
`GetSqlBinary`의 <xref:Microsoft.Data.SqlClient.SqlDataReader> 메서드를 사용하여 `varbinary(max)` 열의 내용을 검색할 수 있습니다. 다음 코드 조각에서는 테이블에서 <xref:Microsoft.Data.SqlClient.SqlCommand> 데이터를 선택하는 `cmd`라는 `varbinary(max)` 개체와 <xref:Microsoft.Data.SqlClient.SqlDataReader> 스트림으로 데이터를 검색하는 `reader`라는 <xref:System.Data.SqlTypes.SqlBinary> 개체를 가정합니다.  
  
```csharp  
reader = cmd.ExecuteReader(CommandBehavior.CloseConnection);  
while (reader.Read())  
    {  
        SqlBinary binaryStream = reader.GetSqlBinary(0);  
    }  
```  
  
### <a name="using-getbytes-to-retrieve-data"></a>GetBytes를 사용하여 데이터 검색  
`GetBytes`의 <xref:Microsoft.Data.SqlClient.SqlDataReader> 메서드는 지정된 열 오프셋의 바이트 스트림을 지정된 배열 오프셋에서 시작하는 바이트 배열로 읽어옵니다. 다음 코드 조각에서는 바이트를 바이트 배열로 검색하는 <xref:Microsoft.Data.SqlClient.SqlDataReader>라는 `reader` 개체를 가정합니다. `GetSqlBytes`와 달리 `GetBytes`에는 배열 버퍼의 크기가 필요합니다.  
  
```csharp  
while (reader.Read())  
{  
    byte[] buffer = new byte[4000];  
    long byteCount = reader.GetBytes(1, 0, buffer, 0, 4000);  
}  
```  
  
### <a name="using-getvalue-to-retrieve-data"></a>GetValue를 사용하여 데이터 검색  
`GetValue`의 <xref:Microsoft.Data.SqlClient.SqlDataReader> 메서드는 지정된 열 오프셋에서 배열로 값을 읽습니다. 다음 코드 조각에서는 첫 번째 열 오프셋에서 이진 데이터를 검색한 다음 두 번째 열 오프셋에서 문자열 데이터를 검색하는 <xref:Microsoft.Data.SqlClient.SqlDataReader>라는 `reader` 개체를 가정합니다.  
  
```csharp  
while (reader.Read())  
{  
    // Read the data from varbinary(max) column  
    byte[] binaryData = (byte[])reader.GetValue(0);  
  
    // Read the data from varchar(max) or nvarchar(max) column  
    String stringData = (String)reader.GetValue(1);  
}  
```  
  
## <a name="converting-from-large-value-types-to-clr-types"></a>큰 값 형식에서 CLR 형식으로 변환  
`varchar(max)` 같은 문자열 변환 메서드를 사용하여 `nvarchar(max)` 또는 `ToString` 열의 내용을 변환할 수 있습니다. 다음 코드 조각에서는 데이터를 검색하는 <xref:Microsoft.Data.SqlClient.SqlDataReader>라는 `reader` 개체를 가정합니다.  
  
```csharp  
while (reader.Read())  
{  
     string str = reader[0].ToString();  
     Console.WriteLine(str);  
}  
```  
  
### <a name="example"></a>예제  
다음 코드는 `LargePhoto` 데이터베이스의 `ProductPhoto` 테이블에서 이름 및 `AdventureWorks` 개체를 검색하여 파일에 저장합니다. 어셈블리는 <xref:System.Drawing> 네임스페이스에 대한 참조를 사용하여 컴파일해야 합니다.  <xref:Microsoft.Data.SqlClient.SqlDataReader.GetSqlBytes%2A>의 <xref:Microsoft.Data.SqlClient.SqlDataReader> 메서드는 <xref:System.Data.SqlTypes.SqlBytes> 속성을 노출하는 `Stream` 개체를 반환합니다. 코드에서는 이 개체를 사용하여 새 `Bitmap` 개체를 만든 다음 Gif `ImageFormat`으로 저장합니다.  
  
[!code-csharp[DataWorks SqlBytes_Stream#1](~/../sqlclient/doc/samples/SqlBytes_Stream.cs#1)]
  
## <a name="using-large-value-type-parameters"></a>큰 값 형식 매개 변수 사용  
<xref:Microsoft.Data.SqlClient.SqlParameter> 개체에서 더 작은 값 형식을 사용하는 것과 같은 방법으로 <xref:Microsoft.Data.SqlClient.SqlParameter> 개체에서 큰 값 형식을 사용할 수 있습니다. 다음 예제에서처럼 큰 값 형식은 <xref:Microsoft.Data.SqlClient.SqlParameter> 값으로 검색할 수 있습니다. 이 코드에서는 다음 GetDocumentSummary 저장 프로시저가 AdventureWorks 샘플 데이터베이스에 있다고 가정합니다. 저장 프로시저는 @DocumentID라는 입력 매개 변수를 사용하여 @DocumentSummary 출력 매개 변수에 DocumentSummary 열의 내용을 반환합니다.  
  
```sql
CREATE PROCEDURE GetDocumentSummary   
(  
    @DocumentID int,  
    @DocumentSummary nvarchar(MAX) OUTPUT  
)  
AS  
SET NOCOUNT ON  
SELECT  @DocumentSummary=Convert(nvarchar(MAX), DocumentSummary)  
FROM    Production.Document  
WHERE   DocumentID=@DocumentID  
```  
  
### <a name="example"></a>예제  
ADO.NET 코드는 <xref:Microsoft.Data.SqlClient.SqlConnection> 및 <xref:Microsoft.Data.SqlClient.SqlCommand> 개체를 만들어 GetDocumentSummary 저장 프로시저를 실행하고 문서 요약을 검색하여 큰 값 형식으로 저장합니다. 이 코드에서는 @DocumentID 입력 매개 변수 값을 전달한 다음 콘솔 창에 @DocumentSummary 출력 매개 변수에 다시 전달된 결과를 표시합니다.  
  
[!code-csharp[DataWorks SqlParameter_Value#1](~/../sqlclient/doc/samples/SqlParameter_Value.cs#1)]
  
## <a name="next-steps"></a>다음 단계
- [SQL Server 이진 및 큰 값 데이터](sql-server-binary-large-value-data.md)
- [ADO.NET의 SQL Server 데이터 작업](sql-server-data-operations.md)
