---
title: FileTable 만들기, 변경 및 삭제 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: blob
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-blob
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- FileTables [SQL Server], altering
- FileTables [SQL Server], dropping
- FileTables [SQL Server], creating
ms.assetid: 47d69e37-8778-4630-809b-2261b5c41c2c
caps.latest.revision: 25
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ba8ada2a67db9c0f6ea4882fb6fd04b26caa4f9f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32923618"
---
# <a name="create-alter-and-drop-filetables"></a>FileTable 만들기, 변경 및 삭제
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  새 FileTable을 만들거나 기존 FileTable을 변경 또는 삭제하는 방법에 대해 설명합니다.  
  
##  <a name="BasicsCreate"></a> FileTable 만들기  
 FileTable은 미리 정의된 고정 스키마가 있는 특수한 사용자 테이블입니다. 이 스키마는 FILESTREAM 데이터, 파일/디렉터리 정보 및 파일 특성을 저장합니다. FileTable 스키마에 대한 자세한 내용은 [FileTable Schema](../../relational-databases/blob/filetable-schema.md)를 참조하세요.  
  
 Transact-SQL 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 사용하여 새 FileTable을 만들 수 있습니다. FileTable에는 고정 스키마가 있으므로 열 목록을 지정할 필요가 없습니다. FileTable을 만드는 간단한 구문에서 다음을 지정할 수 있습니다.  
  
-   디렉터리 이름. FileTable 폴더 계층 구조에서 이 테이블 수준 디렉터리는 데이터베이스 수준에서 지정된 데이터베이스 디렉터리의 자식이 되고 테이블에 저장된 파일 또는 디렉터리의 부모가 됩니다.  
  
-   FileTable의 **Name** 열에 있는 파일 이름에 사용할 데이터 정렬의 이름  
  
-   자동으로 만들어지는 UNIQUE 제약 조건 및 세 가지 기본 키에 사용할 이름  
  
###  <a name="HowToCreate"></a> 방법: FileTable 만들기  
 **Transact-SQL을 사용하여 FileTable 만들기**  
 **AS FileTable** 옵션이 포함된 [CREATE TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md) 문을 호출하여 FileTable을 만듭니다. FileTable에는 고정 스키마가 있으므로 열 목록을 지정할 필요가 없습니다. 새 FileTable에 대해 다음 설정을 지정할 수 있습니다.  
  
1.  **FILETABLE_DIRECTORY**. FileTable에 저장된 모든 파일 및 디렉터리에 대한 루트 디렉터리 역할을 하는 디렉터리를 지정합니다. 이 이름은 데이터베이스의 모든 FileTable 디렉터리 이름 중에서 고유해야 합니다. 고유성 비교는 현재 데이터 정렬 설정과 관계없이 대/소문자를 구분하지 않습니다.  
  
    -   이 값의 데이터 형식은 **nvarchar(255)** 이며 **Latin1_General_CI_AS_KS_WS**의 고정된 데이터 정렬을 사용합니다.  
  
    -   제공하는 디렉터리 이름은 올바른 디렉터리 이름에 대한 파일 시스템 요구 사항을 따라야 합니다.  
  
    -   이 이름은 데이터베이스의 모든 FileTable 디렉터리 이름 중에서 고유해야 합니다. 고유성 비교는 현재 데이터 정렬 설정과 관계없이 대/소문자를 구분하지 않습니다.  
  
    -   FileTable 만들 때 디렉터리 이름을 제공하지 않은 경우 FileTable의 이름이 디렉터리 이름으로 사용됩니다.  
  
2.  **FILETABLE_COLLATE_FILENAME**. FileTable의 **Name** 열에 적용할 데이터 정렬의 이름을 지정합니다.  
  
    1.  지정한 데이터 정렬은 Windows 파일 이름 의미 체계를 따르도록 **대/소문자를 구분하지 않아야** 합니다.  
  
    2.  **FILETABLE_COLLATE_FILENAME**값을 제공하지 않거나 **database_default**를 지정한 경우 열은 현재 데이터베이스의 데이터 정렬을 상속합니다. 현재 데이터베이스 데이터 정렬이 대/소문자를 구분하면 오류가 발생하고 **CREATE TABLE** 작업이 실패합니다.  
  
3.  자동으로 만들어지는 UNIQUE 제약 조건 및 세 가지 기본 키에 사용할 이름도 지정할 수 있습니다. 이름을 입력하지 않으면 시스템이 이 항목의 뒷부분에 나와 있는 이름을 생성합니다.  
  
    -   **FILETABLE_PRIMARY_KEY_CONSTRAINT_NAME**  
  
    -   **FILETABLE_STREAMID_UNIQUE_CONSTRAINT_NAME**  
  
    -   **FILETABLE_FULLPATH_UNIQUE_CONSTRAINT_NAME**  
  
 **예**  
  
 다음 예제에서는 새 FileTable을 만들고 **FILETABLE_DIRECTORY** 및 **FILETABLE_COLLATE_FILENAME**둘 다에 대해 사용자 정의 값을 지정합니다.  
  
