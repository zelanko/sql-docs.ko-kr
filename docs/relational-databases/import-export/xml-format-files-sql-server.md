---
title: "XML 서식 파일(SQL Server) | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-bulk-import-export
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- format files [SQL Server], XML format files
- bulk importing [SQL Server], format files
- XML format files [SQL Server]
ms.assetid: 69024aad-eeea-4187-8fea-b49bc2359849
caps.latest.revision: 45
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: bf5b724d58fde9162bc75a4052f569b5218bbe8c
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="xml-format-files-sql-server"></a>XML 서식 파일(SQL Server)
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에서는 *테이블에 데이터를 대량으로 가져오는 데 사용할* XML 형식 파일 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 을 작성하기 위한 구문을 정의하는 XML 스키마를 제공합니다. XML 서식 파일은 XSDL(XML Schema Definition Language)에 정의되어 있는 이 스키마에 충실해야 합니다. XML 서식 파일은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 도구를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client와 함께 설치한 경우에만 지원됩니다.  
  
 XML 서식 파일은 **bcp** 명령, BULK INSERT 문 또는 INSERT ... SELECT \* FROM OPENROWSET(BULK...)과 함께 사용할 수 있습니다. **bcp** 명령을 사용하면 테이블에 대해 XML 형식 파일을 자동으로 생성할 수 있습니다. 자세한 내용은 [bcp Utility](../../tools/bcp-utility.md)를 참조하세요.  
  
