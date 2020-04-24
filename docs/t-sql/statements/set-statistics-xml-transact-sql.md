---
title: SET STATISTICS XML(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SET_STATISTICS_XML_TSQL
- SET STATISTICS XML
dev_langs:
- TSQL
helpviewer_keywords:
- statistical information [SQL Server], statement processing
- STATISTICS XML option
- SET STATISTICS XML statement
- statements [SQL Server], statistical information
- XML [SQL Server], statement execution information
ms.assetid: 2b6d4c5a-a7f5-4dd1-b10a-7632265b1af7
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9e06886ec3a66e4860927a9f953c0bee9da2b902
ms.sourcegitcommit: 8ffc23126609b1cbe2f6820f9a823c5850205372
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81634635"
---
# <a name="set-statistics-xml-transact-sql"></a>SET STATISTICS XML(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 실행하고 해당 문이 실행된 방법에 대한 자세한 정보를 잘 정의된 XML 문서 형식으로 생성하도록 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
  
SET STATISTICS XML { ON | OFF }  
```  
  
## <a name="remarks"></a>설명  
 SET STATISTICS XML 옵션은 실행 시 또는 런타임에 설정되며, 구문 분석 시에는 설정되지 않습니다.  
  
 SET STATISTICS XML을 ON으로 설정하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 실행된 각 문에 대한 실행 정보를 반환합니다. 이 옵션을 ON으로 설정하면 다시 OFF로 설정할 때까지 이후의 모든 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문에 대한 정보가 반환됩니다. SET STATISTICS XML이 일괄 처리에서 유일한 문일 필요는 없습니다.  
  
 SET STATISTICS XML은 **sqlcmd** 유틸리티 같은 애플리케이션에 대한 출력을 **nvarchar(max)** 형식으로 반환합니다. 여기서 XML 출력은 이후에 다른 도구가 쿼리 계획 정보를 표시하고 처리하는 데 사용합니다.  
  
 SET STATISTICS XML은 XML 문서 집합으로 정보를 반환합니다. SET STATISTICS XML ON 문 뒤에 오는 각 문은 단일 문서로 출력에 반영됩니다. 각 문서에는 문의 텍스트가 먼저 오고 그 뒤에 실행 단계에 대한 세부 정보가 옵니다. 출력에서는 비용, 액세스한 인덱스, 수행한 연산 유형 같은 런타임 정보, 조인 순서, 물리적 연산이 수행된 횟수, 각 물리 연산자가 생성한 행 수 등을 보여 줍니다.  
  
 SET STATISTICS XML에 의한 XML 출력의 XML 스키마가 포함된 문서는 설치하는 동안 Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 설치되어 있는 컴퓨터의 로컬 디렉터리에 복사됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 파일이 포함된 다음 드라이브에 있습니다.  
  
 \Microsoft SQL Server\100\Tools\Binn\schemas\sqlserver\2004\07\showplan\showplanxml.xsd  
  
 실행 계획 스키마는 [이 웹 사이트](https://go.microsoft.com/fwlink/?linkid=43100&clcid=0x409)에서도 제공합니다.  
  
 SET STATISTICS PROFILE과 SET STATISTICS XML은 서로 유사합니다. 전자는 텍스트 출력을 생성하고 후자는 XML 출력을 생성합니다. 이후 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 새 쿼리 실행 계획 정보가 SET STATISTICS PROFILE 문이 아니라 SET STATISTICS XML 문을 통해서만 표시됩니다.  
  
> [!NOTE]  
>  **에서** 실제 실행 계획 포함[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]을 선택하면 이 SET 옵션에서 XML 실행 계획 출력을 생성하지 않습니다. 이 SET 옵션을 사용하기 전에 **실제 실행 계획 포함** 단추의 선택을 취소하세요.  
  
## <a name="permissions"></a>사용 권한  
 SET STATISTICS XML을 사용하여 출력을 보려면 다음 권한이 있어야 합니다.  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 실행할 수 있는 적절한 권한  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] 문이 참조하는 개체가 포함된 모든 데이터베이스에 대한 SHOWPLAN 권한  
  
 STATISTICS XML 결과 집합을 생성하지 않는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문의 경우 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 실행할 수 있는 적절한 권한만 있으면 됩니다. STATISTICS XML 결과 집합을 생성하는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문의 경우에는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문 실행 권한과 SHOWPLAN 권한이 모두 있어야 합니다. 그렇지 않으면 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문 실행이 중단되고 실행 계획 정보도 생성되지 않습니다.  
  
## <a name="examples"></a>예  
 다음 두 문에서는 SET STATISTICS XML 설정을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 쿼리에서 인덱스 사용을 분석하고 최적화하는 방법을 보여 줍니다. 첫 번째 쿼리에서는 인덱싱된 열의 WHERE 절에 Equals(=) 비교 연산자를 사용합니다. 두 번째 쿼리에서는 WHERE 절에 LIKE 연산자를 사용합니다. 이렇게 하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 클러스터형 인덱스 검색을 사용하여 WHERE 절 조건을 충족하는 데이터를 찾을 수 있습니다. 처음 인덱싱된 쿼리의 경우에는 **EstimateRows** 및 **EstimatedTotalSubtreeCost** 특성의 값이 더 작습니다. 즉, 인덱싱된 쿼리가 인덱싱되지 않은 쿼리에 비해 훨씬 빨리 처리되고 리소스도 더 적게 사용한다는 의미입니다.  
  
```sql
USE AdventureWorks2012;  
GO  
SET STATISTICS XML ON;  
GO  
-- First query.  
SELECT BusinessEntityID   
FROM HumanResources.Employee  
WHERE NationalIDNumber = '509647174';  
GO  
-- Second query.  
SELECT BusinessEntityID, JobTitle   
FROM HumanResources.Employee  
WHERE JobTitle LIKE 'Production%';  
GO  
SET STATISTICS XML OFF;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [SET SHOWPLAN_XML&#40;Transact-SQL&#41;](../../t-sql/statements/set-showplan-xml-transact-sql.md)   
 [sqlcmd 유틸리티](../../tools/sqlcmd-utility.md)  
  
  
