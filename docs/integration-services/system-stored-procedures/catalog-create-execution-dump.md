---
description: catalog.create_execution_dump
title: catalog.create_execution_dump | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 91319b0b-5536-4ab4-a403-9559ed9dd177
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 4c640ea3f78aa6e518b8f6d0250fbc288b40cd02
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88456964"
---
# <a name="catalogcreate_execution_dump"></a>catalog.create_execution_dump 

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  실행 중인 패키지가 일시 중지하고 덤프 파일을 만들도록 합니다. 덤프 파일은 *\<drive>* :\Program Files\Microsoft SQL Server\130\Shared\ErrorDumps 폴더에 저장됩니다.  
  
## <a name="syntax"></a>구문  
  
```sql  
catalog.create_execution_dump [ @execution_id = ] execution_id  
  
```  
  
## <a name="arguments"></a>인수  
 [ @execution_id = ] *execution_id*  
 실행 중인 패키지의 실행 ID입니다. *execution_id*는 **bigint**입니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 실행 ID 88인 실행 중인 패키지가 덤프 파일을 만들도록 프롬프트됩니다.  
  
```sql
EXEC create_execution_dump @execution_id = 88  
```  
  
## <a name="return-codes"></a>반환 코드  
 0(성공)  
  
 저장 프로시저가 실패하면 오류를 반환합니다.  
  
## <a name="result-set"></a>결과 집합  
 None  
  
## <a name="permissions"></a>사용 권한  
 이 저장 프로시저 사용자는 **ssis_admin** 데이터베이스 역할의 멤버여야 합니다.  
  
## <a name="errors-and-warnings"></a>오류 및 경고  
 다음 목록에서는 저장 프로시저 실패 조건을 설명합니다.  
  
-   지정된 실행 ID가 잘못되었습니다.  
  
-   패키지가 이미 완료되었습니다.  
  
-   패키지가 현재 덤프 파일을 만들고 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [패키지 실행을 위한 덤프 파일 생성](../../integration-services/troubleshooting/generating-dump-files-for-package-execution.md)  
  
  
