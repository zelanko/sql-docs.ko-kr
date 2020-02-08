---
title: FileTable로 파일 로드 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FileTables [SQL Server], migrating files
- FileTables [SQL Server], bulk loading
- FileTables [SQL Server], loading files
ms.assetid: dc842a10-0586-4b0f-9775-5ca0ecc761d9
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: de6e6a237c0aa80e2793f33373ec664dfe93f953
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "72908705"
---
# <a name="load-files-into-filetables"></a>FileTable로 파일 로드
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  파일을 FileTable로 로드 또는 마이그레이션하는 방법에 대해 설명합니다.  
  
##  <a name="BasicsLoadNew"></a> FileTable로 파일 로드 또는 마이그레이션  
 FileTable로 파일을 로드하거나 마이그레이션하기 위해 선택하는 방법은 파일이 현재 저장된 위치에 따라 달라집니다.  
  
|파일의 현재 위치|마이그레이션 옵션|  
|-------------------------------|---------------------------|  
|파일이 현재 파일 시스템에 저장되어 있습니다.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 파일에 대해 알지 못합니다.|FileTable은 Windows 파일 시스템에 폴더로 나타나므로 파일을 이동하거나 복사하는 데 사용할 수 있는 방법으로 파일을 새 FileTable로 쉽게 로드할 수 있습니다. 이러한 방법에는 Windows 탐색기, 명령줄 옵션(xcopy, robocopy 등), 사용자 지정 스크립트나 애플리케이션이 포함됩니다.<br /><br /> 기존 폴더를 FileTable로 변환할 수 없습니다.|  
|파일이 현재 파일 시스템에 저장되어 있습니다.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 파일에 대한 포인터가 포함된 메타데이터의 테이블이 포함되어 있습니다.|첫 번째 단계는 앞에서 설명한 방법 중 하나를 사용하여 파일을 이동하거나 복사하는 것입니다.<br /><br /> 두 번째 단계는 파일의 새 위치를 가리키도록 기존 메타데이터 테이블을 업데이트하는 것입니다.<br /><br /> 자세한 내용은 이 항목의 [예: 파일 시스템에서 FileTable로 파일 마이그레이션](#HowToMigrateFiles)을 참조하세요.|  
  
###  <a name="HowToLoadNew"></a> 방법: FileTable로 파일 로드  
다음 방법을 사용하여 파일을 FileTable로 로드할 수 있습니다.  
  
-   Windows 탐색기에서 원본 폴더의 파일을 새 FileTable 폴더로 끌어 옵니다.  
  
-   명령 프롬프트나 일괄 처리 파일 또는 스크립트에서 MOVE, COPY, XCOPY 또는 ROBOCOPY 등의 명령줄 옵션을 사용합니다.  
  
-   C# 또는 Visual Basic.NET에서 파일을 이동하거나 복사하는 사용자 지정 애플리케이션을 작성합니다. **System.IO** 네임스페이스에서 메서드를 호출합니다.  
  
###  <a name="HowToMigrateFiles"></a> 예제: 파일 시스템에서 FileTable로 파일 마이그레이션  
 이 시나리오에서는 파일이 파일 시스템에 저장되어 있고 파일에 대한 포인터가 포함된 메타데이터의 테이블이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 있다고 가정합니다. 파일을 FileTable로 이동한 다음 메타데이터에 있는 각 파일의 원래 UNC 경로를 FileTable UNC 경로로 바꾸려고 합니다. [GetPathLocator&#40;Transact-SQL&#41;](../../relational-databases/system-functions/getpathlocator-transact-sql.md) 함수를 사용하면 이 목표를 쉽게 달성할 수 있습니다.  
  
 이 예의 경우 사진에 대한 데이터가 들어 있는 **PhotoMetadata**라는 기존 데이터베이스 테이블이 있다고 가정합니다. 이 테이블에는 .jpg 파일의 실제 UNC 경로가 포함되어 있는 **varchar** (512) 형식의 **UNCPath**열이 있습니다.  
  
 파일 시스템의 이미지 파일을 FileTable로 마이그레이션하려면 다음을 수행해야 합니다.  
  
1.  파일을 저장할 새 FileTable을 만듭니다. 이 예에서는 테이블 이름으로 **dbo.PhotoTable**을 사용하지만 테이블을 만드는 코드는 표시되지 않습니다.  
  
2.  xcopy 또는 유사한 도구를 사용하여 .jpg 파일과 해당 디렉터리 구조를 FileTable의 루트 디렉터리에 복사합니다.  
  
3.  다음 예제와 유사한 코드를 사용하여 **PhotoMetadata** 테이블의 메타데이터를 수정합니다.  

```sql  
--  Add a path locator column to the PhotoMetadata table.  
ALTER TABLE PhotoMetadata ADD pathlocator hierarchyid;  
  
-- Get the root path of the Photo directory on the File Server.  
DECLARE @UNCPathRoot varchar(100) = '\\RemoteShare\Photographs';  
  
-- Get the root path of the FileTable.  
DECLARE @FileTableRoot varchar(1000);  
SELECT @FileTableRoot = FileTableRootPath('dbo.PhotoTable');  
  
-- Update the PhotoMetadata table.  
  
-- Replace the File Server UNC path with the FileTable path.  
UPDATE PhotoMetadata  
    SET UNCPath = REPLACE(UNCPath, @UNCPathRoot, @FileTableRoot);  
  
-- Update the pathlocator column to contain the pathlocator IDs from the FileTable.  
UPDATE PhotoMetadata  
    SET pathlocator = GetPathLocator(UNCPath);  
```  
  
##  <a name="BasicsBulkLoad"></a> FileTable로 파일 대량 로드  
 FileTable은 다음과 같은 경우 대량 작업에서 일반 테이블처럼 동작합니다.  
  
 FileTable에 파일 및 디렉터리 네임스페이스의 무결성이 유지되도록 하는 시스템 정의 제약 조건이 있습니다. FileTable로 대량 로드되는 데이터에 대해 이러한 제약 조건을 확인해야 합니다. 일부 대량 삽입 작업에서는 테이블 제약 조건이 무시될 수 있으므로 다음 요구 사항이 적용됩니다.  
  
-   제약 조건이 적용되는 대량 로드 작업은 FileTable에 대해 다른 테이블의 경우와 동일하게 실행할 수 있습니다. 이 범주에는 다음 작업이 포함됩니다.  
  
    -   CHECK_CONSTRAINTS 절을 사용하는 bcp  
  
    -   CHECK_CONSTRAINTS 절을 사용하는 BULK INSERT  
  
    -   INSERT INTO ... IGNORE_CONSTRAINTS 절을 사용하지 않는 SELECT * FROM OPENROWSET(BULK ...)  
  
-   FileTable 시스템 정의 제약 조건을 해제하지 않은 경우 제약 조건을 적용하지 않은 대량 로드 작업은 실패합니다. 이 범주에는 다음 작업이 포함됩니다.  
  
    -   CHECK_CONSTRAINTS 절을 사용하지 않는 bcp  
  
    -   CHECK_CONSTRAINTS 절을 사용하지 않는 BULK INSERT  
  
    -   INSERT INTO ... IGNORE_CONSTRAINTS 절을 사용하는 SELECT * FROM OPENROWSET(BULK ...)  
  
###  <a name="HowToBulkLoad"></a> 방법: FileTable로 파일 대량 로드  
 다음과 같은 다양한 방법을 사용하여 파일을 FileTable로 대량 로드할 수 있습니다.  
  
-   **bcp**  
  
    -   **CHECK_CONSTRAINTS** 절을 사용하여 호출합니다.  
  
    -   FileTable 네임스페이스를 사용하지 않도록 설정하고, **CHECK_CONSTRAINTS** 절을 사용하지 않고 호출합니다. 그런 다음 FileTable 네임스페이스를 다시 사용하도록 설정합니다.  
  
-   **BULK INSERT**  
  
    -   **CHECK_CONSTRAINTS** 절을 사용하여 호출합니다.  
  
    -   FileTable 네임스페이스를 사용하지 않도록 설정하고, **CHECK_CONSTRAINTS** 절을 사용하지 않고 호출합니다. 그런 다음 FileTable 네임스페이스를 다시 사용하도록 설정합니다.  
  
-   **INSERT INTO ... SELECT \* FROM OPENROWSET(BULK ...)**  
  
    -   **IGNORE_CONSTRAINTS** 절을 사용하여 호출합니다.  
  
    -   FileTable 네임스페이스를 사용하지 않도록 설정하고, **IGNORE_CONSTRAINTS** 절을 사용하지 않고 호출합니다. 그런 다음 FileTable 네임스페이스를 다시 사용하도록 설정합니다.  
  
 FileTable 제약 조건을 해제하는 방법은 [FileTables 관리](../../relational-databases/blob/manage-filetables.md)를 참조하세요.  
  
###  <a name="disabling"></a> 방법: 대량 로드에 대한 FileTable 제약 조건 사용 안 함  
 시스템 정의 제약 조건을 적용하는 오버헤드 없이 파일을 FileTable로 대량 로드하려면 제약 조건을 일시적으로 사용하지 않도록 설정할 수 있습니다. 자세한 내용은 [FileTables 관리](../../relational-databases/blob/manage-filetables.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-SQL을 사용하여 FileTable에 액세스](../../relational-databases/blob/access-filetables-with-transact-sql.md)   
 [파일 입/출력 API를 사용하여 FileTable 액세스](../../relational-databases/blob/access-filetables-with-file-input-output-apis.md)  
  
  
