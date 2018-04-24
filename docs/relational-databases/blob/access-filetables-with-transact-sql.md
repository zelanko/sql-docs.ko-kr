---
title: Transact-SQL을 사용하여 FileTable에 액세스 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: blob
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-blob
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- FileTables [SQL Server], accessing files with T-SQL
ms.assetid: 3c4a5ffb-c521-4696-99cb-2b03cffc9c02
caps.latest.revision: 13
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a959a32dcc25a8d6eaa2a5b84201f535e328f041
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="access-filetables-with-transact-sql"></a>Transact-SQL을 사용하여 FileTable에 액세스
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  FileTable에서 [!INCLUDE[tsql](../../includes/tsql-md.md)] DML(데이터 조작 언어) 명령이 작동하는 방식에 대해 설명합니다.  
  
##  <a name="BasicsInsert"></a> FileTable에 대한 INSERT 작업  
 FileTable에 대해 **INSERT** 작업을 수행할 때는 다음 사항을 고려해야 합니다.  
  
-   모든 파일 특성 열에 NOT NULL 제약 조건이 있습니다. 값을 명시적으로 설정하지 않은 경우 적절한 기본값이 제공됩니다.  
  
-   INSERT 문이 **name**, **path_locator**, **parent_path_locator** 또는 파일 특성을 설정하는 경우 시스템 정의 제약 조건이 적용됩니다.  
  
-   응용 프로그램에서는 [GetPathLocator&#40;Transact-SQL&#41;](../../relational-databases/system-functions/getpathlocator-transact-sql.md) 함수에 파일 시스템 경로를 제공하여 파일 또는 디렉터리에 대한 **path_locator**를 가져올 수 있습니다.  
  
##  <a name="BasicsUpdate"></a> FileTable에 대한 UPDATE 작업  
 FileTable에 대해 **UPDATE** 작업을 수행할 때는 다음 사항을 고려해야 합니다.  
  
-   사용자 정의 데이터를 업데이트할 수 있습니다.  
  
-   INSERT 문이 **name**, **path_locator**, **parent_path_locator**또는 파일 특성을 설정하는 경우 시스템 정의 제약 조건이 적용됩니다.  
  
-   타임스탬프를 포함하여 다른 열에 영향을 주지 않고 **file_stream** 열에서 FILESTREAM 데이터를 업데이트할 수 있습니다.  
  
##  <a name="BasicsDelete"></a> FileTable에 대한 DELETE 작업  
 FileTable에 대해 **DELETE** 작업을 수행할 때는 다음 사항을 고려해야 합니다.  
  
-   행을 삭제하면 해당 파일 또는 디렉터리도 파일 시스템에서 제거됩니다.  
  
-   행이 다른 파일 또는 디렉터리가 포함된 디렉터리에 해당하는 경우 행이 삭제되지 않습니다.  
  
##  <a name="BasicsConstraints"></a> FileTable에 대한 DML 작업에 적용되는 제약 조건  
 시스템 정의 제약 조건은 DML 동작이 파일 네임스페이스 계층의 무결성을 훼손할 수 없도록 보장합니다. 적용되는 제약 조건은 다음과 같습니다.  
  
-   파일 또는 디렉터리의 **이름** 을 설정하거나 변경할 경우:  
  
    -   Windows 파일 및 디렉터리 명명 규칙이 적용됩니다.  
  
    -   부모 디렉터리의 이름 고유성이 적용됩니다.  
  
-   **path_locator** 또는 **parent_path_locator**를 설정하거나 변경하여 파일 또는 디렉터리의 위치를 설정하거나 변경할 경우:  
  
    -   고유성이 적용됩니다.  
  
    -   **path_locator** 및 **parent_path_locator** 값의 일관성을 비롯하여 디렉터리 및 파일의 계층 구조 트리 일관성이 적용됩니다.  
  
-   **file_stream** 열이 null이 아닌 경우 **is_directory** 값을 true로 설정할 수 없습니다. **file_stream** 열의 데이터는 행에 디렉터리가 아닌 파일이 표시됨을 나타냅니다.  
  
-   파일 특성 열은 Null이 될 수 없습니다. NOT NULL 제약 조건은 기본값으로 적용됩니다.  
  
-   **last_access_time** 값은 **last_write_time** 및 **creation_time**보다 이전일 수 없습니다.  
  
## <a name="see-also"></a>참고 항목  
 [FileTable로 파일 로드](../../relational-databases/blob/load-files-into-filetables.md)   
 [FileTable에서 디렉터리 및 경로 작업](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md)   
 [파일 입/출력 API를 사용하여 FileTable 액세스](../../relational-databases/blob/access-filetables-with-file-input-output-apis.md)   
 [FileTable DDL, 함수, 저장 프로시저 및 뷰](../../relational-databases/blob/filetable-ddl-functions-stored-procedures-and-views.md)  
  
  