```sql  
CREATE TABLE DocumentStore AS FileTable  
    WITH (   
          FileTable_Directory = 'DocumentTable',  
          FileTable_Collate_Filename = database_default  
         );  
GO  
```  
  
 또한 다음 예에서는 새로운 Filetable을 만듭니다. 사용자 정의 값이 지원되지 않기 때문에 **FILETABLE_DIRECTORY** 값은 FileTable 값이 되고, **FILETABLE_COLLATE_FILENAME** 값은 database_default가 되며, 기본 키 및 UNIQUE 제약 조건에는 시스템에서 생성한 이름이 지정됩니다.  
  
```sql  
CREATE TABLE DocumentStore AS FileTable;  
GO  
```  
  
 **SQL Server Management Studio를 사용하여 FileTable 만들기**  
 개체 탐색기에서 선택한 데이터베이스의 개체를 확장하고 **테이블** 폴더에서 마우스 오른쪽 단추를 클릭한 다음 **새 FileTable**을 선택합니다.  
  
 이 옵션은 Transact-SQL 스크립트 템플릿이 포함된 새 스크립트 창을 엽니다. 이 템플릿을 사용자 지정하여 FileTable을 만드는 데 사용할 수 있습니다. **쿼리** 메뉴에서 **템플릿 매개 변수 값 지정** 옵션을 사용하여 스크립트를 쉽게 사용자 지정할 수 있습니다.  
  
###  <a name="ReqCreate"></a> FileTable 만들기에 대한 요구 사항 및 제한 사항  
  
-   기존 테이블을 변경하여 FileTable로 변환할 수 없습니다.  
  
-   데이터베이스 수준에서 이전에 지정된 디렉터리에 null이 아닌 값이 있어야 합니다. 데이터베이스 수준 디렉터리를 지정하는 방법에 대한 자세한 내용은 [FileTable의 필수 구성 요소를 사용하도록 설정](../../relational-databases/blob/enable-the-prerequisites-for-filetable.md)을 참조하세요.  
  
-   FileTable에는 FILESTREAM 열이 포함되어 있으므로 FileTable에는 유효한 FILESTREAM 파일 그룹이 있어야 합니다. 필요에 따라 **CREATE TABLE** 명령의 일부로 유효한 FILESTREAM 파일 그룹을 지정하여 FileTable을 만들 수 있습니다. 파일 그룹을 지정하지 않으면 FileTable에는 데이터베이스의 기본 FILESTREAM 파일 그룹이 사용됩니다. 데이터베이스에 FILESTREAM 파일 그룹이 없으면 오류가 발생합니다.  
  
-   **TABLE…AS FILETABLE CREATE** 문의 일부로 테이블 제약 조건을 만들 수 없습니다. 그러나 **ALTER TABLE** 문을 사용하여 나중에 제약 조건을 추가할 수 있습니다.  
  
-   **tempdb** 데이터베이스나 다른 시스템 데이터베이스에는 FileTable을 만들 수 없습니다.  
  
-   FileTable을 임시 테이블로 만들 수 없습니다.  
  
##  <a name="BasicsAlter"></a> FileTable 변경  
 FileTable에는 미리 정의된 고정 스키마가 있으므로 해당 열을 추가하거나 변경할 수 없습니다. 그러나 FileTable에 사용자 지정 인덱스, 트리거, 제약 조건 및 다른 옵션을 추가할 수 있습니다.  
  
 시스템 정의 제약 조건을 포함하여 ALTER TABLE 문을 사용하여 FileTable 네임스페이스를 사용하거나 사용하지 않도록 설정하는 방법은 [FileTable 관리](../../relational-databases/blob/manage-filetables.md)를 참조하세요.  
  
###  <a name="HowToChange"></a> 방법: FileTable의 디렉터리 변경  
 **Transact-SQL을 사용하여 FileTable의 디렉터리 변경**  
 ALTER TABLE 문을 호출하고 **FILETABLE_DIRECTORY** SET 옵션에 유효한 새 값을 제공합니다.  
  
 **예제**  
  
```sql  
ALTER TABLE filetable_name  
    SET ( FILETABLE_DIRECTORY = N'directory_name' );  
GO  
```  
  
 **SQL Server Management Studio를 사용하여 FileTable의 디렉터리 변경**  
 개체 탐색기에서 FileTable을 마우스 오른쪽 단추로 클릭하고 **속성** 을 선택하여 **테이블 속성** 대화 상자를 엽니다. **FileTable** 페이지에서 **FileTable 디렉터리 이름**의 새 값을 입력합니다.  
  
