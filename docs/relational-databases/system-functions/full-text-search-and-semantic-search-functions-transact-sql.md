---
title: 전체 텍스트 검색 및 의미 체계 검색 함수 (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- semantic search [SQL Server], system functions
ms.assetid: a61a3694-7604-4583-962e-fc30f771c6fa
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: cdf480d27a0cc0a1b1b646a5c902d7994ad88b5e
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85734368"
---
# <a name="full-text-search-and-semantic-search-functions-transact-sql"></a>전체 텍스트 Search 및 의미 체계 Search 함수(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  이 섹션에서는 전체 텍스트 검색 및 의미 체계 검색과 관련된 시스템 함수에 대해 설명합니다.  
  
## <a name="full-text-search-functions"></a>전체 텍스트 Search 함수  
 [CONTAINSTABLE&#40;Transact-SQL&#41;](../../relational-databases/system-functions/containstable-transact-sql.md)  
 특정 단어나 구와 정확히 일치하거나 비슷하게 일치하는 단어 검색, 서로 근접한 단어 검색 또는 가중치 검색에서 일치하는 항목이 포함된 열에 대해 0개 이상의 행이 있는 테이블을 반환합니다.  
  
 [FREETEXTTABLE&#40;Transact-SQL&#41;](../../relational-databases/system-functions/freetexttable-transact-sql.md)  
 지정 된 *freetext_string*에 있는 텍스트의 정확한 단어 뿐만 아니라 의미와 일치 하는 값을 포함 하는 열에 대해 0 개 이상의 행이 포함 된 테이블을 반환 합니다.  
  
## <a name="semantic-search-functions"></a>의미 체계 Search 함수  
 [semantickeyphrasetable&#40;Transact-SQL&#41;](../../relational-databases/system-functions/semantickeyphrasetable-transact-sql.md)  
 지정된 테이블의 열과 관련된 키 구가 있는 0개 이상의 행으로 구성된 테이블을 반환합니다.  
  
 [semanticsimilaritydetailstable&#40;Transact-SQL&#41;](../../relational-databases/system-functions/semanticsimilaritydetailstable-transact-sql.md)  
 의미상 유사한 내용의 두 문서(원본 문서 및 대응 문서) 간에 공통적인 키 구가 있는 0개 이상의 행으로 구성된 테이블을 반환합니다.  
  
 [semanticsimilaritytable&#40;Transact-SQL&#41;](../../relational-databases/system-functions/semanticsimilaritytable-transact-sql.md)  
 열 내용이 지정된 문서와 의미상 유사한 0개 이상의 행으로 구성된 테이블을 반환합니다.  
  
  
