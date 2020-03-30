---
title: 파일에서 이미지 삽입
description: 파일에서 이미지를 사용하는 방법을 설명합니다.
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: 35900aa2-5615-4174-8212-ba184c6b82fb
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: 9d80f5eec2c33fed635c18937185e2e21798e93b
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "78896719"
---
# <a name="inserting-an-image-from-a-file"></a>파일에서 이미지 삽입

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

데이터 원본에 있는 필드의 유형에 따라 BLOB(Binary Large Object) 이진 또는 문자 데이터로 데이터베이스에 쓸 수 있습니다. BLOB은 일반적으로 문서와 그림을 포함하는 `text`, `ntext` 및 `image` 데이터 형식을 지칭하는 일반 용어입니다.  
  
데이터베이스에 BLOB 값을 쓰려면 적합한 INSERT 또는 UPDATE 문을 실행하고 BLOB 값을 입력 매개 변수로 전달합니다. BLOB이 텍스트로 저장된 경우(예: SQL Server `text` 필드) BLOB을 문자열 매개 변수로 전달할 수 있습니다. BLOB이 이진 형식으로 저장된 경우(예: SQL Server `image` 필드) `byte` 형식의 배열을 이진 매개 변수로 전달할 수 있습니다.
  
## <a name="example"></a>예제  
다음 코드 예제에서는 Northwind 데이터베이스의 Employees 테이블에 직원 정보를 추가합니다. 직원의 사진을 파일에서 읽고 테이블의 Photo 필드(이미지 필드)에 추가합니다.  
  
```csharp  
public static void AddEmployee(  
  string lastName,   
  string firstName,   
  string title,   
  DateTime hireDate,   
  int reportsTo,   
  string photoFilePath,   
  string connectionString)  
{  
  byte[] photo = GetPhoto(photoFilePath);  
  
  using (SqlConnection connection = new SqlConnection(  
    connectionString))  
  
  SqlCommand command = new SqlCommand(  
    "INSERT INTO Employees (LastName, FirstName, " +  
    "Title, HireDate, ReportsTo, Photo) " +  
    "Values(@LastName, @FirstName, @Title, " +  
    "@HireDate, @ReportsTo, @Photo)", connection);   
  
  command.Parameters.Add("@LastName",    
     SqlDbType.NVarChar, 20).Value = lastName;  
  command.Parameters.Add("@FirstName",   
      SqlDbType.NVarChar, 10).Value = firstName;  
  command.Parameters.Add("@Title",       
      SqlDbType.NVarChar, 30).Value = title;  
  command.Parameters.Add("@HireDate",   
       SqlDbType.DateTime).Value = hireDate;  
  command.Parameters.Add("@ReportsTo",   
      SqlDbType.Int).Value = reportsTo;  
  
  command.Parameters.Add("@Photo",  
      SqlDbType.Image, photo.Length).Value = photo;  
  
  connection.Open();  
  command.ExecuteNonQuery();  
  }  
}  
  
public static byte[] GetPhoto(string filePath)  
{  
  FileStream stream = new FileStream(  
      filePath, FileMode.Open, FileAccess.Read);  
  BinaryReader reader = new BinaryReader(stream);  
  
  byte[] photo = reader.ReadBytes((int)stream.Length);  
  
  reader.Close();  
  stream.Close();  
  
  return photo;  
}  
```  
  
## <a name="next-steps"></a>다음 단계
- [SQL Server 이진 및 큰 값 데이터](sql-server-binary-large-value-data.md)
