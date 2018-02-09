---
title: FileTableRootPath (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- FileTableRootPath_TSQL
- FileTableRootPath
dev_langs:
- TSQL
helpviewer_keywords:
- FileTableRootPath function
ms.assetid: 0cba908a-c85c-4b09-b16a-df1cb333c629
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1dd6d1b54d92142f3089b6323127257341ffe4d4
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/09/2018
---
# <a name="filetablerootpath-transact-sql"></a>FileTableRootPath(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  특정 FileTable 또는 현재 데이터베이스에 대한 루트 수준 UNC 경로를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
FileTableRootPath ( [ ‘[schema_name.]FileTable_name’ ], @option )  
```  
  
## <a name="arguments"></a>인수  
 *FileTable_name*  
 FileTable의 이름입니다. *FileTable_name* 유형의 **nvarchar**합니다. 선택적 매개 변수입니다. 기본값은 현재 데이터베이스입니다. 지정 *schema_name* 요소도 선택적 항목입니다. NULL을 전달 *FileTable_name* 기본 매개 변수 값을 사용 하려면  
  
 *@option*  
 경로에 있는 서버 구성 요소의 형식을 지정하는 방법을 정의하는 정수 식입니다. *@option*다음 값 중 하나일 수 있습니다.  
  
|Value|설명|  
|-----------|-----------------|  
|**0**|NetBIOS 형식으로 변환된 서버 이름을 반환합니다. 예를 들면 다음과 같습니다.<br /><br /> `\\SERVERNAME\MSSQLSERVER\MyDocumentDB`<br /><br /> 이 값은 기본값입니다.|  
|**1**|서버 이름을 변환하지 않고 반환합니다. 예를 들면 다음과 같습니다.<br /><br /> `\\ServerName\MSSQLSERVER\MyDocumentDB`|  
|**2**|전체 서버 경로를 반환합니다. 예를 들면 다음과 같습니다.<br /><br /> `\\ServerName.MyDomain.com\MSSQLSERVER\MyDocumentDB`|  
  
## <a name="return-type"></a>반환 형식  
 **nvarchar(4000)**  
  
 데이터베이스는 Always On 가용성 그룹에 속해 있을 때 면 **FileTableRootPath** 함수가 컴퓨터 이름 대신 (VNN) 가상 네트워크 이름 반환 합니다.  
  
## <a name="general-remarks"></a>일반적인 주의 사항  
 **FileTableRootPath** 함수는 다음 조건 중 하나에 NULL을 반환 합니다.  
  
-   값 *FileTable_name* 올바르지 않습니다.  
  
-   호출자에게 지정된 테이블 또는 현재 데이터베이스를 참조할 수 있는 충분한 사용 권한이 없는 경우  
  
-   FILESTREAM 옵션이 *database_directory* 현재 데이터베이스에 대해 설정 되지 않았습니다.  
  
 자세한 내용은 [Work with Directories and Paths in FileTables](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md)을 참조하세요.  
  
## <a name="best-practices"></a>최선의 구현 방법  
 코드와 응용 프로그램을 현재 컴퓨터 및 데이터베이스 외에서도 사용할 수 있도록 하려면 코드를 작성할 때 절대 파일 경로를 사용하지 않는 것이 좋습니다. 대신 전체 경로 파일에 대 한 런타임 시 사용 하 여 가져올는 **FileTableRootPath** 및 **GetFileNamespacePath** 함수를 다음 예제에 표시 된 대로 함께 합니다. 기본적으로 **GetFileNamespacePath** 함수는 데이터베이스의 루트 경로 아래에 있는 파일의 상대 경로를 반환합니다.  
  
```sql  
USE MyDocumentDB;  
  
@root varchar(100)  
SELECT @root = FileTableRootPath();  
@fullPath = varchar(1000);  
  
SELECT @fullPath = @root + file_stream.GetFileNamespacePath()  
FROM DocumentStore  
WHERE Name = N’document.docx’;  
```  
  
## <a name="security"></a>보안  
  
### <a name="permissions"></a>Permissions  
 **FileTableRootPath** 함수에 필요 합니다.  
  
-   특정 FileTable의 루트 경로를 가져올 수 있는 FileTable에 대한 SELECT 권한  
  
-   **db_datareader** 또는 상위 사용 권한이 현재 데이터베이스에 대 한 루트 경로 가져올 수 있습니다.  
  
## <a name="examples"></a>예  
 다음 예제에서는 호출 하는 방법을 보여는 **FileTableRootPath** 함수입니다.  
  
```  
USE MyDocumentDB;  
-- returns “\\MYSERVER\MSSQLSERVER\MyDocumentDB”  
SELECT FileTableRootPath();  
  
-- returns “\\MYSERVER\MSSQLSERVER\MyDocumentDB\MyFileTable”  
SELECT FileTableRootPath(N'dbo.MyFileTable');  
  
-- returns “\\MYSERVER\MSSQLSERVER\MyDocumentDB\MyFileTable”  
SELECT FileTableRootPath(N'MyFileTable');  
```  
  
## <a name="see-also"></a>관련 항목:  
 [FileTable에서 디렉터리 및 경로 작업](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md)  
  
  
