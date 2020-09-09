---
description: sp_browsemergesnapshotfolder(Transact-SQL)
title: sp_browsemergesnapshotfolder (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_browsemergesnapshotfolder
- sp_browsemergesnapshotfolder_TSQL
helpviewer_keywords:
- sp_browsemergesnapshotfolder
ms.assetid: e248642f-5fea-4ed7-be1a-36ff75abcfde
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 0fa33826f8a046e4d60447700c4e9d31aaa4d47f
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89541957"
---
# <a name="sp_browsemergesnapshotfolder-transact-sql"></a>sp_browsemergesnapshotfolder(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  병합 게시에 대해 가장 최근에 생성된 스냅샷의 전체 경로를 반환합니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_browsemergesnapshotfolder [@publication= ] 'publication'  
```  
  
## <a name="arguments"></a>인수  
`[ @publication = ] 'publication'` 게시의 이름입니다. *게시* 는 **sysname**이며 기본값은 없습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**snapshot_folder**|**nvarchar (2000)**|스냅샷 디렉터리의 전체 경로입니다.|  
  
## <a name="remarks"></a>설명  
 **sp_browsemergesnapshotfolder** 는 병합 복제에 사용 됩니다.  
  
 게시가 게시자 작업 디렉터리 및 게시자 스냅샷 폴더 모두에서 스냅샷 파일을 생성하도록 설정되면 결과 집합은 두 행을 포함하게 됩니다. 첫 번째 행은 게시 스냅샷 폴더를 포함하며 두 번째 행은 게시자 작업 디렉터리를 포함합니다.  
  
 **sp_browsemergesnapshotfolder** 는 병합 스냅숏 파일이 생성 되는 디렉터리를 결정 하는 데 유용 합니다. 이 폴더/경로 및 그 내용은 이동식 미디어에 복사될 수 있고 스냅샷은 대체 스냅샷 위치에서 구독을 동기화하는 데 사용될 수 있습니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할 또는 **db_owner** 고정 데이터베이스 역할의 멤버만 **sp_browsemergesnapshotfolder**을 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