###  <a name="ReqAlter"></a> FileTable 변경에 대한 요구 사항 및 제한 사항  
  
-   **FILETABLE_COLLATE_FILENAME**값은 변경할 수 없습니다.  
  
-   FileTable의 시스템 정의 열은 변경, 삭제하거나 사용하지 않도록 설정할 수 없습니다.  
  
-   FileTable에 새 사용자 열, 계산 열 또는 지속형 계산 열을 추가할 수 없습니다.  
  
##  <a name="BasicsDrop"></a> FileTable 삭제  
 [DROP TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/drop-table-transact-sql.md) 문의 일반 구문을 사용하여 FileTable을 삭제할 수 있습니다.  
  
 Filetable를 삭제하면 다음 개체도 삭제됩니다.  
  
-   FileTable의 모든 열과 테이블에 연결된 모든 개체(예: 인덱스, 제약 조건 및 트리거)도 삭제됩니다.  
  
-   포함된 FileTable 디렉터리 및 하위 디렉터리가 데이터베이스의 FILESTREAM 파일 및 디렉터리 계층 구조에서 사라집니다.  
  
 FileTable의 파일 네임스페이스에 열려 있는 파일 핸들이 있는 경우 DROP TABLE 명령이 실패합니다. 열려 있는 핸들을 닫는 방법에 대한 자세한 내용은 [FileTable 관리](../../relational-databases/blob/manage-filetables.md)를 참조하세요.  
  
##  <a name="BasicsOtherObjects"></a> FileTable을 만들 때 생성되는 다른 데이터베이스 개체  
 새 FileTable을 만들면 일부 시스템 정의 인덱스 및 제약 조건도 만들어집니다. 이러한 개체는 변경하거나 삭제할 수 없으며, FileTable 자체가 삭제된 경우에만 사라집니다. 이러한 개체의 목록을 보려면 카탈로그 뷰 [sys.filetable_system_defined_objects&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-filetable-system-defined-objects-transact-sql.md)를 쿼리합니다.  
  
```sql  
--View all objects for all filetables, unsorted  
SELECT * FROM sys.filetable_system_defined_objects;  
GO  
  
--View sorted list with friendly names  
SELECT OBJECT_NAME(parent_object_id) AS 'FileTable', OBJECT_NAME(object_id) AS 'System-defined Object'  
    FROM sys.filetable_system_defined_objects  
    ORDER BY FileTable, 'System-defined Object';  
GO  
```  
  
 **새 FileTable을 만들 때 생성되는 인덱스**  
 새 FileTable을 만들면 다음과 같은 시스템 정의 인덱스도 만들어집니다.  
  
|||  
|-|-|  
|**열**|**인덱스 유형**|  
|[path_locator] ASC|기본 키, 비클러스터형|  
|[parent_path_locator] ASC,<br /><br /> [name] ASC|고유, 비클러스터형|  
|[stream_id] ASC|고유, 비클러스터형|  
  
 **새 FileTable을 만들 때 생성되는 제약 조건**  
 새 FileTable을 만들면 다음과 같은 시스템 정의 제약 조건도 만들어집니다.  
  
|제약 조건|적용|  
|-----------------|--------------|  
|다음 열에 대한 기본 제약 조건:<br /><br /> creation_time<br /><br /> is_archive<br /><br /> is_directory<br /><br /> is_hidden<br /><br /> is_offline<br /><br /> is_readonly<br /><br /> is_system<br /><br /> is_temporary<br /><br /> last_access_time<br /><br /> last_write_time<br /><br /> path_locator<br /><br /> stream_id|시스템 정의 기본 제약 조건이 지정된 열에 기본값을 적용합니다.|  
|CHECK 제약 조건|시스템 정의 CHECK 제약 조건이 다음 요구 사항을 적용합니다.<br /><br /> 유효한 파일 이름<br /><br /> 유효한 파일 특성<br /><br /> 부모 개체는 디렉터리여야 합니다.<br /><br /> 파일 조작 중에는 네임스페이스 계층 구조가 잠깁니다.|  
  
 **시스템 정의 제약 조건에 대한 명명 규칙**  
 위에서 설명한 시스템 정의 제약 조건은 **\<constraintType>_\<tablename>[\_\<columnname>]\_\<uniquifier>** 형식입니다. 여기서 각 항목은 다음을 나타냅니다.  
  
-   *<constraint_type>* 은 CK(확인 제약 조건), DF(기본 제약 조건), FK(외래 키), PK(기본 키) 또는 UQ(고유 제약 조건)입니다.  
  
-   *\<uniquifier>* 는 이름을 고유하게 만드는 시스템 생성 문자열입니다. 이 문자열은 FileTable 이름 및 고유 식별자를 포함할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [FileTable 관리](../../relational-databases/blob/manage-filetables.md)  
  
  