> [!NOTE]  
>  *비 XML 서식 파일* 및 *XML 서식 파일*의 두 가지 서식 파일 유형을 대량으로 내보내고 가져올 수 있습니다. XML 서식 파일은 비 XML 서식 파일 대신 사용할 수 있는 보다 융통성 있고 강력한 파일 유형입니다. 비 XML 서식 파일에 대한 자세한 내용은 [비 XML 서식 파일&#40;SQL Server&#41;](../../relational-databases/import-export/non-xml-format-files-sql-server.md)를 참조하세요.  
  
 **항목 내용:**  
  
-   [XML 형식 파일의 이점](#BenefitsOfXmlFFs)  
  
-   [XML 서식 파일의 구조](#StructureOfXmlFFs)  
  
-   [XML 서식 파일의 스키마 구문](#SchemaSyntax)  
  
-   [예제 XML 형식 파일](#SampleXmlFFs)  
  
-   [관련 태스크](#RelatedTasks)  
  
-   [관련 내용](#RelatedContent)  
  
##  <a name="BenefitsOfXmlFFs"></a> XML 형식 파일의 이점  
  
-   XML 형식 파일은 자체 설명적인 파일로, 쉽게 읽고 만들고 확장할 수 있습니다. 또한 사람이 읽을 수 있는 형태이기 때문에 대량 작업 중에 데이터가 해석되는 방식을 쉽게 이해할 수 있습니다.  
  
-   XML 형식 파일에는 대상 열의 데이터 형식이 포함됩니다.  XML 인코딩은 데이터 파일의 데이터 형식과 데이터 요소뿐만 아니라 데이터 요소와 테이블 열 간의 매핑도 명확하게 설명합니다.  
  
     이 특성은 데이터 파일에 데이터가 기록된 방식과 파일 내의 각 필드와 연결된 데이터 형식을 달리 지정할 수 있게 해줍니다. 예를 들어 데이터 파일이 데이터의 문자 표시를 포함하면 해당 SQL 열 형식은 무시됩니다.  
  
-   XML 형식 파일을 사용하면 데이터 파일에서 단일 LOB(Large Object) 데이터 형식이 포함된 필드를 로드할 수 있습니다.  
  
-   XML 서식 파일은 이전 버전과의 호환성을 유지하면서 향상될 수 있습니다. 또한 XML 인코딩은 명확하기 때문에 지정된 데이터 파일에 대해 다수의 서식 파일을 쉽게 만들 수 있습니다. 데이터 필드 전체나 일부를 서로 다른 테이블이나 뷰에 매핑해야 하는 경우 이 기능이 유용합니다.  
  
-   XML 구문은 작업 방향과 무관합니다. 즉, 대량 내보내기와 대량 가져오기의 구문은 동일합니다.  
  
-   XML 서식 파일을 사용하여 데이터를 대량으로 테이블이나 파티션이 없는 뷰로 가져오고 내보낼 수 있습니다.  
  
-   OPENROWSET(BULK...) 함수의 경우 대상 테이블 지정은 선택 사항입니다. 이 함수는 XML 형식 파일을 이용하여 데이터 파일에서 데이터를 읽기 때문입니다.  
  
    > [!NOTE]  
    >  **bcp** 명령과 BULK INSERT 문의 경우 대상 테이블 열을 사용하여 형식 변환을 수행하므로 대상 테이블이 필요합니다.  
  
##  <a name="StructureOfXmlFFs"></a> XML 서식 파일의 구조  
 비 XML 서식 파일과 마찬가지로 XML 서식 파일도 데이터 파일의 데이터 필드 형식과 구조를 정의하며 해당 데이터 필드를 단일 대상 테이블의 열에 매핑합니다.  
  
 XML 서식 파일에는 두 개의 주요 구성 요소 \<RECORD>와 \<ROW>가 있습니다.  
  
-   \<RECORD>는 데이터 파일에 저장되어 있는 데이터를 설명합니다.  
  
     각 \<RECORD> 요소는 하나 이상의 \<FIELD> 요소 집합을 포함합니다. 이러한 요소는 데이터 파일의 필드에 해당합니다. 기본 구문은 다음과 같습니다.  
  
     \<RECORD>  
  
     \<FIELD .../> [ ...*n* ]  
  
     \</RECORD>  
  
     각 \<FIELD> 요소는 특정 데이터 필드의 콘텐츠를 설명합니다. 필드 하나는 테이블의 열 하나에만 매핑할 수 있지만 모든 필드를 열에 매핑해야 하는 것은 아닙니다.  
  
     데이터 파일의 필드는 고정/가변 길이이거나 종료된 문자일 수 있습니다. *필드 값* 은 문자(1바이트 표현 사용), 와이드 문자(유니코드 2바이트 표현 사용), 네이티브 데이터베이스 형식 또는 파일 이름으로 표현될 수 있습니다. 필드 값이 파일 이름으로 표현되는 경우 파일 이름은 대상 테이블의 BLOB 열 값이 포함된 파일을 가리킵니다.  
  
-   \<ROW>는 파일의 데이터를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블로 가져올 때 데이터 파일의 데이터 행을 구성하는 방법을 설명합니다.  
  
     \<ROW> 요소에는 \<COLUMN> 열 집합이 포함됩니다. 이러한 요소는 테이블 열에 해당합니다. 기본 구문은 다음과 같습니다.  
  
     \<ROW>  
  
     \<COLUMN .../> [ ...*n* ]  
  
     \</ROW>  
  
     각 \<COLUMN> 요소는 데이터 파일의 필드 하나에만 매핑할 수 있습니다. \<ROW> 요소에서 \<COLUMN> 요소의 순서에 따라 대량 작업에서 반환되는 순서가 정의됩니다. XML 서식 파일은 각 \<COLUMN> 요소에 대량 가져오기 작업의 대상 테이블에 있는 열과 관계가 없는 로컬 이름을 지정합니다.  
  
##  <a name="SchemaSyntax"></a> XML 서식 파일의 스키마 구문  
 이 섹션에서는 XML 형식 파일의 XML 스키마 요소 및 특성에 대한 요약을 제공합니다. 서식 파일의 구문은 작업 방향과는 무관합니다. 즉, 대량 내보내기와 대량 가져오기의 구문은 동일합니다. 또한 이 섹션에서는 대량 가져오기에서 \<ROW> 및 \<COLUMN> 요소를 사용하는 방법과 요소의 xsi:type 값을 데이터 집합에 포함시키는 방법에 대해 설명합니다.  
  
 구문이 실제 XML 형식 파일과 일치하는지 보려면 이 항목 뒷부분에 있는 [예제 XML 형식 파일](#SampleXmlFFs)을 참조하세요.  
  
> [!NOTE]  
>  필드와 테이블 열의 번호 또는 순서가 서로 다른 데이터 파일로부터 대량 가져오기를 수행하도록 서식 파일을 수정할 수 있습니다. 자세한 내용은 [데이터를 가져오거나 내보내기 위한 서식 파일&#40;SQL Server&#41;](../../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md)를 참조하세요.  
  
 **섹션 내용**  
  
-   [XML 스키마의 기본 구문](#BasicSyntax)  
  
-   [대량 가져오기에서 \<ROW> 요소를 사용하는 방법](#HowUsesROW)  
  
-   [대량 가져오기에서 \<COLUMN> 요소를 사용하는 방법](#HowUsesColumn)  
  
-   [데이터 집합에 xsi:type 값 넣기](#PutXsiTypeValueIntoDataSet)  
  
###  <a name="BasicSyntax"></a> XML 스키마의 기본 구문  
 이 문의 구문에서는 요소(\<BCPFORMAT>, \<RECORD>, \<FIELD>, \<ROW>, \<COLUMN>) 및 그 기본 특성만 보여 줍니다.  
  
 \<BCPFORMAT ...>  
  
 \<RECORD>  
  
 \<FIELD ID = "*fieldID*" xsi:type = "*fieldType*" [...]  
  
 />  
  
 \</RECORD>  
  
 \<ROW>  
  
 \<COLUMN SOURCE = "*fieldID*" NAME = "*columnName*" xsi:type = "*columnType*" [...]  
  
 />  
  
 \</ROW>  
  
 \</BCPFORMAT>  
  
> [!NOTE]  
>  \<FIELD> 또는 \<COLUMN> 요소의 xsi:type 값과 연관된 추가 특성은 이 항목의 뒷부분에서 설명합니다.  
  
 **섹션 내용**  
  
-   [스키마 요소](#SchemaElements)  
  
-   [\<FIELD> 요소의 특성](#AttrOfFieldElement)(및 [\<FIELD> 요소의 xsi:type 값](#XsiTypeValuesOfFIELD))  
  
-   [\<COLUMN> 요소의 특성](#AttrOfColumnElement)(및 [\<COLUMN> xsi:type 값](#XsiTypeValuesOfCOLUMN))  
  
####  <a name="SchemaElements"></a> 스키마 요소  
 이 섹션에서는 XML 스키마가 XML 서식 파일에 대해 정의하는 각 요소의 목적에 대해 요약합니다. 특성은 뒷부분의 다른 섹션에서 설명합니다.  
  
 \<BCPFORMAT>  
 지정된 데이터 파일의 레코드 구조와 테이블 행의 열과의 일치를 정의하는 서식 파일 요소입니다.  
  
 \<RECORD .../>  
 하나 이상의 \<FIELD> 요소를 포함하는 복잡한 요소를 정의합니다. 서식 파일에서 필드가 선언되는 순서는 이들 필드가 데이터 파일에 나열되는 순서입니다.  
  
 \<FIELD .../>  
 데이터를 포함하는 데이터 파일의 필드를 정의합니다.  
  
 이 요소의 특성은 이 항목의 뒷부분에 나오는 [\<FIELD> 요소의 특성](#AttrOfFieldElement)에서 설명합니다.  
  
 \<ROW .../>  
 하나 이상의 \<COLUMN> 요소를 포함하는 복잡한 요소를 정의합니다. \<COLUMN> 요소의 순서는 RECORD 정의에 있는 \<FIELD> 요소의 순서와는 독립적입니다. 반면, 서식 파일에 있는 \<COLUMN> 요소의 순서는 결과 행 집합의 열 순서를 결정합니다. 데이터 필드는 해당 \<COLUMN> 요소가 \<COLUMN> 요소에서 선언되는 순서대로 로드됩니다.  
  
 자세한 내용은 뒷부분의 [대량 가져오기의 \<ROW> 요소 사용 방법](#HowUsesROW)을 참조하세요.  
  
 \<COLUMN>  
 열을 요소(\<COLUMN>)로 정의합니다. 각 \<COLUMN> 요소는 ID가 \<COLUMN> 요소의 SOURCE 특성에서 지정되는 \<FIELD> 요소에 해당합니다.  
  
 이 요소의 특성은 이 항목의 뒷부분에 나오는 [\<COLUMN> 요소의 특성](#AttrOfColumnElement)에서 설명합니다. 자세한 내용은 뒷부분의 [대량 가져오기의 \<COLUMN> 요소를 사용하는 방법](#HowUsesColumn)을 참조하세요.  
  
 \</BCPFORMAT>  
 서식 파일을 끝내는 데 필요합니다.  
  
####  <a name="AttrOfFieldElement"></a> \<FIELD> 요소의 특성  
 이 섹션에서는 \<FIELD> 요소의 특성에 대해 설명합니다. 다음 스키마 구문으로 요약할 수 있습니다.  
  
 \<FIELD  
  
 ID **="***fieldID***"**  
  
 xsi**:**type **="***fieldType***"**  
  
 [ LENGTH **="***n***"** ]  
  
 [ PREFIX_LENGTH **="***p***"** ]  
  
 [ MAX_LENGTH **="***m***"** ]  
  
 [ COLLATION **="***collationName***"** ]  
  
 [ TERMINATOR **="***terminator***"** ]  
  
 />  
  
 각 \<FIELD> 요소는 다른 요소와는 독립적입니다. 필드는 다음 특성에 따라 설명됩니다.  
  
|FIELD 특성|설명|선택 /<br /><br /> 필수임|  
|---------------------|-----------------|------------------------------|  
|ID **="***fieldID***"**|데이터 파일에서 필드의 논리적 이름을 지정합니다. 필드의 ID는 필드를 참조하는 데 사용되는 키입니다.<br /><br /> \<FIELD ID**="***fieldID***"**/>는 \<COLUMN SOURCE**="***fieldID***"**/>에 매핑됩니다.|필수임|  
|xsi:type **="***fieldType***"**|요소의 인스턴스 유형을 식별하는 XML 구문(특성처럼 사용)입니다. *fieldType* 값은 지정한 인스턴스에서 필요한 옵션 특성(아래)을 결정합니다.|필수(데이터 형식에 따라 다름)|  
|LENGTH **="***n***"**|이 특성은 고정 길이 데이터 형식의 인스턴스 길이를 정의합니다.<br /><br /> *n* 값은 양의 정수여야 합니다.|선택(xsi:type 값에서 필요로 하지 않는 경우)|  
|PREFIX_LENGTH **="***p***"**|이 특성은 이진 데이터 표현의 접두사 길이를 정의합니다. PREFIX_LENGTH 값인 *p*는 1, 2, 4 또는 8 중 하나를 사용해야 합니다.|선택(xsi:type 값에서 필요로 하지 않는 경우)|  
|MAX_LENGTH **="***m***"**|이 특성은 지정된 필드에 저장할 수 있는 최대 바이트 수입니다. 대상 테이블이 없는 경우 열의 최대 길이를 알 수 없습니다. MAX_LENGTH 특성은 출력 문자 열의 최대 길이를 제한하여 열 값에 할당된 저장소를 제한합니다. 특히 SELECT FROM 절에서 OPENROWSET 함수의 BULK 옵션을 사용할 때 편리합니다.<br /><br /> *m* 값은 양의 정수여야 합니다. 기본적으로 최대 길이는 **char** 열의 경우 8000자, **nchar** 열의 경우 4000자입니다.|선택 사항|  
|COLLATION **="***collationName***"**|COLLATION은 문자 필드에서만 사용할 수 있습니다. SQL 데이터 정렬 이름 목록은 [SQL Server 데이터 정렬 이름&#40;Transact-SQL&#41;](../../t-sql/statements/sql-server-collation-name-transact-sql.md)을 참조하세요.|선택 사항|  
|TERMINATOR **= "***terminator***"**|이 특성은 데이터 필드의 종결자를 지정합니다. 종결자는 어떠한 문자도 가능합니다. 종결자는 데이터의 일부가 아닌 고유 문자여야 합니다.<br /><br /> 기본적으로 필드 종결자는 탭 문자(\t로 표시)입니다. 단락 기호를 표시하려면 \r\n을 사용하세요.|이 특성이 필요한 문자 데이터의 xsi:type에만 사용됩니다.|  
  
#####  <a name="XsiTypeValuesOfFIELD"></a> \<FIELD> 요소의 xsi:type 값  
 xsi:type 값은 요소 인스턴스의 데이터 형식을 식별하는 XML 구문(특성처럼 사용)입니다. xsi:type 값의 사용 방법은 이 섹션의 뒷부분에 나오는 "데이터 집합에 xsi:type 값 넣기"를 참조하세요.  
  
 \<FIELD> 요소의 xsi:type 값은 다음 데이터 형식을 지원합니다.  
  
|\<FIELD> xsi:type 값|데이터 형식의<br /><br /> 선택적 XML 특성|데이터 형식의<br /><br /> 선택적 XML 특성|  
|-------------------------------|---------------------------------------------------|---------------------------------------------------|  
|**NativeFixed**|**LENGTH**|없음|  
|**NativePrefix**|**PREFIX_LENGTH**|MAX_LENGTH|  
|**CharFixed**|**LENGTH**|COLLATION|  
|**NCharFixed**|**LENGTH**|COLLATION|  
|**CharPrefix**|**PREFIX_LENGTH**|MAX_LENGTH, COLLATION|  
|**NCharPrefix**|**PREFIX_LENGTH**|MAX_LENGTH, COLLATION|  
|**CharTerm**|**TERMINATOR**|MAX_LENGTH, COLLATION|  
|**NCharTerm**|**TERMINATOR**|MAX_LENGTH, COLLATION|  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식에 대한 자세한 내용은 [데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)을 참조하세요.  
  
####  <a name="AttrOfColumnElement"></a> \<COLUMN> 요소의 특성  
 이 섹션에서는 \<COLUMN> 요소의 특성에 대해 설명합니다. 다음 스키마 구문으로 요약할 수 있습니다.  
  
 \<요소의 Xsi:type 값  
  
 SOURCE = "*fieldID*"  
  
 NAME = "*columnName*"  
  
 xsi:type = "*columnType*"  
  
 [ LENGTH = "*n*" ]  
  
 [ PRECISION = "*n*" ]  
  
 [ SCALE = "*value*" ]  
  
 [ NULLABLE = { "YES"  
  
 "NO" } ]  
  
 />  
  
 필드는 다음 특성을 사용하여 대상 테이블의 열에 매핑됩니다.  
  
|COLUMN 특성|설명|선택 /<br /><br /> 필수임|  
|----------------------|-----------------|------------------------------|  
|SOURCE **="***fieldID***"**|열에 매핑되는 필드의 ID를 지정합니다.<br /><br /> \<COLUMN SOURCE**="***fieldID***"**/>는 \<FIELD ID**="***fieldID***"**/>에 매핑됩니다.|필수임|  
|NAME = "*columnName*"|서식 파일에 의해 표현된 행 집합의 열 이름을 지정합니다. 이 열 이름은 결과 집합에서 열을 식별하는 데 사용되며 대상 테이블에서 사용되는 열 이름과 일치할 필요는 없습니다.|필수임|  
|xsi**:**type **="***ColumnType***"**|요소의 인스턴스 데이터 형식을 식별하는 XML 구문(특성처럼 사용)입니다. *ColumnType* 값은 지정한 인스턴스에서 필요한 옵션 특성(아래)을 결정합니다.<br /><br /> 참고: *ColumnType*의 가능한 값 및 관련 특성은 [&lt;COLUMN&gt; 요소의 Xsi:type 값](#XsiTypeValuesOfCOLUMN) 섹션의 \<COLUMN> 요소 테이블에 나와 있습니다.|선택 사항|  
|LENGTH **="***n***"**|고정 길이 데이터 형식의 인스턴스 길이를 정의합니다. LENGTH는 xsi:type이 문자열 데이터 형식인 경우에만 사용됩니다.<br /><br /> *n* 값은 양의 정수여야 합니다.|선택(xsi:type이 문자열 데이터 형식인 경우에만 사용 가능)|  
|PRECISION **="***n***"**|숫자의 전체 자릿수를 나타냅니다. 예를 들어 123.45의 전체 자릿수는 5입니다.<br /><br /> 값은 양의 정수여야 합니다.|선택(xsi:type이 가변 숫자 데이터 형식인 경우에만 사용 가능)|  
|SCALE **="***int***"**|숫자에서 소수점 이하 자릿수를 나타냅니다. 예를 들어 123.45의 소수 자릿수는 2입니다.<br /><br /> 값은 정수여야 합니다.|선택(xsi:type이 가변 숫자 데이터 형식인 경우에만 사용 가능)|  
|NULLABLE **=** { **"**YES**"**<br /><br /> **"**NO**"** }|열이 NULL 값을 허용하는지 여부를 나타냅니다. 이 특성은 FIELDS와는 독립적입니다. 그러나 열이 NULLABLE이 아닌 경우 필드에서 NULL을 지정하면(아무 값도 지정하지 않음) 런타임 오류가 발생합니다.<br /><br /> NULLABLE 특성은 일반 SELECT FROM OPENROWSET(BULK...) 문의 경우에만 사용됩니다.|선택 사항(모든 데이터 형식에 사용 가능)|  
  
#####  <a name="XsiTypeValuesOfCOLUMN"></a> \<COLUMN> 요소의 xsi:type 값  
 xsi:type 값은 요소 인스턴스의 데이터 형식을 식별하는 XML 구문(특성처럼 사용)입니다. xsi:type 값의 사용 방법은 이 섹션의 뒷부분에 나오는 "데이터 집합에 xsi:type 값 넣기"를 참조하세요.  
  
 \<COLUMN> 요소는 다음과 같이 원시 SQL 데이터 형식을 지원합니다.  
  
|형식 범주|\<COLUMN> 데이터 형식|데이터 형식의<br /><br /> 선택적 XML 특성|데이터 형식의<br /><br /> 선택적 XML 특성|  
|-------------------|---------------------------|---------------------------------------------------|---------------------------------------------------|  
|고정|**SQLBIT**, **SQLTINYINT**, **SQLSMALLINT**, **SQLINT**, **SQLBIGINT**, **SQLFLT4**, **SQLFLT8**, **SQLDATETIME**, **SQLDATETIM4**, **SQLDATETIM8**, **SQLMONEY**, **SQLMONEY4**, **SQLVARIANT**및 **SQLUNIQUEID**|없음|NULLABLE|  
|가변 숫자|**SQLDECIMAL** 및 **SQLNUMERIC**|없음|NULLABLE, PRECISION, SCALE|  
|LOB|**SQLIMAGE**, **CharLOB**, **SQLTEXT**및 **SQLUDT**|없음|NULLABLE|  
|문자 LOB|**SQLNTEXT**|없음|NULLABLE|  
|이진 문자열|**SQLBINARY** 및 **SQLVARYBIN**|없음|NULLABLE, LENGTH|  
|문자열|**SQLCHAR**, **SQLVARYCHAR**, **SQLNCHAR**및 **SQLNVARCHAR**|없음|NULLABLE, LENGTH|  
  
> [!IMPORTANT]  
>  SQLXML 데이터를 대량으로 내보내거나 가져오려면 서식 파일에서 다음 데이터 형식 중 하나를 사용합니다. SQLCHAR 또는 SQLVARYCHAR(데이터 정렬에 의해 포함된 코드 페이지나 클라이언트 코드 페이지로 데이터가 전송됨), SQLNCHAR 또는 SQLNVARCHAR(데이터가 유니코드로 전송됨), SQLBINARY 또는 SQLVARYBIN(데이터가 변환되지 않고 전송됨) 데이터 형식 중 하나를 사용합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식에 대한 자세한 내용은 [데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)을 참조하세요.  
  
###  <a name="HowUsesROW"></a> 대량 가져오기에서 \<ROW> 요소를 사용하는 방법  
 일부 컨텍스트에서는 \<ROW> 요소가 무시됩니다. \<ROW> 요소가 대량 가져오기 작업에 영향을 주는지 여부는 작업 수행 방법에 따라 달라질 수 있습니다.  
  
-   **bcp** 명령  
  
     데이터가 대상 테이블에 로드되면 **bcp**는 \<ROW> 구성 요소를 무시합니다. 대신 **bcp** 는 대상 테이블의 열 유형을 기반으로 하는 데이터를 로드합니다.  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] 문(BULK INSERT 및 OPENROWSET의 대량 행 집합 공급자)  
  
     대량의 데이터를 테이블로 가져오는 경우 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문은 \<ROW> 구성 요소를 사용하여 입력 행 집합을 생성합니다. 또한 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문은 \<ROW>에서 지정된 열 유형과 대상 테이블에 있는 해당 열에 따라 적절한 형식 변환을 수행합니다. 서식 파일에서 지정된 열 유형과 대상 테이블에서 지정된 열 유형이 일치하지 않는 경우 추가 형식 변환이 수행됩니다. **bcp**와 비교할 때 이 추가 형식 변환으로 인해 BULK INSERT 또는 OPENROWSET의 대량 행 집합 공급자 동작에서 다소 불일치(전체 자릿수 손실)가 발생할 수 있습니다.  
  
     \<ROW> 요소의 정보를 사용하면 추가 정보 없이 행을 생성할 수 있습니다. 따라서 SELECT 문(SELECT \* FROM OPENROWSET(BULK *datafile* FORMATFILE=*xmlformatfile*)을 사용하여 행 집합을 생성할 수 있습니다.  
  
    > [!NOTE]  
    >  OPENROWSET BULK 절에는 서식 파일이 필요합니다. XML 서식 파일을 사용해야만 필드 데이터 형식에서 열 데이터 형식으로 변환할 수 있습니다.  
  
###  <a name="HowUsesColumn"></a> 대량 가져오기에서 \<COLUMN> 요소를 사용하는 방법  
 대량의 데이터를 테이블로 가져오는 경우 서식 파일의 \<COLUMN> 요소는 다음을 지정하여 데이터 파일 필드를 테이블 열에 매핑합니다.  
  
-   데이터 파일의 행 내의 각 필드 위치  
  
-   필드 데이터 형식을 원하는 열 데이터 형식으로 변환하는 데 사용되는 열 유형  
  
 열이 필드에 매핑되지 않으면 해당 필드는 생성된 행에 복사되지 않습니다. 이 동작을 통해 데이터 파일은 다른 열(다른 테이블)을 포함하는 행을 생성할 수 있습니다.  
  
 마찬가지로 테이블에서 데이터를 대량으로 내보내는 경우 서식 파일의 각 \<COLUMN>은 입력 테이블 행의 열을 출력 데이터 파일의 해당 필드에 매핑합니다.  
  
###  <a name="PutXsiTypeValueIntoDataSet"></a> 데이터 집합에 xsi:type 값 넣기  
 XSD(XML 스키마 정의) 언어를 통해 XML 문서의 유효성이 검사된 경우 xsi:type 값을 데이터 집합에 넣을 수 없습니다. 그러나 다음 코드 조각의 설명과 같이 XML 서식 파일을 XML 문서(예: `myDoc`)에 로드하여 xsi:type 정보를 데이터 집합에 넣을 수 있습니다.  
  
```  
...;  
myDoc.LoadXml(xmlFormat);  
XmlNodeList ColumnList = myDoc.GetElementsByTagName("COLUMN");  
for(int i=0;i<ColumnList.Count;i++)  
{  
   Console.Write("COLUMN: xsi:type=" +ColumnList[i].Attributes["type",  
      "http://www.w3.org/2001/XMLSchema-instance"].Value+"\n");  
}  
```  
  
##  <a name="SampleXmlFFs"></a> 예제 XML 형식 파일  
 이 섹션에는 [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)] 의 예를 포함하여 다양한 경우의 XML 형식 파일 사용에 대한 정보가 들어 있습니다.  
  
> [!NOTE]  
>  다음 예의 데이터 파일에서 `<tab>` 은 데이터 파일의 탭 문자를 나타내며 `<return>` 은 캐리지 리턴을 나타냅니다.  
  
 이 예에서는 다음과 같은 XML 형식 파일 사용의 주요 측면을 설명합니다.  
  
-   [테이블 열과 동일하게 문자 데이터 필드 정렬](#OrderCharFieldsSameAsCols)  
  
-   [데이터 필드와 테이블 열을 서로 다르게 정렬](#OrderFieldsAndColsDifferently)  
  
-   [데이터 필드 생략](#OmitField)  
  
-   [다양한 형식의 필드를 열에 매핑](#MapXSItype)  
  
-   [XML 데이터를 테이블에 매핑](#MapXMLDataToTbl)  
  
-   [고정 길이 또는 고정 너비 필드 가져오기](#ImportFixedFields)  
  
-   [추가 예](#AdditionalExamples)  
  
> [!NOTE]  
>  서식 파일을 만드는 방법은 [서식 파일 만들기&#40;SQL Server&#41;](../../relational-databases/import-export/create-a-format-file-sql-server.md)를 참조하세요.  
  
###  <a name="OrderCharFieldsSameAsCols"></a> 1. 테이블 열과 동일하게 문자 데이터 필드 정렬  
 다음 예에서는 3개의 문자 데이터 필드가 포함된 데이터 파일을 설명하는 XML 서식 파일을 보여 줍니다. 서식 파일은 데이터 파일을 3개의 열이 포함된 테이블로 매핑합니다. 데이터 필드는 테이블 열과 일 대 일로 대응합니다.  
  
 **테이블(행):** Person (Age int, FirstName varchar(20), LastName varchar(30))  
  
 **데이터 파일(레코드):** Age\<tab>Firstname\<tab>Lastname\<return>  
  
 다음 XML 서식 파일은 데이터 파일의 데이터를 테이블로 읽어 옵니다.  
  
 서식 파일은 `<RECORD>` 요소에서 3개의 필드에 있는 데이터 값을 문자 데이터로 표현합니다. 각 필드에서 `TERMINATOR` 특성은 데이터 값 다음에 오는 종결자를 나타냅니다.  
  
 데이터 필드는 테이블 열과 일 대 일로 대응합니다. 서식 파일은 `<ROW>` 요소의 `Age` 열을 첫 번째 필드에, `FirstName` 열을 두 번째 필드에, `LastName` 열을 세 번째 필드에 매핑합니다.  
  
```  
<?xml version="1.0"?>  
<BCPFORMAT   
xmlns="http://schemas.microsoft.com/sqlserver/2004/bulkload/format"   
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
  <RECORD>  
    <FIELD ID="1" xsi:type="CharTerm" TERMINATOR="\t"   
      MAX_LENGTH="12"/>   
    <FIELD ID="2" xsi:type="CharTerm" TERMINATOR="\t"   
      MAX_LENGTH="20" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
    <FIELD ID="3" xsi:type="CharTerm" TERMINATOR="\r\n"   
      MAX_LENGTH="30"   
      COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
  </RECORD>  
  <ROW>  
    <COLUMN SOURCE="1" NAME="age" xsi:type="SQLINT"/>  
    <COLUMN SOURCE="2" NAME="firstname" xsi:type="SQLVARYCHAR"/>  
    <COLUMN SOURCE="3" NAME="lastname" xsi:type="SQLVARYCHAR"/>  
  </ROW>  
</BCPFORMAT>  
```  
  
> [!NOTE]  
>  해당하는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 예제는 [서식 파일 만들기&#40;SQL Server&#41;](../../relational-databases/import-export/create-a-format-file-sql-server.md)를 참조하세요.  
  
###  <a name="OrderFieldsAndColsDifferently"></a> 2. 데이터 필드와 테이블 열을 서로 다르게 정렬  
 다음 예에서는 3개의 문자 데이터 필드가 포함된 데이터 파일을 설명하는 XML 서식 파일을 보여 줍니다. 서식 파일은 데이터 파일을 데이터 파일의 필드와 다르게 정렬된 3개의 열을 포함하는 테이블로 매핑합니다.  
  
 **테이블(행):** Person (Age int, FirstName varchar(20), LastName varchar(30))  
  
 **데이터 파일**(레코드): Age\<tab>Lastname\<tab>Firstname\<return>  
  
 서식 파일은 `<RECORD>` 요소에서 3개의 필드에 있는 데이터 값을 문자 데이터로 표현합니다.  
  
 서식 파일은 `<ROW>` 요소의 `Age` 열을 첫 번째 필드에, `FirstName` 열을 세 번째 필드에, `LastName` 열을 두 번째 필드에 매핑합니다.  
  
```  
<?xml version="1.0"?>  
<BCPFORMAT   
xmlns="http://schemas.microsoft.com/sqlserver/2004/bulkload/format"   
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
  <RECORD>  
    <FIELD ID="1" xsi:type="CharTerm" TERMINATOR="\t"   
      MAX_LENGTH="12"/>  
    <FIELD ID="2" xsi:type="CharTerm" TERMINATOR="\t" MAX_LENGTH="20"   
      COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
    <FIELD ID="3" xsi:type="CharTerm" TERMINATOR="\r\n"   
      MAX_LENGTH="30" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
  </RECORD>  
  <ROW>  
    <COLUMN SOURCE="1" NAME="age" xsi:type="SQLINT"/>  
    <COLUMN SOURCE="3" NAME="firstname" xsi:type="SQLVARYCHAR"/>  
    <COLUMN SOURCE="2" NAME="lastname" xsi:type="SQLVARYCHAR"/>  
  </ROW>  
</BCPFORMAT>  
```  
  
> [!NOTE]  
>  해당하는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 예제는 [서식 파일을 사용하여 테이블 열을 데이터 파일 필드에 매핑&#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)를 참조하세요.  
  
###  <a name="OmitField"></a> 3. 데이터 필드 생략  
 다음 예에서는 4개의 문자 데이터 필드가 포함된 데이터 파일을 설명하는 XML 서식 파일을 보여 줍니다. 서식 파일은 데이터 파일을 3개의 열이 포함된 테이블로 매핑합니다. 두 번째 데이터 필드는 대응되는 테이블 열이 없습니다.  
  
 **테이블(행):** Person (Age int, FirstName varchar(20), LastName varchar(30))  
  
 **데이터 파일(레코드):** Age\<tab>employeeID\<tab>Firstname\<tab>Lastname\<return>  
  
 서식 파일은 `<RECORD>` 요소에서 4개의 필드에 있는 데이터 값을 문자 데이터로 표현합니다. 각 필드에서 TERMINATOR 특성은 데이터 값 다음에 오는 종결자를 나타냅니다.  
  
 서식 파일은 `<ROW>` 요소의 `Age` 열을 첫 번째 필드에, `FirstName` 열을 세 번째 필드에, `LastName` 열을 네 번째 필드에 매핑합니다.  
  
```  
<BCPFORMAT   
xmlns="http://schemas.microsoft.com/sqlserver/2004/bulkload/format"   
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
  <RECORD>  
    <FIELD ID="1" xsi:type="CharTerm" TERMINATOR="\t"   
      MAX_LENGTH="12"/>  
    <FIELD ID="2" xsi:type="CharTerm" TERMINATOR="\t"   
      MAX_LENGTH="10"   
      COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
    <FIELD ID="3" xsi:type="CharTerm" TERMINATOR="\t"   
      MAX_LENGTH="20"   
      COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
    <FIELD ID="4" xsi:type="CharTerm" TERMINATOR="\r\n"   
      MAX_LENGTH="30"   
      COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
  </RECORD>  
  <ROW>  
    <COLUMN SOURCE="1" NAME="age" xsi:type="SQLINT"/>  
    <COLUMN SOURCE="3" NAME="firstname" xsi:type="SQLVARYCHAR"/>  
    <COLUMN SOURCE="4" NAME="lastname" xsi:type="SQLVARYCHAR"/>  
  </ROW>  
</BCPFORMAT>  
```  
  
> [!NOTE]  
>  해당하는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 예제는 [서식 파일을 사용하여 데이터 필드 건너뛰기&#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-data-field-sql-server.md)를 참조하세요.  
  
###  <a name="MapXSItype"></a> 4. \<FIELD> xsi:type을 \<COLUMN> xsi:type에 매핑  
 다음 예에서는 다양한 형식의 필드와 함께 해당 필드와 열의 매핑을 보여 줍니다.  
  
```  
<?xml version = "1.0"?>  
<BCPFORMAT  
xmlns="http://schemas.microsoft.com/sqlserver/2004/bulkload/format"   
   xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
   <RECORD>  
      <FIELD xsi:type="CharTerm" ID="C1" TERMINATOR="\t"   
            MAX_LENGTH="4"/>  
      <FIELD xsi:type="CharFixed" ID="C2" LENGTH="10"   
         COLLATION="SQL_LATIN1_GENERAL_CP1_CI_AS"/>  
      <FIELD xsi:type="CharPrefix" ID="C3" PREFIX_LENGTH="2"   
         MAX_LENGTH="32" COLLATION="SQL_LATIN1_GENERAL_CP1_CI_AS"/>  
      <FIELD xsi:type="NCharTerm" ID="C4" TERMINATOR="\t"   
         MAX_LENGTH="4"/>  
      <FIELD xsi:type="NCharFixed" ID="C5" LENGTH="10"   
         COLLATION="SQL_LATIN1_GENERAL_CP1_CI_AS"/>  
      <FIELD xsi:type="NCharPrefix" ID="C6" PREFIX_LENGTH="2"   
         MAX_LENGTH="32" COLLATION="SQL_LATIN1_GENERAL_CP1_CI_AS"/>  
      <FIELD xsi:type="NativeFixed" ID="C7" LENGTH="4"/>  
   </RECORD>  
   <ROW>  
      <COLUMN SOURCE="C1" NAME="Age" xsi:type="SQLTINYINT"/>  
      <COLUMN SOURCE="C2" NAME="FirstName" xsi:type="SQLVARYCHAR"   
      LENGTH="16" NULLABLE="NO"/>  
      <COLUMN SOURCE="C3" NAME="LastName" />  
      <COLUMN SOURCE="C4" NAME="Salary" xsi:type="SQLMONEY"/>  
      <COLUMN SOURCE="C5" NAME="Picture" xsi:type="SQLIMAGE"/>  
      <COLUMN SOURCE="C6" NAME="Bio" xsi:type="SQLTEXT"/>  
      <COLUMN SOURCE="C7" NAME="Interest"xsi:type="SQLDECIMAL"   
      PRECISION="5" SCALE="3"/>  
   </ROW>  
</BCPFORMAT>  
```  
  
###  <a name="MapXMLDataToTbl"></a> 5. XML 데이터를 테이블에 매핑  
 다음 예에서는 두 개의 빈 열을 가진 테이블(`t_xml`)을 만듭니다. 테이블의 첫 번째 열은 `int` 데이터 형식에, 두 번째 열은 `xml` 데이터 형식에 매핑됩니다.  
  
```  
CREATE TABLE t_xml (c1 int, c2 xml)  
```  
  
 다음 XML 서식 파일에서는 `t_xml`테이블에 데이터 파일을 로드합니다.  
  
```  
<?xml version="1.0"?>  
<BCPFORMAT xmlns="http://schemas.microsoft.com/sqlserver/2004/bulkload/format"   
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
 <RECORD>  
  <FIELD ID="1" xsi:type="NativePrefix" PREFIX_LENGTH="1"/>  
  <FIELD ID="2" xsi:type="NCharPrefix" PREFIX_LENGTH="8"/>  
 </RECORD>  
 <ROW>  
  <COLUMN SOURCE="1" NAME="c1" xsi:type="SQLINT"/>  
  <COLUMN SOURCE="2" NAME="c2" xsi:type="SQLNCHAR"/>  
 </ROW>  
</BCPFORMAT>  
```  
  
###  <a name="ImportFixedFields"></a> 6. 고정 길이 또는 고정 너비 필드 가져오기  
 다음 예에서는 `10` 자 또는 `6` 자의 각 고정 필드에 대해 설명합니다. 서식 파일은 이러한 필드 길이/너비를 각각 `LENGTH="10"` 및 `LENGTH="6"`으로 나타냅니다. 데이터 파일의 모든 행은 캐리지 리턴-줄바꿈 조합 {CR}{LF}로 끝납니다. 여기서 서식 파일은 `TERMINATOR="\r\n"`로 나타냅니다.  
  
```  
<?xml version="1.0"?>  
<BCPFORMAT  
       xmlns="http://schemas.microsoft.com/sqlserver/2004/bulkload/format"  
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
  <RECORD>  
    <FIELD ID="1" xsi:type="CharFixed" LENGTH="10"/>  
    <FIELD ID="2" xsi:type="CharFixed" LENGTH="6"/>  
    <FIELD ID="3" xsi:type="CharTerm" TERMINATOR="\r\n"  
  </RECORD>  
  <ROW>  
    <COLUMN SOURCE="1" NAME="C1" xsi:type="SQLINT" />  
    <COLUMN SOURCE="2" NAME="C2" xsi:type="SQLINT" />  
  </ROW>  
</BCPFORMAT>  
```  
  
###  <a name="AdditionalExamples"></a> 추가 예  
 비 XML 서식 파일과 XML 서식 파일의 추가 예를 보려면 다음 항목을 참조하세요.  
  
-   [서식 파일을 사용하여 테이블 열 건너뛰기&#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-table-column-sql-server.md)  
  
-   [서식 파일을 사용하여 데이터 필드 건너뛰기&#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-data-field-sql-server.md)  
  
-   [서식 파일을 사용하여 테이블 열을 데이터 파일 필드에 매핑&#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)  
  
##  <a name="RelatedTasks"></a> 관련 태스크  
  
-   [서식 파일 만들기&#40;SQL Server&#41;](../../relational-databases/import-export/create-a-format-file-sql-server.md)  
  
-   [서식 파일을 사용하여 데이터 대량 가져오기&#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-bulk-import-data-sql-server.md)  
  
-   [서식 파일을 사용하여 테이블 열 건너뛰기&#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-table-column-sql-server.md)  
  
-   [서식 파일을 사용하여 데이터 필드 건너뛰기&#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-data-field-sql-server.md)  
  
-   [서식 파일을 사용하여 테이블 열을 데이터 파일 필드에 매핑&#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)  
  
##  <a name="RelatedContent"></a> 관련 내용  
 없음  
  
## <a name="see-also"></a>참고 항목  
 [데이터 대량 가져오기 및 내보내기&#40;SQL Server&#41;](../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md)   
 [데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [비 XML 서식 파일&#40;SQL Server&#41;](../../relational-databases/import-export/non-xml-format-files-sql-server.md)   
 [데이터를 가져오거나 내보내기 위한 서식 파일&#40;SQL Server&#41;](../../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md)  
  
  
