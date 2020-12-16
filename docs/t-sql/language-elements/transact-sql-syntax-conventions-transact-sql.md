---
description: Transact-SQL 구문 표기 규칙(Transact-SQL)
title: Transact-SQL 구문 규칙(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- sql13.TSQLExpandPortal.f1
dev_langs:
- TSQL
helpviewer_keywords:
- conventions [SQL Server]
- Applies to section in Transact-SQL topics
- code example conventions [SQL Server]
- objects [SQL Server], names
- code [SQL Server], conventions
- multipart names [SQL Server]
- Transact-SQL syntax conventions
- syntax conventions [SQL Server]
- code [SQL Server]
- Transact-SQL
- naming conventions [SQL Server]
- syntax [SQL Server], Transact-SQL
ms.assetid: 35fbcf7f-8b55-46cd-a957-9b8c7b311241
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: cea868a3023b8b69ef69384f03983183d869531b
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97464254"
---
# <a name="transact-sql-syntax-conventions-transact-sql"></a>Transact-SQL 구문 표기 규칙(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

다음 표에서는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 참조의 구문 다이어그램에 사용되는 규칙을 나열하고 설명합니다.  
  
|규칙|사용 대상|  
|----------------|--------------|  
|대문자|[!INCLUDE[tsql](../../includes/tsql-md.md)] 키워드입니다.|  
|_기울임꼴_|사용자가 제공하는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 구문 매개 변수입니다.|  
|**굵게**|데이터베이스 이름, 테이블 이름, 열 이름, 인덱스 이름, 저장 프로시저, 유틸리티, 데이터 형식 이름 및 텍스트를 표시된 대로 정확히 입력합니다.|  
|밑줄|밑줄 친 값이 포함된 절이 문에 지정되지 않을 때 적용되는 기본값을 나타냅니다.|  
|&#124; (세로줄)|대괄호 또는 중괄호 내에서 구문 항목을 구분합니다. 항목 중 하나만 사용할 수 있습니다.|  
|`[ ]`(대괄호)|선택적 구문 항목입니다. 대괄호는 입력하지 않습니다.|  
|{}(중괄호)|필수 구문 항목입니다. 중괄호는 입력하지 않습니다.|  
|[ **,** ..._n_]|앞의 항목이 _n_ 번 반복될 수 있음을 나타냅니다. 각 항목은 쉼표로 구분됩니다.|  
|[..._n_]|앞의 항목이 _n_ 번 반복될 수 있음을 나타냅니다. 각 항목은 공백으로 구분됩니다.|  
|;|[!INCLUDE[tsql](../../includes/tsql-md.md)] 문 종결자입니다. 이 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 대부분의 문에 세미콜론이 필요하지 않지만 이후 버전에서는 필요합니다.|  
|\<label> ::=|구문 블록의 이름입니다. 이 규칙을 사용하여 문에서 한 곳 이상 사용할 수 있는 긴 구문의 섹션 또는 구문 단위를 그룹화하고 레이블을 지정합니다. 구문 블록이 사용될 수 있는 각 위치는 갈매기 기호로 묶인 레이블(\<label>)로 표시됩니다.<br /><br /> 집합은 식 모음(예: \<grouping set>)이고, 목록은 집합 모음(예: \<composite element list>)입니다.|  
  
## <a name="multipart-names"></a>다중 부분 이름  
다른 지침이 없으면 데이터베이스 개체 이름에 대한 모든 [!INCLUDE[tsql](../../includes/tsql-md.md)] 참조는 다음 형식과 같이 네 부분으로 된 이름으로 구성됩니다.  
  
_server\_name_.[_database\_name_].[_schema\_name_]._object\_name_  
  
| _database\_name_.[_schema\_name_]._object\_name_  
 
| _schema\_name_._object\_name_  
  
| _object\_name_  
  
_server\_name_  
연결된 서버 이름 또는 원격 서버 이름을 지정합니다.  
  
_database\_name_  
개체가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 로컬 인스턴스에 있을 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스의 이름을 지정합니다. 개체가 연결된 서버에 있으면 *database_name* 은 OLE DB 카탈로그를 지정합니다.  
  
_schema\_name_  
개체가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 있을 경우 해당 개체가 포함된 스키마의 이름을 지정합니다. 개체가 연결된 서버에 있으면 *schema_name* 은 OLE DB 스키마 이름을 지정합니다.  
  
_object\_name_  
개체의 이름을 참조합니다.  
  
특정 개체를 참조할 때 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]에서 개체를 식별하기 위해 항상 서버, 데이터베이스 및 스키마를 지정할 필요는 없습니다. 그러나 개체를 찾을 수 없으면 오류가 반환됩니다.  
  
