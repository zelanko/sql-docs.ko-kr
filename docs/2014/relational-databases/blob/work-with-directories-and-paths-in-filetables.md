---
title: FileTable에서 디렉터리 및 경로 작업 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FileTables [SQL Server], directories
ms.assetid: f1e45900-bea0-4f6f-924e-c11e1f98ab62
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ca25b7c537c333d6bc9eb7745ea2ec6ad6055c4b
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58536505"
---
# <a name="work-with-directories-and-paths-in-filetables"></a>FileTable에서 디렉터리 및 경로 작업
  파일이 FileTable에 저장되는 디렉터리 구조에 대해 설명합니다.  
  
##  <a name="HowToDirectories"></a> 어떻게: FileTable에서 디렉터리 및 경로 작업  
 다음 세 개의 함수를 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 FileTable 디렉터리 작업을 수행할 수 있습니다.  
  
|원하는 결과|사용할 함수|  
|------------------------|-----------------------|  
|특정 FileTable 또는 현재 데이터베이스에 대한 루트 수준 UNC 경로를 가져옵니다.|[FileTableRootPath&#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/filetablerootpath-transact-sql)|  
|FileTable의 파일이나 디렉터리에 대한 절대 또는 상대 UNC 경로를 가져옵니다.|[GetFileNamespacePath&#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/getfilenamespacepath-transact-sql)|  
|경로를 제공하여 FileTable의 지정된 파일 또는 디렉터리에 대한 경로 로케이터 ID 값을 가져옵니다.|[GetPathLocator&#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/getpathlocator-transact-sql)|  
  
##  <a name="BestPracticeRelativePaths"></a> 어떻게: 이식 가능한 코드에 상대 경로 사용  
 코드와 애플리케이션을 현재 컴퓨터 및 데이터베이스 외에서도 사용할 수 있도록 하려면 코드를 작성할 때 절대 파일 경로를 사용하지 않는 것이 좋습니다. 대신 다음 예와 같이 [FileTableRootPath&#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/filetablerootpath-transact-sql) 및 [GetFileNamespacePath&#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/getfilenamespacepath-transact-sql) 함수를 함께 사용하여 런타임에 파일의 전체 경로를 가져옵니다. 기본적으로 `GetFileNamespacePath` 함수는 데이터베이스의 루트 경로 아래에 있는 파일의 상대 경로를 반환합니다.  
  
```sql  
USE database_name;  
DECLARE @root nvarchar(100);  
DECLARE @fullpath nvarchar(1000);  
  
SELECT @root = FileTableRootPath();  
SELECT @fullpath = @root + file_stream.GetFileNamespacePath()  
    FROM filetable_name  
    WHERE name = N'document_name';  
  
PRINT @fullpath;  
GO  
```  
  
##  <a name="restrictions"></a> 중요 제한 사항  
  
###  <a name="nesting"></a> 중첩 수준  
  
> [!IMPORTANT]  
>  15개 수준을 초과하는 하위 디렉터리를 FileTable 디렉터리에 저장할 수 없습니다. 15개 수준의 하위 디렉터리를 저장할 경우 최하위 수준에는 파일이 포함될 수 없습니다. 최하위 수준에 파일이 있으면 수준이 초과됩니다.  
  
###  <a name="fqnlength"></a> 전체 경로 이름의 길이  
  
> [!IMPORTANT]  
>  NTFS 파일 시스템은 Windows 셸 및 대부분의 Windows API의 260자 제한보다 긴 경로 이름을 지원합니다. 따라서 전체 경로 이름이 260자를 초과할 수 있기 때문에 Windows 탐색기 또는 다른 많은 Windows 애플리케이션으로 보거나 열 수 없는 Transact-SQL을 사용하여 FileTable의 파일 계층에 파일을 만들 수 있습니다. 그러나 Transact-SQL을 사용해서도 이러한 파일에 계속 액세스할 수 있습니다.  
  
##  <a name="fullpath"></a> FileTable에 저장된 항목의 전체 경로  
 FileTable에 저장된 파일 또는 디렉터리의 전체 경로는 다음 요소로 시작됩니다.  
  
1.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 수준에서 파일 I/O 액세스를 위해 설정된 공유  
  
2.  데이터베이스 수준에서 지정된 **DIRECTORY_NAME**  
  
3.  FileTable 수준에서 지정된 **FILETABLE_DIRECTORY**  
  
 결과 계층 구조는 다음과 같습니다.  
  
 `\\<machine>\<instance-level FILESTREAM share>\<database-level directory>\<FileTable directory>\`  
  
 이 디렉터리 계층 구조는 FileTable 파일 네임스페이스의 루트를 구성합니다. 이 디렉터리 계층 구조 아래에 FileTable에 대한 FILESTREAM 데이터가 파일 및 하위 디렉터리로 저장되며, 이 하위 디렉터리도 파일과 하위 디렉터리를 포함할 수 있습니다.  
  
 인스턴스 수준 FILESTREAM 공유에 만들어지는 디렉터리 계층 구조는 가상 디렉터리 계층 구조라는 것을 유념해야 합니다. 이 계층 구조는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 저장되며 NTFS 파일 시스템에는 물리적으로 표시되지 않습니다. 이 FILESTREAM 공유 및 여기에 포함된 FileTable에서 파일 및 디렉터리에 액세스하는 모든 작업은 파일 시스템에 포함된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 요소에서 가로채어 처리합니다.  
  
##  <a name="roots"></a> 인스턴스, 데이터베이스 및 FileTable 수준에서 루트 디렉터리의 의미 체계  
 이 디렉터리 계층 구조는 다음과 같은 의미 체계를 적용합니다.  
  
-   인스턴스 수준 FILESTREAM 공유는 관리자에 의해 구성되어 서버 속성으로 저장됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자를 사용하여 이 공유의 이름을 바꿀 수 있습니다. 이름 바꾸기 작업을 적용하려면 서버를 다시 시작해야 합니다.  
  
-   새 데이터베이스를 만들 때 데이터베이스 수준 **DIRECTORY_NAME** 은 기본적으로 null입니다. 관리자는 **ALTER DATABASE** 문을 사용하여 이 이름을 설정하거나 변경할 수 있습니다. 이름은 해당 인스턴스에서 고유해야 하며 대/소문자를 구분하지 않습니다.  
  
-   일반적으로 FileTable을 만들 때 **FILETABLE_DIRECTORY** 이름을 **CREATE TABLE** 문의 일부로 제공합니다. **ALTER TABLE** 명령을 사용하여 이 이름을 변경할 수 있습니다.  
  
-   파일 I/O 작업을 통해 이 루트 디렉터리의 이름을 바꿀 수 없습니다.  
  
-   이러한 루트 디렉터리는 단독 파일 핸들로 열 수 있습니다.  
  
##  <a name="is_directory"></a> FileTable 스키마의 is_directory 열  
 다음 표에서는 **is_directory** 열과 FileTable의 FILESTREAM 데이터가 포함된 **file_stream** 열 간의 상호 작용에 대해 설명합니다.  
  
||||  
|-|-|-|  
|*is_directory* **값**|*file_stream* **값**|**동작**|  
|FALSE|NULL|이는 시스템 정의 제약 조건에 의해 catch되는 잘못된 조합입니다.|  
|FALSE|\<value>|항목은 파일을 나타냅니다.|  
|TRUE|NULL|항목은 디렉터리를 나타냅니다.|  
|TRUE|\<값>|이는 시스템 정의 제약 조건에 의해 catch되는 잘못된 조합입니다.|  
  
##  <a name="alwayson"></a> AlwaysOn 가용성 그룹에 VNN(가상 네트워크 이름) 사용  
 FILESTREAM 또는 FileTable 데이터가 포함된 데이터베이스가 AlwaysOn 가용성 그룹에 속하는 경우  
  
-   FILESTREAM 및 FileTable 함수가 컴퓨터 이름 대신 VNN(가상 네트워크 이름)을 사용하거나 반환합니다. 이러한 함수에 대한 자세한 내용은 [Filestream 및 FileTable 함수&#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/filestream-and-filetable-functions-transact-sql)를 참조하세요.  
  
-   파일 시스템 API를 통한 FILESTREAM 또는 FileTable 데이터에 대한 모든 액세스에는 컴퓨터 이름 대신 VNN이 사용되어야 합니다. 자세한 내용은 [AlwaysOn 가용성 그룹의 FILESTREAM 및 FileTable&#40;SQL Server&#41;](../../database-engine/availability-groups/windows/filestream-and-filetable-with-always-on-availability-groups-sql-server.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [FileTable의 필수 구성 요소를 사용하도록 설정](enable-the-prerequisites-for-filetable.md)   
 [FileTable 만들기, 변경 및 삭제](create-alter-and-drop-filetables.md)   
 [Transact-SQL을 사용하여 FileTable에 액세스](access-filetables-with-transact-sql.md)   
 [파일 입/출력 API를 사용하여 FileTable 액세스](access-filetables-with-file-input-output-apis.md)  
  
  
