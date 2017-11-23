---
title: GetPathLocator (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- GetPathLocator
- GetPathLocator_TSQL
dev_langs: TSQL
helpviewer_keywords: GetPathLocator function
ms.assetid: 78b7e220-445b-4fdf-811b-7253f4f2b058
caps.latest.revision: "15"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 30e1f626885e850d8aca6cc30360033c055855f2
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="getpathlocator-transact-sql"></a>GetPathLocator(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  FileTable의 지정된 파일 또는 디렉터리에 대한 경로 로케이터 ID 값을 반환합니다.  
  
||  
|-|  
|**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ~ [현재 버전](http://msdn.microsoft.com/library/bb500435.aspx)).|  
  
## <a name="syntax"></a>구문  
  
```  
  
GetPathLocator(filenamespace_path)  
```  
  
## <a name="arguments"></a>인수  
 *filenamespace_path*  
 FileTable의 네임스페이스 경로입니다. 형식의 네임 스페이스 경로 **nvarchar (max)**합니다.  
  
 데이터베이스는 Always On 가용성 그룹에 속해 있을 때 면 **GetPathLocator** 함수 (VNN) 가상 네트워크 이름 또는 컴퓨터 이름을 허용 합니다.  
  
## <a name="return-type"></a>반환 형식  
 **hierarchyid**  
  
## <a name="general-remarks"></a>일반적인 주의 사항  
 자세한 내용은 [Work with Directories and Paths in FileTables](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md)을 참조하세요.  
  
## <a name="examples"></a>예  
 사용할 수는 **GetPathLocator** 를 FileTable로 파일 서버에서 파일을 마이그레이션하는 경우에 작동 합니다. 이 시나리오에서는 파일을 FileTable로 이동한 다음 각 파일의 원래 UNC 경로를 FileTable UNC 경로로 바꿉니다. 전체 예제를 참조 하십시오. [Filetable로 파일 로드](../../relational-databases/blob/load-files-into-filetables.md)합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [FileTable에서 디렉터리 및 경로 작업](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md)  
  
  
