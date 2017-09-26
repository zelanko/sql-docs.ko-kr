---
title: catalog.create_execution_dump | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 91319b0b-5536-4ab4-a403-9559ed9dd177
caps.latest.revision: 12
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: b05e1b46845c0a2b5ee47b94dc239d79d4a12a17
ms.contentlocale: ko-kr
ms.lasthandoff: 09/26/2017

---
# <a name="catalogcreateexecutiondump"></a>catalog.create_execution_dump
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  실행 중인 패키지가 일시 중지하고 덤프 파일을 만들도록 합니다. 파일에 저장 되는 * \<드라이브 >*: files\microsoft SQL Server\130\Shared\ErrorDumps 폴더입니다.  
  
## <a name="syntax"></a>구문  
  
```tsql  
create_execution_dump [ @execution_id = ] execution_id  
  
```  
  
## <a name="arguments"></a>인수  
 [ @execution_id =] *execution_id*  
 실행 중인 패키지의 실행 ID입니다. *execution_id* 은 **bigint**합니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 실행 ID 88인 실행 중인 패키지가 덤프 파일을 만들도록 프롬프트됩니다.  
  
```  
  
EXEC create_execution_dump @execution_id = 88  
  
```  
  
## <a name="return-codes"></a>반환 코드  
 0(성공)  
  
 저장 프로시저가 실패하면 오류를 반환합니다.  
  
## <a name="result-set"></a>결과 집합  
 없음  
  
## <a name="permissions"></a>Permissions  
 이 저장된 프로시저는 사용자의 구성원이 될 필요는 **ssis_admin** 데이터베이스 역할입니다.  
  
## <a name="errors-and-warnings"></a>오류 및 경고  
 다음 목록에서는 저장 프로시저 실패 조건을 설명합니다.  
  
-   지정된 실행 ID가 잘못되었습니다.  
  
-   패키지가 이미 완료되었습니다.  
  
-   패키지가 현재 덤프 파일을 만들고 있습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [패키지 실행을 위한 덤프 파일 생성](../../integration-services/troubleshooting/generating-dump-files-for-package-execution.md)  
  
  
