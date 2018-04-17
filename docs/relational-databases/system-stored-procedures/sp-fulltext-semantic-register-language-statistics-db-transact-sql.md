---
title: sp_fulltext_semantic_register_language_statistics_db (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_fulltext_semantic_register_language_statistics_db
- sp_fulltext_semantic_register_language_statistics_db_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_fulltext_semantic_register_language_statistics_db
ms.assetid: bef1b104-5a44-4327-9ae4-45eae3000f7e
caps.latest.revision: 12
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f6a69f0ed0808e3b90237168e820268e41026581
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="spfulltextsemanticregisterlanguagestatisticsdb-transact-sql"></a>sp_fulltext_semantic_register_language_statistics_db(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 현재 인스턴스에서 미리 채워진 의미 체계 언어 통계 데이터베이스를 등록합니다.  
  
 이 언어 의미 체계 데이터베이스를 연결하고 이 저장 프로시저를 사용하여 등록한 후에만 의미 체계 추출을 시작할 수 있습니다. 이 태스크는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 각 인스턴스에 대해 한 번씩만 수행하면 됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```sql  
EXEC sp_fulltext_semantic_register_language_statistics_db  
    [ @dbname = ] ‘database_name’;  
GO  
```  
  
##  <a name="Arguments"></a> 인수  
 [ @dbname =] '*database_name*'  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 현재 인스턴스에 대해 등록할 의미 체계 언어 통계 데이터베이스의 이름입니다. 데이터베이스가 연결되어 있어야 합니다. *a s e _* 은 **sysname**, NULL이 아닐 수도 있습니다.  
  
## <a name="return-code-value"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-set"></a>결과 집합  
 없음  
  
## <a name="general-remarks"></a>일반적인 주의 사항  
 의미 체계 언어 통계 데이터베이스에는 텍스트 내용의 의미 체계 처리에 필요한 언어 관련 통계가 포함되어 있습니다.  
  
 **sp_fulltext_semantic_register_language_statistics_db** 다음 단계를 수행 합니다.  
  
1.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 의미 체계 처리를 지원하는 버전인지 확인합니다.  
  
2.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 아직 의미 체계 언어 통계 데이터베이스가 정의되어 있지 않은지 확인합니다.  
  
3.  데이터베이스가 올바른 의미 체계 언어 통계 데이터베이스인지 확인합니다.  
  
4.  의미 체계 언어 통계 데이터베이스에 대한 사용 권한을 설정하여 이 데이터베이스에 대한 사용자 액세스를 제한합니다.  
  
5.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대한 의미 체계 언어 통계 데이터베이스의 이름을 정의하는 메타데이터를 삽입합니다.  
  
6.  설치된 의미 체계 언어 통계 의미 데이터베이스와 내부 언어 모델 테이블 간의 매핑을 정의하는 메타데이터를 삽입합니다.  
  
7.  데이터베이스를 사용할 수 있는지 확인합니다.  
  
 자세한 내용은 [의미 체계 검색 설치 및 구성](../../relational-databases/search/install-and-configure-semantic-search.md)을 참조하세요.  
  
## <a name="metadata"></a>메타데이터  
 인스턴스에 설치 된 의미 체계 언어 통계 데이터베이스에 대 한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], 카탈로그 뷰를 쿼리 [sys.fulltext_semantic_language_statistics_database &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-semantic-language-statistics-database-transact-sql.md)합니다.  
  
## <a name="security"></a>보안  
  
### <a name="permissions"></a>Permissions  
 CONTROL SERVER 권한이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예제에서는 호출 하 여 의미 체계 언어 통계 데이터베이스를 등록 하는 방법을 보여 줍니다 **sp_fulltext_semantic_register_language_statistics_db**합니다.  
  
```sql  
EXEC sp_fulltext_semantic_register_language_statistics_db @dbname = 'semanticsDb';  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [의미 체계 검색 설치 및 구성](../../relational-databases/search/install-and-configure-semantic-search.md)  
  
  
