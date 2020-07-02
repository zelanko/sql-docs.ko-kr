---
title: FileTableRootPath (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- FileTableRootPath_TSQL
- FileTableRootPath
dev_langs:
- TSQL
helpviewer_keywords:
- FileTableRootPath function
ms.assetid: 0cba908a-c85c-4b09-b16a-df1cb333c629
author: rothja
ms.author: jroth
ms.openlocfilehash: 1311ddfe90beafa3f3d89b27e510eac34aa5ae94
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85734404"
---
# <a name="filetablerootpath-transact-sql"></a>FileTableRootPath(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  특정 FileTable 또는 현재 데이터베이스에 대한 루트 수준 UNC 경로를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
FileTableRootPath ( [ '[schema_name.]FileTable_name' ], @option )  
```  
  
## <a name="arguments"></a>인수  
 *FileTable_name*  
 FileTable의 이름입니다. *FileTable_name* 은 **nvarchar**형식입니다. 선택적 매개 변수입니다. 기본값은 현재 데이터베이스입니다. *Schema_name* 지정도 선택 사항입니다. *FileTable_name* 에 대해 NULL을 전달 하 여 기본 매개 변수 값을 사용할 수 있습니다.  
  
 *\@option*  
 경로에 있는 서버 구성 요소의 형식을 지정하는 방법을 정의하는 정수 식입니다. * \@ 옵션* 은 다음 값 중 하나를 사용할 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**0**|NetBIOS 형식으로 변환된 서버 이름을 반환합니다. 예를 들면 다음과 같습니다.<br /><br /> `\\SERVERNAME\MSSQLSERVER\MyDocumentDatabase`<br /><br /> 기본값입니다.|  
|**1**|서버 이름을 변환하지 않고 반환합니다. 예를 들면 다음과 같습니다.<br /><br /> `\\ServerName\MSSQLSERVER\MyDocumentDatabase`|  
|**2**|전체 서버 경로를 반환합니다. 예를 들면 다음과 같습니다.<br /><br /> `\\ServerName.MyDomain.com\MSSQLSERVER\MyDocumentDatabase`|  
  
## <a name="return-type"></a>반환 형식  
 **nvarchar(4000)**  
  
 데이터베이스가 Always On 가용성 그룹에 속하는 경우 **FileTableRootPath** 함수는 컴퓨터 이름 대신 vnn (가상 네트워크 이름)을 반환 합니다.  
  
## <a name="general-remarks"></a>일반적인 주의 사항  
 **FileTableRootPath** 함수는 다음 조건 중 하나가 true 인 경우 NULL을 반환 합니다.  
  
-   *FileTable_name* 값이 잘못 되었습니다.  
  
-   호출자에게 지정된 테이블 또는 현재 데이터베이스를 참조할 수 있는 충분한 사용 권한이 없는 경우  
  
-   현재 데이터베이스에 대해 *DATABASE_DIRECTORY* FILESTREAM 옵션이 설정 되지 않았습니다.  
  
 자세한 내용은 [Work with Directories and Paths in FileTables](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md)을 참조하세요.  
  
## <a name="best-practices"></a>모범 사례  
 코드와 애플리케이션을 현재 컴퓨터 및 데이터베이스 외에서도 사용할 수 있도록 하려면 코드를 작성할 때 절대 파일 경로를 사용하지 않는 것이 좋습니다. 대신, 다음 예제와 같이 **FileTableRootPath** 및 **GetFileNamespacePath** 함수를 함께 사용 하 여 런타임에 파일의 전체 경로를 가져옵니다. 기본적으로 **GetFileNamespacePath** 함수는 데이터베이스의 루트 경로 아래에 있는 파일의 상대 경로를 반환합니다.  
  
```sql  
USE MyDocumentDatabase;  
  
@root varchar(100)  
SELECT @root = FileTableRootPath();  
@fullPath = varchar(1000);  
  
SELECT @fullPath = @root + file_stream.GetFileNamespacePath()  
FROM DocumentStore  
WHERE Name = N'document.docx';  
```  
  
## <a name="security"></a>보안  
  
### <a name="permissions"></a>사용 권한  
 **FileTableRootPath** 함수에는 다음이 필요 합니다.  
  
-   특정 FileTable의 루트 경로를 가져올 수 있는 FileTable에 대한 SELECT 권한  
  
-   현재 데이터베이스의 루트 경로를 가져올 수 있는 권한이 **db_datareader** 이상입니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 **FileTableRootPath** 함수를 호출 하는 방법을 보여 줍니다.  
  
```  
USE MyDocumentDatabase;  
-- returns "\\MYSERVER\MSSQLSERVER\MyDocumentDatabase"  
SELECT FileTableRootPath();  
  
-- returns "\\MYSERVER\MSSQLSERVER\MyDocumentDatabase\MyFileTable"  
SELECT FileTableRootPath(N'dbo.MyFileTable');  
  
-- returns "\\MYSERVER\MSSQLSERVER\MyDocumentDatabase\MyFileTable"  
SELECT FileTableRootPath(N'MyFileTable');  
```  
  
## <a name="see-also"></a>참고 항목  
 [FileTable에서 디렉터리 및 경로 작업](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md)  
  
  
