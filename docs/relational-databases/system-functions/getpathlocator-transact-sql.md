---
description: GetPathLocator(Transact-SQL)
title: GetPathLocator (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- GetPathLocator
- GetPathLocator_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- GetPathLocator function
ms.assetid: 78b7e220-445b-4fdf-811b-7253f4f2b058
author: rothja
ms.author: jroth
ms.openlocfilehash: 2551dfbb7d71b33542f4bc6fd8087c10f974e45b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88464766"
---
# <a name="getpathlocator-transact-sql"></a>GetPathLocator(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  FileTable의 지정된 파일 또는 디렉터리에 대한 경로 로케이터 ID 값을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
GetPathLocator(filenamespace_path)  
```  
  
## <a name="arguments"></a>인수  
 *filenamespace_path*  
 FileTable의 네임스페이스 경로입니다. 네임 스페이스 경로는 **nvarchar (max)** 형식입니다.  
  
 데이터베이스가 Always On 가용성 그룹에 속하는 경우 **Getpathlocator** 함수는 vnn (가상 네트워크 이름) 또는 컴퓨터 이름을 허용 합니다.  
  
## <a name="return-type"></a>반환 형식  
 **hierarchyid**  
  
## <a name="general-remarks"></a>일반적인 주의 사항  
 자세한 내용은 [Work with Directories and Paths in FileTables](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md)을 참조하세요.  
  
## <a name="examples"></a>예제  
 파일 서버에서 FileTable로 파일을 마이그레이션할 때 **Getpathlocator** 함수를 사용할 수 있습니다. 이 시나리오에서는 파일을 FileTable로 이동한 다음 각 파일의 원래 UNC 경로를 FileTable UNC 경로로 바꿉니다. 전체 예제를 보려면 [filetable에 파일 로드](../../relational-databases/blob/load-files-into-filetables.md)를 참조 하세요.  
  
## <a name="see-also"></a>참고 항목  
 [FileTable에서 디렉터리 및 경로 작업](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md)  
  
  
