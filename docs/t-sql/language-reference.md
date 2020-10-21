---
description: Transact-SQL 참조(데이터베이스 엔진)
title: Transact-SQL 참조(데이터베이스 엔진) | Microsoft Docs
ms.custom: ''
ms.date: 04/29/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- sql13.tsqlref.f1
- devlang-tsql
helpviewer_keywords:
- Transact-SQL
ms.assetid: dbba47d7-e08e-4435-b876-35dced1f325d
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 422ab559997e5dc33a0d8155c198cb23cba5698b
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/14/2020
ms.locfileid: "92035896"
---
# <a name="transact-sql-reference-database-engine"></a>Transact-SQL 참조(데이터베이스 엔진)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../includes/tsql-appliesto-ss2008-all-md.md)]

이 토픽에서는 Microsoft [!INCLUDE[tsql](../includes/tsql-md.md)](T-SQL) 참조 토픽을 찾고 사용하는 방법에 대한 기본 사항을 제공합니다. T-SQL은 Microsoft SQL 제품 및 서비스를 사용하는데 있어 핵심입니다. SQL 데이터베이스와 통신하는 모든 도구와 애플리케이션은 T-SQL 명령을 보내서 수행합니다.  

## <a name="t-sql-compliance-to-sql-standard"></a>T-SQL의 SQL 표준 준수
[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 특정 표준이 구현된 방식을 설명하는 상세한 기술 문서를 보려면 [Microsoft SQL Server 표준 지원 설명서](/openspecs/sql_standards/ms-sqlstandlp/89fb00b1-4b9e-4296-92ce-a2b3f7ca01d2)를 참조하세요.

## <a name="tools-that-use-t-sql"></a>T-SQL을 사용하는 도구
T-SQL 명령을 실행하는 Microsoft 도구 중 일부는 다음과 같습니다.

- [SSMS(SQL Server Management Studio)](../ssms/download-sql-server-management-studio-ssms.md)
- [SSDT(SQL Server Data Tools)](../ssdt/download-sql-server-data-tools-ssdt.md)
- [sqlcmd](../tools/sqlcmd-utility.md)
- [Azure Data Studio](../azure-data-studio/what-is.md)
  
## <a name="locate-the-transact-sql-reference-topics"></a>Transact-SQL 참조 토픽 찾기  
T-SQL 토픽을 찾으려면 이 페이지의 오른쪽 위에 있는 검색을 사용하거나, 또는 페이지의 왼쪽에 있는 목차를 사용합니다. Management Studio 쿼리 편집기 창에서 T-SQL 키워드를 입력하고 F1 키를 누를 수도 있습니다. 
  
## <a name="find-system-views"></a>시스템 뷰 찾기
시스템 테이블, 뷰, 함수 및 프로시저를 찾으려면 SQL 설명서 섹션의 [관계형 데이터베이스 사용](../relational-databases/databases/databases.md)에 있는 링크를 참조하세요.

- [시스템 카탈로그 뷰](../relational-databases/system-catalog-views/catalog-views-transact-sql.md)
- [시스템 호환성 뷰](../relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)
- [시스템 동적 관리 뷰](../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)
- [시스템 함수](../relational-databases/system-functions/system-functions-category-transact-sql.md)
- [시스템 정보 스키마 뷰](../relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)
- [시스템 저장 프로시저](../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)
- [시스템 테이블](../relational-databases/system-tables/system-tables-transact-sql.md)

## <a name="applies-to-references"></a>'적용 대상' 참조  
 T-SQL 참조 토픽에는 다른 Azure SQL 서비스뿐만 아니라, 2008부터 시작하는 여러 버전의 SQL Server가 포함됩니다.  각 토픽의 위쪽에는 토픽의 제목을 지원하는 제품 및 서비스를 나타내는 섹션이 있습니다. 

예를 들어, 이 토픽은 모든 버전에 적용되며 다음 레이블이 있습니다. 
  
 [!INCLUDE[tsql-appliesto-ss2008-all_md](../includes/tsql-appliesto-ss2008-all-md.md)]   

또 다른 예로, 다음 레이블은 Azure Synapse Analytics 및 병렬 데이터 웨어하우스에만 적용되는 토픽을 나타냅니다.

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw_md](../includes/applies-to-version/asa-pdw.md)]

경우에 따라 토픽이 제품이나 서비스에서 사용되지만 모든 인수는 지원되지 않습니다. 이 경우 추가적인 **적용 대상** 섹션이 토픽 본문의 적절한 인수 설명에 삽입됩니다.  
 
## <a name="get-help-from-microsoft-q--a"></a>Microsoft Q & A에서 도움 받기  
온라인 도움말을 보려면 [Microsoft Q & A Transact-SQL 포럼](/answers/topics/sql-server-transact-sql.html)을 참조하세요.  
 
## <a name="see-other-language-references"></a>다른 언어 참조 보기
SQL 문서에는 이러한 다른 언어 참조가 포함됩니다.
  
- [XQuery 언어 참조](../xquery/xquery-language-reference-sql-server.md)
- [Integration Services 언어 참조](../integration-services/integration-services-language-reference.md)
- [복제 언어 참조](../relational-databases/replication/replication-language-reference.md)
- [Analysis Services 언어 참조](../mdx/multidimensional-expressions-mdx-reference.md)  

## <a name="next-steps"></a>다음 단계
T-SQL 참조 토픽을 찾는 방법을 이해했으므로 다음을 수행할 준비가 되었습니다.

- T-SQL을 작성하는 방법에 대한 간단한 자습서를 통한 작업은 [자습서: Transact-SQL 문 작성](../t-sql/tutorial-writing-transact-sql-statements.md)을 참조하세요. 
- [Transact-SQL 구문 표기 규칙 &#40;Transact-SQL&#41;](../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md) 보기  

  
