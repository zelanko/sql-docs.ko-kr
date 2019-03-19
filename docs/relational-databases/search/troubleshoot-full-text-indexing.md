---
title: 전체 텍스트 인덱싱 문제 해결 | Microsoft 문서
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: search, sql-database
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- indexes [full-text search]
- troubleshooting [SQL Server], full-text search
- troubleshooting [full-text search]
ms.assetid: 964c43a8-5019-4179-82aa-63cd0ef592ef
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e408699252c30478036dc74a9ffe3a20e1e97c77
ms.sourcegitcommit: 03870f0577abde3113e0e9916cd82590f78a377c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/18/2019
ms.locfileid: "57973467"
---
# <a name="troubleshoot-full-text-indexing"></a>전체 텍스트 인덱싱 문제 해결
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
     
##  <a name="failure"></a> 전체 텍스트 인덱싱 오류 문제 해결  
 전체 텍스트 인덱스를 채우거나 유지 관리하는 동안 전체 텍스트 인덱서는 아래에서 설명하는 이유로 인해 하나 이상의 행을 인덱싱하지 못할 수 있습니다. 이러한 행 수준 오류가 발생해도 채우기는 완료됩니다. 그러나 인덱서가 이러한 행을 건너뛰므로 이러한 행에 포함된 내용은 쿼리할 수 없습니다.  
  
 인덱싱 오류는 다음과 같은 경우에 발생할 수 있습니다.  
  
-   인덱서가 필터 또는 단어 분리기 구성 요소를 찾거나 로드할 수 없습니다. 이 오류는 테이블 행에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 등록되지 않은 언어로 된 문서 내용이나 문서 형식이 포함되어 있는 경우 발생할 수 있습니다. 등록된 단어 분리기 또는 필터 구성 요소에 서명하지 않았거나 로드 시 서명 확인에 실패하는 경우에도 이 오류가 발생할 수 있습니다.  
  
-   단어 분리기 또는 필터와 같은 구성 요소가 실패하거나 인덱서에 오류를 반환합니다. 이 오류는 인덱싱 중인 문서가 손상되어 필터가 문서에서 텍스트를 추출할 수 없는 경우 발생할 수 있습니다. 전체 텍스트 필터 데몬 호스트(fdhost.exe)의 메모리 제한으로 인해 구성 요소가 특정 크기를 초과하는 단일 행의 내용을 처리할 수 없는 경우에도 이 오류가 발생할 수 있습니다.  
  
 각 행 수준 오류의 경우 탐색 로그를 통해 오류 원인에 대한 자세한 내용을 볼 수 있습니다. 오류 수는 전체 또는 증분 채우기 완료 시 요약 표시됩니다.  
  
 인덱싱 프로세스 자체에 영향을 주어 채우기를 완료할 수 없는 오류도 있습니다.  
  
-   전체 텍스트 인덱스가 전체 텍스트 카탈로그에 포함될 수 있는 행 수에 대한 제한을 초과합니다.  
  
-   인덱싱 중인 테이블에 있는 클러스터형 인덱스 또는 전체 텍스트 키 인덱스가 변경, 삭제 또는 다시 작성되었습니다.  
  
-   하드웨어 오류 또는 디스크 손상으로 인해 전체 텍스트 카탈로그가 손상되었습니다.  
  
-   전체 텍스트 인덱싱 중인 테이블을 포함하는 파일 그룹이 오프라인 상태가 되거나 읽기 전용으로 설정되었습니다.  
  
 중요한 전체 텍스트 인덱스 채우기 작업을 완료한 다음이나 채우기가 완료되지 않은 경우 탐색 로그를 검사합니다.  
  
### <a name="unsigned-components"></a>서명되지 않은 구성 요소  
 기본적으로 전체 텍스트 인덱서를 사용하려면 로드하는 필터 및 단어 분리기에 서명해야 합니다. 일부 사용자 지정 구성 요소 설치 시에서와 같이 구성 요소를 서명하지 않는 경우에는 전체 텍스트 인덱서가 서명 확인을 무시하도록 구성해야 합니다.  
  
> [!IMPORTANT]  
>  서명 확인을 무시하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 보안 수준이 낮아집니다. 구현하는 모든 구성 요소에 서명하거나 가져오는 모든 구성 요소에 서명이 되어 있는지 확인하는 것이 좋습니다. 구성 요소에 서명하는 방법은 [sp_fulltext_service&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql.md)를 참조하세요.  
  
  
##  <a name="state"></a> 트랜잭션 로그가 복원된 후 일관성 없는 상태의 전체 텍스트 인덱스  
 데이터베이스의 트랜잭션 로그를 복원할 때 전체 텍스트 인덱스에 일관성이 없다는 경고가 표시될 수 있습니다. 이는 데이터베이스가 백업된 후 테이블에 대한 전체 텍스트 인덱스가 수정되었기 때문입니다. 전체 텍스트 인덱스를 일관성 있게 구성하려면 해당 테이블에 대해 전체 채우기(탐색)를 실행해야 합니다. 자세한 내용은 [전체 텍스트 인덱스 채우기](../../relational-databases/search/populate-full-text-indexes.md)를 참조하세요.  
  
  
## <a name="see-also"></a>참고 항목  
 [ALTER FULLTEXT CATALOG&#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-catalog-transact-sql.md)   
 [전체 텍스트 인덱스 채우기](../../relational-databases/search/populate-full-text-indexes.md)  
  
  
