---
title: GetFileNamespacePath (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
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
- GetFileNamespacePath
- GetFileNamespacePath_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- GetFileNamespacePath function
ms.assetid: b393ecef-baa8-4d05-a268-b2f309fce89a
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3f5c7dcdc32fa7f7d9519b00f5d33d9d0083ca85
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/09/2018
---
# <a name="getfilenamespacepath-transact-sql"></a>GetFileNamespacePath(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  FileTable의 파일 또는 디렉터리에 대한 UNC 경로를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
<column-name>.GetFileNamespacePath(is_full_path, @option)  
```  
  
## <a name="arguments"></a>인수  
 *column-name*  
 varbinary (max) 열 이름을 **file_stream** FileTable의 열입니다.  
  
 *열 이름* 값 유효한 열 이름 이어야 합니다. 식이나 다른 데이터 형식의 열에서 변환 또는 캐스팅된 값은 사용할 수 없습니다.  
  
 *is_full_path*  
 상대 경로를 반환할지 절대 경로를 반환할지 지정하는 정수 식입니다. *is_full_path* 다음 값 중 하나일 수 있습니다.  
  
|Value|설명|  
|-----------|-----------------|  
|**0**|데이터베이스 수준 디렉터리 내에서의 상대 경로를 반환합니다.<br /><br /> 기본값입니다.|  
|**1**|`\\computer_name`으로 시작하는 전체 UNC 경로를 반환합니다.|  
  
 *@option*  
 경로에 있는 서버 구성 요소의 형식을 지정하는 방법을 정의하는 정수 식입니다. *@option*다음 값 중 하나일 수 있습니다.  
  
|Value|설명|  
|-----------|-----------------|  
|**0**|NetBIOS 형식으로 변환된 서버 이름을 반환합니다. 예를 들면 다음과 같습니다.<br /><br /> `\\SERVERNAME\MSSQLSERVER\MyDocumentDB`<br /><br /> 이 값은 기본값입니다.|  
|**1**|서버 이름을 변환하지 않고 반환합니다. 예를 들면 다음과 같습니다.<br /><br /> `\\ServerName\MSSQLSERVER\MyDocumentDB`|  
|**2**|전체 서버 경로를 반환합니다. 예를 들면 다음과 같습니다.<br /><br /> `\\ServerName.MyDomain.com\MSSQLSERVER\MyDocumentDB`|  
  
## <a name="return-type"></a>반환 형식  
 **nvarchar(max)**  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 장애 조치(Failover) 클러스터에 클러스터된 경우 이 경로의 일부로 반환된 컴퓨터 이름은 클러스터형 인스턴스의 가상 호스트 이름입니다.  
  
 데이터베이스는 Always On 가용성 그룹에 속해 있을 때 면 **FileTableRootPath** 함수가 컴퓨터 이름 대신 (VNN) 가상 네트워크 이름 반환 합니다.  
  
## <a name="general-remarks"></a>일반적인 주의 사항  
 경로는 **GetFileNamespacePath** 함수는 다음과 같은 형식의 논리 디렉터리 또는 파일 경로 반환 합니다.  
  
 `\\<machine>\<instance-level FILESTREAM share>\<database-level directory>\<FileTable directory>\...`  
  
 이 논리 경로는 물리적 NTFS 경로에 직접적으로 대응되지는 않습니다. 이 논리 경로는 FILESTREAM의 파일 시스템 필터 드라이버 및 FILESTREAM 에이전트에 의해 물리적 경로로 변환됩니다. 논리 경로와 물리적 경로를 구분하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 경로 유효성에 영향을 주지 않고 내부적으로 데이터를 다시 구성할 수 있습니다.  
  
## <a name="best-practices"></a>최선의 구현 방법  
 코드와 응용 프로그램을 현재 컴퓨터 및 데이터베이스 외에서도 사용할 수 있도록 하려면 코드를 작성할 때 절대 파일 경로를 사용하지 않는 것이 좋습니다. 대신 전체 경로 파일에 대 한 런타임 시 사용 하 여 가져올는 **FileTableRootPath** 및 **GetFileNamespacePath** 함수를 다음 예제에 표시 된 대로 함께 합니다. 기본적으로 **GetFileNamespacePath** 함수는 데이터베이스의 루트 경로 아래에 있는 파일의 상대 경로를 반환합니다.  
  
```sql  
USE MyDocumentDB;  
@root varchar(100)  
SELECT @root = FileTableRootPath();  
  
@fullPath = varchar(1000);  
SELECT @fullPath = @root + file_stream.GetFileNamespacePath() FROM DocumentStore  
WHERE Name = N’document.docx’;  
```  
  
## <a name="remarks"></a>주의  
  
## <a name="examples"></a>예  
 다음 예제에서는 호출 하는 방법을 보여는 **GetFileNamespacePath** 함수를 파일이 나 FileTable의 디렉터리에 대 한 UNC 경로 가져옵니다.  
  
```  
-- returns the relative path of the form “\MyFileTable\MyDocDirectory\document.docx”  
SELECT file_stream.GetFileNamespacePath() AS FilePath FROM DocumentStore  
WHERE Name = N’document.docx’;  
  
-- returns “\\MyServer\MSSQLSERVER\MyDocumentDB\MyFileTable\MyDocDirectory\document.docx”  
SELECT file_stream.GetFileNamespacePath(1, Null) AS FilePath FROM DocumentStore  
WHERE Name = N’document.docx’;  
```  
  
## <a name="see-also"></a>관련 항목:  
 [FileTable에서 디렉터리 및 경로 작업](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md)  
  
  