> [!NOTE]  
> 이름 확인 오류를 방지하기 위해서는 스키마 범위 개체를 지정할 때 항상 스키마를 지정하는 것이 좋습니다.  
  
중간 노드를 생략하려면 마침표를 사용해 이 위치를 표시하십시오. 다음 표에서는 개체 이름의 유효한 형식을 보여 줍니다.  
  
|개체 참조 형식|Description|  
|-----------------------------|-----------------|  
|_server_._database_._schema_._object_|네 부분으로 이루어진 이름입니다.|  
|_server_._database_.._object_|스키마 이름이 생략됩니다.|  
|_server_.._schema_._object_|데이터베이스 이름이 생략됩니다.|  
|_server_..._object_|데이터베이스 및 스키마 이름이 생략됩니다.|  
|_database_._schema_._object_|서버 이름이 생략됩니다.|  
|_database_.._object_|서버 및 스키마 이름이 생략됩니다.|  
|_schema_._object_|서버 및 데이터베이스 이름이 생략됩니다.|  
|_object_|서버, 데이터베이스 및 스키마 이름이 생략됩니다.|  
  
## <a name="code-example-conventions"></a>코드 예 표기 규칙  
특별한 언급이 없으면 [!INCLUDE[tsql](../../includes/tsql-md.md)] 참조에서 제공되는 예는 다음 옵션에 대해 기본 설정을 사용하여 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 테스트되었습니다.  
  
-   ANSI_NULLS  
-   ANSI_NULL_DFLT_ON  
-   ANSI_PADDING  
-   ANSI_WARNINGS  
-   CONCAT_NULL_YIELDS_NULL  
-   QUOTED_IDENTIFIER  
  
[!INCLUDE[tsql](../../includes/tsql-md.md)] 참조에 있는 대부분의 코드 예는 정렬 시 대/소문자를 구분하는 서버에서 테스트되었으며 일반적으로 테스트 서버에서는 ANSI/ISO 1252 코드 페이지가 실행됩니다.  
  
많은 코드 예제에서 유니코드 문자열 상수 앞에 문자 **N** 을 접두사로 붙입니다. **N** 접두사가 없으면 문자열이 데이터베이스의 기본 코드 페이지로 변환됩니다. 이 기본 코드 페이지는 일부 문자를 인식하지 않을 수 있습니다.  
  
## <a name="applies-to-references"></a>'적용 대상' 참조  
[!INCLUDE[tsql](../../includes/tsql-md.md)] 참조에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상), [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 및 [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 관련 항목이 포함되어 있습니다.   

각 문서의 위쪽에는 문서의 주제를 지원하는 제품을 나타내는 섹션이 있습니다. 제품이 생략되면 문서에서 설명하는 기능을 해당 제품에서 사용할 수 없습니다. 예를 들어 가용성 그룹이 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]에서 도입되었습니다. **CREATE AVAILABILITY GROUP** 문서는 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 또는 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]에 적용되지 않으므로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상)에 적용됨을 나타냅니다.  
  
문서의 일반적인 주제를 제품에서 사용할 수 있지만 경우에 따라 일부 인수가 지원되지 않습니다. 예를 들어 포함된 데이터베이스 사용자가 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]에서 도입되었습니다. 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 제품에서 **CREATE USER** 문을 사용할 수 있지만, **WITH PASSWORD** 구문은 이전 버전에서 사용할 수 없습니다. 추가적인 **적용 대상** 섹션이 항목 본문의 적절한 인수 설명에 삽입됩니다.  
  
## <a name="see-also"></a>참고 항목  
[Transact-SQL 참조 &#40;데이터베이스 엔진&#41;](../language-reference.md)    
[예약 키워드 &#40;Transact SQL&#41;](../../t-sql/language-elements/reserved-keywords-transact-sql.md)      
[Transact-SQL 디자인 문제](/previous-versions/visualstudio/visual-studio-2010/dd193411(v=vs.100))    
[Transact-SQL 명명 문제](/previous-versions/visualstudio/visual-studio-2010/dd193246(v=vs.100))        
[Transact-SQL 성능 문제](/previous-versions/visualstudio/visual-studio-2010/dd172117(v=vs.100))