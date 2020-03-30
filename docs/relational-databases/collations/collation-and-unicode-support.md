---
title: 데이터 정렬 및 유니코드 지원 | Microsoft Docs
ms.custom: ''
ms.date: 12/05/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- binary collations [SQL Server]
- expression-level collations [SQL Server]
- Windows collations [SQL Server]
- globalization [SQL Server], about globalization
- supplementary character support
- code pages [SQL Server], about code pages
- collations [SQL Server], about collations
- Unicode [SQL Server], collations
- database-level collations [SQL Server]
- reading order
- column-level collations
- locales [SQL Server], about locales
- locales [SQL Server]
- code pages [SQL Server]
- SQL Server collations
- UTF-8
- UTF-16
- UTF8
- UTF16
- UCS2
- server-level collations [SQL Server]
ms.assetid: 92d34f48-fa2b-47c5-89d3-a4c39b0f39eb
author: pmasl
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2d20f0cd4a08e22787caecfb663ef0d2dcd47003
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "75831811"
---
# <a name="collation-and-unicode-support"></a>데이터 정렬 및 유니코드 지원
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 데이터 정렬은 데이터에 대한 정렬 규칙과 대/소문자 및 악센트 구분 속성을 제공합니다. **char**, **varchar** 등의 문자 데이터 형식과 함께 사용되는 데이터 정렬은 해당 데이터 형식을 나타내는 데 사용할 수 있는 코드 페이지와 해당 문자를 지정합니다. 

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 새 인스턴스를 설치하든, 데이터베이스 백업을 복원하든, 서버를 클라이언트 데이터베이스에 연결하든 간에 사용하는 데이터의 로캘 요구 사항, 정렬 순서, 대/소문자 및 악센트 구분 여부를 파악하는 것이 중요합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 사용 가능한 데이터 정렬을 나열하려면 [sys.fn_helpcollations(Transact-SQL)](../../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md)를 참조하세요.    
    
서버, 데이터베이스, 열 또는 식의 데이터 정렬을 선택하면 데이터에 특정 특성이 할당됩니다. 이러한 특성은 여러 데이터베이스 작업의 결과에 영향을 줍니다. 예를 들어 `ORDER BY`를 사용하여 쿼리를 생성하는 경우, 결과 집합의 정렬 순서는 쿼리의 식 수준에서 `COLLATE` 절에 지정되거나 데이터베이스에 적용된 데이터 정렬에 따라 달라집니다.    
    
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 데이터 정렬 지원을 최대한 활용하려면 이 항목에 정의된 용어 및 용어와 데이터 특성 간의 관계를 파악해야 합니다.    
    
##  <a name="collation-terms"></a><a name="Terms"></a> 데이터 정렬 용어    
    
-   [데이터 정렬](#Collation_Defn) 
    - [데이터 정렬 집합](#Collation_sets)
    - [데이터 정렬 수준](#Collation_levels)
-   [로캘](#Locale_Defn)    
-   [코드 페이지](#Code_Page_Defn)    
-   [정렬 순서](#Sort_Order_Defn)    
    
###  <a name="collation"></a><a name="Collation_Defn"></a> 데이터 정렬    
데이터 정렬은 데이터 세트의 각 문자를 나타내는 비트 패턴을 지정합니다. 또한 데이터 정렬은 데이터를 정렬하고 비교하는 규칙을 결정합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 여러 다른 데이터 정렬을 갖는 개체를 단일 데이터베이스에 저장하도록 지원합니다. 비유니코드 열의 경우 데이터 정렬 설정은 데이터에 대한 코드 페이지와 나타낼 수 있는 문자를 지정합니다. 유니코드를 지원하지 않는 열 간에 데이터를 이동하려면 소스 코드 페이지에서 대상 코드 페이지로 데이터를 변환해야 합니다.    
    
데이터 정렬 설정이 각기 다른 데이터베이스의 컨텍스트에서[!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 실행하면 그 결과가 달라질 수 있습니다. 가능한 경우 조직에서 표준화된 데이터 정렬을 사용합니다. 그러면 모든 문자나 유니코드 식에서 데이터 정렬을 지정하지 않아도 됩니다. 데이터 정렬 및 코드 페이지 설정이 다른 개체를 사용해야 할 경우 선행 정렬 우선 순위 규칙을 고려하도록 쿼리를 코딩하세요. 자세한 내용은 [선행 정렬 우선 순위(Transact-SQL)](../../t-sql/statements/collation-precedence-transact-sql.md)를 참조하세요.    
    
데이터 정렬 관련 옵션에는 대/소문자 구분, 악센트 구분, 일본어 가나 구분, 전자/반자 구분, 변형 선택기 구분이 있습니다. [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]은(는) [UTF-8](https://www.wikipedia.org/wiki/UTF-8) 인코딩을 위한 추가 옵션을 도입합니다. 

데이터 정렬 이름에 추가하여 이러한 옵션을 지정할 수 있습니다. 예를 들어 **Japanese_Bushu_Kakusu_100_CS_AS_KS_WS_UTF8** 데이터 정렬은 대/소문자, 악센트, 일본어 가나, 전자/반자를 구분하며 UTF-8로 인코딩됩니다. 또 다른 예로 **Japanese_Bushu_Kakusu_140_CI_AI_KS_WS_VSS** 데이터 정렬은 대/소문자와 악센트를 구분하지 않고 일본어 가나, 전자/반자 및 변형 선택기를 구분하며 유니코드를 지원하지 않는 인코딩을 사용합니다. 

다음 표에서는 이러한 여러 옵션과 관련된 동작을 설명합니다.    
    
|옵션|Description|    
|------------|-----------------|    
|대/소문자 구분(\_CS)|대/소문자를 구분합니다. 이 옵션을 선택하면 소문자가 대문자보다 먼저 정렬됩니다. 이 옵션을 선택하지 않으면 데이터 정렬에서 대소문자를 구분하지 않습니다. 즉, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 정렬할 때 대문자와 소문자를 동일한 것으로 간주합니다. \_CI를 지정하여 대/소문자를 구분하지 않도록 명시적으로 선택할 수 있습니다.|   
|악센트 구분(\_AS)|악센트가 있는 문자와 악센트가 없는 문자를 구분합니다. 예를 들어 “a”와 “ấ”는 같지 않습니다. 이 옵션을 선택하지 않으면 데이터 정렬에서 악센트를 구분하지 않습니다. 즉, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 정렬할 때 악센트가 있는 문자와 악센트가 없는 문자가 동일한 것으로 간주합니다. \_AI를 지정하여 악센트를 구분하지 않도록 명시적으로 선택할 수 있습니다.|    
|일본어 가나 구분(\_KS)|일본어 가나 문자의 다음 두 가지 유형을 구분합니다. 히라가나 및 가타가나. 이 옵션을 선택하지 않으면 데이터 정렬에서 일본어 가나를 구분하지 않습니다. 즉, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 정렬할 때 히라가나 문자와 가타카나 문자를 동일한 것으로 간주합니다. 일본어 가나를 구분하지 않도록 지정하는 유일한 방법은 이 옵션을 생략하는 것입니다.|   
|전자/반자 구분(\_WS)|전자와 반자 문자를 구분합니다. 이 옵션을 선택하지 않으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 정렬할 때 같은 문자의 전자 표시와 반자 표시를 동일한 문자로 간주합니다. 전자/반자를 구분하지 않도록 지정하는 유일한 방법은 이 옵션을 생략하는 것입니다.|  
|변형 선택기 구분(\_VSS)|[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]에서 도입된 일본어 데이터 정렬 **Japanese_Bushu_Kakusu_140** 및 **Japanese_XJIS_140**의 다양한 표의 문자 변형 선택기를 구분합니다. 변형 시퀀스는 기본 문자와 추가 변형 선택기로 구성됩니다. 이 \_VSS 옵션을 선택하지 않으면 데이터 정렬이 변형 선택기를 구분하지 않고 비교 시 변형 선택기가 고려되지 않습니다. 즉, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 정렬할 때 서로 다른 변형 선택기를 사용하여 동일한 기본 문자를 바탕으로 작성된 문자를 동일한 문자로 간주합니다. 자세한 내용은 [Unicode Ideographic Variation Database](https://www.unicode.org/reports/tr37/)(유니코드 표의 문자 변형 데이터베이스)를 참조하세요.<br/><br/> 변형 선택기 구분(\_VSS) 데이터 정렬은 전체 텍스트 검색 인덱스에서 지원되지 않습니다. 전체 텍스트 검색 인덱스는 악센트 구분(\_AS), 일본어 가나 구분(\_KS) 및 전자/반자 구분(\_WS) 옵션만 지원합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] XML 및 CLR 엔진은 (\_VSS) 변형 선택기를 지원하지 않습니다.|      
|이진(\_BIN)<sup>1</sup>|각 문자에 대해 정의된 비트 패턴을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블의 데이터를 정렬하고 비교합니다. 이진 정렬 순서는 대/소문자와 악센트를 구분합니다. 이진은 가장 빠른 정렬 순서입니다. 자세한 내용은 이 문서에서 [이진 데이터 정렬](#Binary-collations) 섹션을 참조하세요.|      
|이진 코드 포인트(\_BIN2) <sup>1</sup> | 유니코드 데이터에 대한 유니코드 코드 포인트를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블의 데이터를 정렬하고 비교합니다. 유니코드를 지원하지 않는 데이터의 경우 이진 코드 포인트에서 이진 정렬 비교와 동일한 비교를 사용합니다.<br/><br/> 이진 코드 포인트 정렬 순서 사용 시의 이점은 정렬된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터를 비교하는 애플리케이션에서 데이터를 재정렬할 필요가 없다는 점입니다. 결과적으로 이진 코드 포인트 정렬 순서를 사용하면 애플리케이션을 더 간단하게 개발할 수 있으며 성능이 향상될 수 있습니다. 자세한 내용은 이 문서에서 [이진 데이터 정렬](#Binary-collations) 섹션을 참조하세요.|
|UTF-8(\_UTF8)|UTF-8 인코딩 데이터를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 저장할 수 있습니다. 이 옵션을 선택하지 않으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 해당 데이터 형식에 유니코드를 지원하지 않는 기본 인코딩 형식을 사용합니다. 자세한 내용은 이 문서에서 [UTF-8 지원](#utf8) 섹션을 참조하세요.| 

<sup>1</sup> BIN 또는 이진 코드 포인트를 선택하면 대/소문자 구분(\_CS), 악센트 구분(\_AS), 일본어 가나 구분(\_KS) 및 전자/반자 구분(\_WS) 옵션을 사용할 수 없습니다.      

#### <a name="examples-of-collation-options"></a>데이터 정렬 옵션의 예
각 데이터 정렬은 일련의 접미사로 결합되어 대/소문자, 악센트, 일본어 가나, 전자/반자 구분 여부를 정의합니다. 다음 예에서는 다양한 접미사 조합에 대한 정렬 순서 동작에 대해 설명합니다.

|Windows 데이터 정렬 접미사|정렬 순서 설명|
|------------|-----------------| 
|\_BIN<sup>1</sup>|이진 정렬|
|\_BIN2<sup>1, 2</sup>|이진 코드 포인트 정렬 순서|
|\_CI_AI<sup>2</sup>|대/소문자 구분 안 함, 악센트 구분 안 함, 일본어 가나 구분 안 함, 전자/반자 구분 안 함|
|\_CI_AI_KS<sup>2</sup>|대/소문자 구분 안 함, 악센트 구분 안 함, 일본어 가나 구분, 전자/반자 구분 안 함|
|\_CI_AI_KS_WS<sup>2</sup>|대/소문자 구분 안 함, 악센트 구분 안 함, 일본어 가나 구분, 전자/반자 구분|
|\_CI_AI_WS<sup>2</sup>|대/소문자 구분 안 함, 악센트 구분 안 함, 일본어 가나 구분 안 함, 전자/반자 구분|
|\_CI_AS<sup>2</sup>|대/소문자 구분 안 함, 악센트 구분, 일본어 가나 구분 안 함, 전자/반자 구분 안 함|
|\_CI_AS_KS<sup>2</sup>|대/소문자 구분 안 함, 악센트 구분, 일본어 가나 구분, 전자/반자 구분 안 함|
|\_CI_AS_KS_WS<sup>2</sup>|대/소문자 구분 안 함, 악센트 구분, 일본어 가나 구분, 전자/반자 구분|
|\_CI_AS_WS<sup>2</sup>|대/소문자 구분 안 함, 악센트 구분, 일본어 가나 구분 안 함, 전자/반자 구분|
|\_CS_AI<sup>2</sup>|대/소문자 구분, 악센트 구분 안 함, 일본어 가나 구분 안 함, 전자/반자 구분 안 함|
|\_CS_AI_KS<sup>2</sup>|대/소문자 구분, 악센트 구분 안 함, 일본어 가나 구분, 전자/반자 구분 안 함|
|\_CS_AI_KS_WS<sup>2</sup>|대/소문자 구분, 악센트 구분 안 함, 일본어 가나 구분, 전자/반자 구분|
|\_CS_AI_WS<sup>2</sup>|대/소문자 구분, 악센트 구분 안 함, 일본어 가나 구분 안 함, 전자/반자 구분|
|\_CS_AS<sup>2</sup>|대/소문자 구분, 악센트 구분, 일본어 가나 구분 안 함, 전자/반자 구분 안 함|
|\_CS_AS_KS<sup>2</sup>|대/소문자 구분, 악센트 구분, 일본어 가나 구분, 전자/반자 구분 안 함|
|\_CS_AS_KS_WS<sup>2</sup>|대/소문자 구분, 악센트 구분, 일본어 가나 구분, 전자/반자 구분|
|\_CS_AS_WS<sup>2</sup>|대/소문자 구분, 악센트 구분, 일본어 가나 구분 안 함, 전자/반자 구분|

<sup>1</sup> 이진 또는 이진 코드 포인트를 선택하면 대/소문자 구분(\_CS), 악센트 구분(\_AS), 일본어 가나 구분(\_KS) 및 전자/반자 구분(\_WS) 옵션을 사용할 수 없습니다.    

<sup>2</sup> UTF-8 옵션(\_UTF8)을 추가하면 UTF-8을 사용하여 유니코드 데이터를 인코딩할 수 있습니다. 자세한 내용은 이 문서에서 [UTF-8 지원](#utf8) 섹션을 참조하세요. 

### <a name="collation-sets"></a><a name="Collation_sets"></a> 데이터 정렬 집합

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 지원하는 데이터 정렬 집합은 다음과 같습니다.    

-  [Windows 데이터 정렬](#Windows-collations)
-  [이진 데이터 정렬](#Binary-collations)
-  [SQL Server 데이터 정렬](#SQL-collations)
    
#### <a name="windows-collations"></a><a name="Windows-collations"></a> Windows 데이터 정렬    
Windows 데이터 정렬은 관련 Windows 시스템 로캘을 기반으로 하는 문자 데이터 저장 규칙을 정의합니다. Windows 데이터 정렬의 경우 유니코드 데이터 비교와 동일한 알고리즘을 사용하여 유니코드를 지원하지 않는 데이터 비교를 구현할 수 있습니다. 기본 Windows 데이터 정렬 규칙은 사전 정렬을 적용할 때 사용되는 알파벳이나 언어를 지정하며, 유니코드를 지원하지 않는 문자 데이터를 저장하는 데 사용되는 코드 페이지도 지정합니다. 유니코드 정렬과 비유니코드 정렬은 모두 특정 버전의 Windows에서 수행되는 문자열 비교와 호환됩니다. 따라서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 내의 데이터 형식에서 일관성이 유지되고, 개발자는 애플리케이션에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 사용되는 것과 동일한 규칙을 사용하여 문자열을 정렬할 수 있습니다. 자세한 내용은 [Windows 데이터 정렬 이름(Transact-SQL)](../../t-sql/statements/windows-collation-name-transact-sql.md)을 참조하세요.    
    
#### <a name="binary-collations"></a><a name="Binary-collations"></a> 이진 데이터 정렬    
이진 데이터 정렬은 로캘 및 데이터 형식으로 정의된 코딩 값 시퀀스에 따라 데이터를 정렬합니다. 대/소문자를 구분합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 이진 데이터 정렬은 사용되는 로캘과 ANSI 코드 페이지를 정의하며 이진 정렬 순서를 적용합니다. 이진 데이터 정렬은 비교적 간단하므로 애플리케이션 성능을 향상하는 데 도움이 됩니다. 유니코드를 지원하지 않는 데이터 형식의 경우 데이터 비교는 ANSI 코드 페이지에 정의된 코드 포인트를 기준으로 수행됩니다. 유니코드 데이터 형식의 경우 데이터 비교는 유니코드 코드 포인트를 기준으로 수행됩니다. 유니코드 데이터 형식에 대한 이진 데이터 정렬의 경우 데이터 정렬 시 로캘이 고려되지 않습니다. 예를 들어 **Latin_1_General_BIN** 및 **Japanese_BIN**은 유니코드 데이터에서 사용할 때 동일한 정렬 결과를 생성합니다. 자세한 내용은 [Windows 데이터 정렬 이름(Transact-SQL)](../../t-sql/statements/windows-collation-name-transact-sql.md)을 참조하세요.   
    
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에는 두 가지 이진 데이터 정렬 유형이 있습니다.

-  유니코드 데이터에 대해 불완전한 코드 포인트 간 비교를 수행한 레거시 **BIN** 데이터 정렬. 이 레거시 이진 데이터 정렬은 WCHAR로 첫 번째 문자를 비교한 후 바이트 단위 비교를 수행했습니다. BIN 데이터 정렬에서 첫 번째 문자만 코드 포인트에 따라 정렬되고 나머지 문자는 바이트 값에 따라 정렬됩니다.

-  순수형 코드 포인트 비교를 구현하는 최신 **BIN2** 데이터 정렬. BIN2 데이터 정렬에서는 모든 문자가 코드 포인트에 따라 정렬됩니다. Intel 플랫폼은 little endian 아키텍처이므로, 유니코드 문자는 항상 바이트 스왑 상태로 저장됩니다.     
    
#### <a name="sql-server-collations"></a><a name="SQL-collations"></a> SQL Server 데이터 정렬    
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 정렬(SQL_\*)은 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]와 정렬 순서가 호환됩니다. 유니코드를 지원하지 않는 데이터에 대한 사전 정렬 규칙은 Windows 운영 체제에서 제공하는 정렬 루틴과 호환되지 않지만, 유니코드 데이터의 정렬은 특정 버전의 Windows 정렬 규칙과 호환됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 정렬은 비유니코드 데이터와 유니코드 데이터에 대해 다른 비교 규칙을 사용하므로 기본 데이터 형식에 따라 동일한 데이터에 대한 비교 결과가 달라집니다. 자세한 내용은 [SQL Server 데이터 정렬 이름(Transact-SQL)](../../t-sql/statements/sql-server-collation-name-transact-sql.md)을 참조하세요. 

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 설치하는 동안 기본 설치 데이터 정렬 설정은 OS(운영 체제) 로캘에 의해 결정됩니다. 설치 전에 OS 로캘을 변경하거나 설치 중에 변경하여 서버 수준 데이터 정렬을 변경할 수 있습니다. 이전 버전과의 호환성을 위해 기본 데이터 정렬은 각 특정 로캘에서 사용 가능한 가장 오래된 버전으로 설정됩니다. 따라서 권장되는 데이터 정렬이 아닐 수도 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기능을 활용하려면 Windows 데이터 정렬을 사용하기 위한 기본 설치 설정을 변경하세요. 예를 들어 OS 로캘 “영어(미국)”(코드 페이지 1252)의 경우 설치 중의 기본 데이터 정렬은 **SQL_Latin1_General_CP1_CI_AS**이고 가장 가까운 Windows 데이터 정렬인 **Latin1_General_100_CI_AS_SC**로 변경될 수 있습니다.
    
> [!NOTE]    
> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 영어 인스턴스를 업그레이드하는 경우, 기존 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스와의 호환성을 위해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 정렬(SQL_\*)을 지정할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 기본 데이터 정렬은 설치 중에 정의되므로 다음 조건에 해당하는 경우 데이터 정렬 설정을 신중하게 지정해야 합니다.    
>     
> -   애플리케이션 코드가 이전 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 정렬의 동작에 의존할 경우    
> -   여러 언어를 반영하는 문자 데이터를 저장해야 하는 경우    
    
### <a name="collation-levels"></a><a name="Collation_levels"></a> 데이터 정렬 수준
다음 수준의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에서 데이터 정렬을 설정할 수 있습니다.    

-  [서버 수준 데이터 정렬](#Server-level-collations)
-  [데이터베이스 수준 데이터 정렬](#Database-level-collations)
-  [열 수준 데이터 정렬](#Column-level-collations)
-  [식 수준 데이터 정렬](#Expression-level-collations)

#### <a name="server-level-collations"></a><a name="Server-level-collations"></a> 서버 수준 데이터 정렬   
기본 서버 데이터 정렬은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 중에 결정되며, 시스템 데이터베이스 및 모든 사용자 데이터베이스의 기본 데이터 정렬이 됩니다. 

다음 표에서는 각각의 Windows 및 SQL LCID(언어 코드 식별자)를 포함하여 OS(운영 체제) 로캘에 따라 결정되는 기본 데이터 정렬 지정을 보여 줍니다.

|Windows 로캘|Windows LCID|SQL LCID|기본 데이터 정렬|
|---------------|---------|---------|---------------|
|아프리칸스어(남아프리카 공화국)|0x0436|0x0409|Latin1_General_CI_AS|
|알바니아어(알바니아)|0x041c|0x041c|Albanian_CI_AS|
|알자스어(프랑스)|0x0484|0x0409|Latin1_General_CI_AS|
|암하라어(에티오피아)|0x045e|0x0409|Latin1_General_CI_AS|
|아랍어(알제리아)|0x1401|0x0401|Arabic_CI_AS|
|Arabic (Bahrain)|0x3c01|0x0401|Arabic_CI_AS|
|아랍어(이집트)|0x0c01|0x0401|Arabic_CI_AS|
|아랍어(이라크)|0x0801|0x0401|Arabic_CI_AS|
|아랍어(요르단)|0x2c01|0x0401|Arabic_CI_AS|
|아랍어(쿠웨이트)|0x3401|0x0401|Arabic_CI_AS|
|아랍어(레바논)|0x3001|0x0401|Arabic_CI_AS|
|아랍어(리비아)|0x1001|0x0401|Arabic_CI_AS|
|아랍어(모로코)|0x1801|0x0401|Arabic_CI_AS|
|아랍어(오만)|0x2001|0x0401|Arabic_CI_AS|
|아랍어(카타르)|0x4001|0x0401|Arabic_CI_AS|
|아랍어(사우디아라비아)|0x0401|0x0401|Arabic_CI_AS|
|아랍어(시리아)|0x2801|0x0401|Arabic_CI_AS|
|아랍어(튀니지)|0x1c01|0x0401|Arabic_CI_AS|
|아랍어(아랍에미리트)|0x3801|0x0401|Arabic_CI_AS|
|아랍어(예멘)|0x2401|0x0401|Arabic_CI_AS|
|아르메니아어(아르메니아)|0x042b|0x0419|Latin1_General_CI_AS|
|아삼어(인도)|0x044d|0x044d|서버 수준에서 사용할 수 없음|
|아제리어(아제르바이잔, 키릴 자모)|0x082c|0x082c|더 이상 사용되지 않으며 서버 수준에서 사용할 수 없음|
|아제리어(아제르바이잔, 라틴 문자)|0x042c|0x042c|더 이상 사용되지 않으며 서버 수준에서 사용할 수 없음|
|바슈키르어(러시아)|0x046d|0x046d|Latin1_General_CI_AI|
|바스크어(바스크)|0x042d|0x0409|Latin1_General_CI_AS|
|벨로루시어(벨로루시)|0x0423|0x0419|Cyrillic_General_CI_AS|
|벵골어(방글라데시)|0x0845|0x0445|서버 수준에서 사용할 수 없음|
|벵골어(인도)|0x0445|0x0439|서버 수준에서 사용할 수 없음|
|보스니아어(보스니아 헤르체고비나, 키릴 자모)|0x201a|0x201a|Latin1_General_CI_AI|
|보스니아어(보스니아 헤르체고비나, 라틴 문자)|0x141a|0x141a|Latin1_General_CI_AI|
|브르타뉴어(프랑스)|0x047e|0x047e|Latin1_General_CI_AI|
|불가리아어(불가리아)|0x0402|0x0419|Cyrillic_General_CI_AS|
|카탈로니아어(카탈로니아)|0x0403|0x0409|Latin1_General_CI_AS|
|중국어(홍콩 특별 행정구, 중국)|0x0c04|0x0404|Chinese_Taiwan_Stroke_CI_AS|
|중국어(마카오 특별 행정구)|0x1404|0x1404|Latin1_General_CI_AI|
|중국어(마카오)|0x21404|0x21404|Latin1_General_CI_AI|
|중국어(중국)|0x0804|0x0804|Chinese_PRC_CI_AS|
|중국어(중국)|0x20804|0x20804|Chinese_PRC_Stroke_CI_AS|
|중국어(싱가포르)|0x1004|0x0804|Chinese_PRC_CI_AS|
|중국어(싱가포르)|0x21004|0x20804|Chinese_PRC_Stroke_CI_AS|
|중국어(대만)|0x30404|0x30404|Chinese_Taiwan_Bopomofo_CI_AS|
|중국어(대만)|0x0404|0x0404|Chinese_Taiwan_Stroke_CI_AS|
|코르시카어(프랑스)|0x0483|0x0483|Latin1_General_CI_AI|
|크로아티아어(보스니아 헤르체고비나, 라틴 문자)|0x101a|0x041a|Croatian_CI_AS|
|크로아티아어(크로아티아)|0x041a|0x041a|Croatian_CI_AS|
|체코어(체코)|0x0405|0x0405|Czech_CI_AS|
|덴마크어(덴마크)|0x0406|0x0406|Danish_Norwegian_CI_AS|
|다리어(아프가니스탄)|0x048c|0x048c|Latin1_General_CI_AI|
|디베히어(몰디브)|0x0465|0x0465|서버 수준에서 사용할 수 없음|
|네덜란드어(벨기에)|0x0813|0x0409|Latin1_General_CI_AS|
|네덜란드어(네덜란드)|0x0413|0x0409|Latin1_General_CI_AS|
|영어(오스트레일리아)|0x0c09|0x0409|Latin1_General_CI_AS|
|영어(벨리즈)|0x2809|0x0409|Latin1_General_CI_AS|
|영어(캐나다)|0x1009|0x0409|Latin1_General_CI_AS|
|영어(카리브 해)|0x2409|0x0409|Latin1_General_CI_AS|
|영어(인도)|0x4009|0x0409|Latin1_General_CI_AS|
|영어(아일랜드)|0x1809|0x0409|Latin1_General_CI_AS|
|영어(자메이카)|0x2009|0x0409|Latin1_General_CI_AS|
|영어(말레이시아)|0x4409|0x0409|Latin1_General_CI_AS|
|영어(뉴질랜드)|0x1409|0x0409|Latin1_General_CI_AS|
|영어(필리핀)|0x3409|0x0409|Latin1_General_CI_AS|
|영어(싱가포르)|0x4809|0x0409|Latin1_General_CI_AS|
|영어(남아프리카)|0x1c09|0x0409|Latin1_General_CI_AS|
|영어(트리니다드 토바고)|0x2c09|0x0409|Latin1_General_CI_AS|
|영어(영국)|0x0809|0x0409|Latin1_General_CI_AS|
|영어(미국)|0x0409|0x0409|SQL_Latin1_General_CP1_CI_AS|
|영어(짐바브웨)|0x3009|0x0409|Latin1_General_CI_AS|
|에스토니아어(에스토니아)|0x0425|0x0425|Estonian_CI_AS|
|페로어(페로 제도)|0x0438|0x0409|Latin1_General_CI_AS|
|필리핀어(필리핀)|0x0464|0x0409|Latin1_General_CI_AS|
|핀란드어(핀란드)|0x040b|0x040b|Finnish_Swedish_CI_AS|
|프랑스어(벨기에)|0x080c|0x040c|French_CI_AS|
|프랑스어(캐나다)|0x0c0c|0x040c|French_CI_AS|
|프랑스어(프랑스)|0x040c|0x040c|French_CI_AS|
|프랑스어(룩셈부르크)|0x140c|0x040c|French_CI_AS|
|프랑스어(모나코)|0x180c|0x040c|French_CI_AS|
|프랑스어(스위스)|0x100c|0x040c|French_CI_AS|
|프리지아어(네덜란드)|0x0462|0x0462|Latin1_General_CI_AI|
|갈리시아어(스페인)|0x0456|0x0409|Latin1_General_CI_AS|
|조지아어(조지아)|0x10437|0x10437|Georgian_Modern_Sort_CI_AS|
|조지아어(조지아)|0x0437|0x0419|Latin1_General_CI_AS|
|독일어 - 전화 번호부 정렬(DIN)|0x10407|0x10407|German_PhoneBook_CI_AS|
|독일어(오스트리아)|0x0c07|0x0409|Latin1_General_CI_AS|
|독일어(독일)|0x0407|0x0409|Latin1_General_CI_AS|
|독일어(리히텐슈타인)|0x1407|0x0409|Latin1_General_CI_AS|
|독일어(룩셈부르크)|0x1007|0x0409|Latin1_General_CI_AS|
|독일어(스위스)|0x0807|0x0409|Latin1_General_CI_AS|
|그리스어(그리스)|0x0408|0x0408|Greek_CI_AS|
|그린란드어(그린란드)|0x046f|0x0406|Danish_Norwegian_CI_AS|
|구자라트어(인도)|0x0447|0x0439|서버 수준에서 사용할 수 없음|
|하우사어(나이지리아, 라틴 문자)|0x0468|0x0409|Latin1_General_CI_AS|
|히브리어(이스라엘)|0x040d|0x040d|Hebrew_CI_AS|
|힌디어(인도)|0x0439|0x0439|서버 수준에서 사용할 수 없음|
|헝가리어(헝가리)|0x040e|0x040e|Hungarian_CI_AS|
|헝가리어의 기술적인 정렬|0x1040e|0x1040e|Hungarian_Technical_CI_AS|
|아이슬란드어(아이슬란드)|0x040f|0x040f|Icelandic_CI_AS|
|이그보어(나이지리아)|0x0470|0x0409|Latin1_General_CI_AS|
|인도네시아어(인도네시아)|0x0421|0x0409|Latin1_General_CI_AS|
|이눅티투트어(캐나다, 라틴 문자)|0x085d|0x0409|Latin1_General_CI_AS|
|이눅티투트어(캐나다 음절)|0x045d|0x045d|Latin1_General_CI_AI|
|아일랜드어(아일랜드)|0x083c|0x0409|Latin1_General_CI_AS|
|이탈리아어(이탈리아)|0x0410|0x0409|Latin1_General_CI_AS|
|이탈리아어(스위스)|0x0810|0x0409|Latin1_General_CI_AS|
|일본어(일본 XJIS)|0x0411|0x0411|Japanese_CI_AS|
|일본어(일본)|0x040411|0x40411|Latin1_General_CI_AI|
|칸나다어(인도)|0x044b|0x0439|서버 수준에서 사용할 수 없음|
|카자흐어(카자흐스탄)|0x043f|0x043f|Kazakh_90_CI_AS|
|크메르어(캄보디아)|0x0453|0x0453|서버 수준에서 사용할 수 없음|
|끼체어(과테말라)|0x0486|0x0c0a|Modern_Spanish_CI_AS|
|키냐르완다어(르완다)|0x0487|0x0409|Latin1_General_CI_AS|
|코카니어(인도)|0x0457|0x0439|서버 수준에서 사용할 수 없음|
|한국어(한국어 사전 정렬)|0x0412|0x0412|Korean_Wansung_CI_AS|
|키르기스어(키르기스스탄)|0x0440|0x0419|Cyrillic_General_CI_AS|
|라오어(라오스)|0x0454|0x0454|서버 수준에서 사용할 수 없음|
|라트비아어(라트비아)|0x0426|0x0426|Latvian_CI_AS|
|리투아니아어(리투아니아)|0x0427|0x0427|Lithuanian_CI_AS|
|저지 소르비아어(독일)|0x082e|0x0409|Latin1_General_CI_AS|
|룩셈부르크어(룩셈부르크)|0x046e|0x0409|Latin1_General_CI_AS|
|마케도니아어(북마케도니아)|0x042f|0x042f|Macedonian_FYROM_90_CI_AS|
|말레이어(브루나이)|0x083e|0x0409|Latin1_General_CI_AS|
|말레이어(말레이시아)|0x043e|0x0409|Latin1_General_CI_AS|
|말라얄람어(인도)|0x044c|0x0439|서버 수준에서 사용할 수 없음|
|몰타어(몰타)|0x043a|0x043a|Latin1_General_CI_AI|
|마오리어(뉴질랜드)|0x0481|0x0481|Latin1_General_CI_AI|
|마푸둥군어(칠레)|0x047a|0x047a|Latin1_General_CI_AI|
|마라티어(인도)|0x044e|0x0439|서버 수준에서 사용할 수 없음|
|모호크어(모호크)|0x047c|0x047c|Latin1_General_CI_AI|
|몽골어(몽골)|0x0450|0x0419|Cyrillic_General_CI_AS|
|몽골어(중국)|0x0850|0x0419|Cyrillic_General_CI_AS|
|네팔어(네팔)|0x0461|0x0461|서버 수준에서 사용할 수 없음|
|노르웨이어(복말)(노르웨이)|0x0414|0x0414|Latin1_General_CI_AI|
|노르웨이어(니노르스크)(노르웨이)|0x0814|0x0414|Latin1_General_CI_AI|
|오크어(프랑스)|0x0482|0x040c|French_CI_AS|
|오리야어(인도)|0x0448|0x0439|서버 수준에서 사용할 수 없음|
|파슈토어(아프가니스탄)|0x0463|0x0463|서버 수준에서 사용할 수 없음|
|페르시아어(이란)|0x0429|0x0429|Latin1_General_CI_AI|
|폴란드어(폴란드)|0x0415|0x0415|Polish_CI_AS|
|포르투갈어(브라질)|0x0416|0x0409|Latin1_General_CI_AS|
|포르투갈어(포르투갈)|0x0816|0x0409|Latin1_General_CI_AS|
|펀잡어(인도)|0x0446|0x0439|서버 수준에서 사용할 수 없음|
|케추아어(볼리비아)|0x046b|0x0409|Latin1_General_CI_AS|
|케추아어(에콰도르)|0x086b|0x0409|Latin1_General_CI_AS|
|케추아어(페루)|0x0c6b|0x0409|Latin1_General_CI_AS|
|루마니아어(루마니아)|0x0418|0x0418|Romanian_CI_AS|
|로만시어(스위스)|0x0417|0x0417|Latin1_General_CI_AI|
|러시아어(러시아)|0x0419|0x0419|Cyrillic_General_CI_AS|
|이나리 라프어(핀란드)|0x243b|0x083b|Latin1_General_CI_AI|
|룰레 라프어(노르웨이)|0x103b|0x043b|Latin1_General_CI_AI|
|룰레 라프어(스웨덴)|0x143b|0x083b|Latin1_General_CI_AI|
|북부 라프어(핀란드)|0x0c3b|0x083b|Latin1_General_CI_AI|
|북부 라프어(노르웨이)|0x043b|0x043b|Latin1_General_CI_AI|
|북부 라프어(스웨덴)|0x083b|0x083b|Latin1_General_CI_AI|
|스콜트 라프어(핀란드)|0x203b|0x083b|Latin1_General_CI_AI|
|남부 라프어(노르웨이)|0x183b|0x043b|Latin1_General_CI_AI|
|남부 라프어(스웨덴)|0x1c3b|0x083b|Latin1_General_CI_AI|
|산스크리트어(인도)|0x044f|0x0439|서버 수준에서 사용할 수 없음|
|세르비아어(보스니아 헤르체고비나, 키릴 자모)|0x1c1a|0x0c1a|Latin1_General_CI_AI|
|세르비아어(보스니아 헤르체고비나, 라틴 문자)|0x181a|0x081a|Latin1_General_CI_AI|
|세르비아어(세르비아, 키릴 자모)|0x0c1a|0x0c1a|Latin1_General_CI_AI|
|세르비아어(세르비아, 라틴 문자)|0x081a|0x081a|Latin1_General_CI_AI|
|세소토 사 레보아어/북부 소토어(남아프리카)|0x046c|0x0409|Latin1_General_CI_AS|
|세츠와나어/츠와나어(남아프리카)|0x0432|0x0409|Latin1_General_CI_AS|
|스리랑카어(스리랑카)|0x045b|0x0439|서버 수준에서 사용할 수 없음|
|슬로바키아어(슬로바키아)|0x041b|0x041b|Slovak_CI_AS|
|슬로베니아어(슬로베니아)|0x0424|0x0424|Slovenian_CI_AS|
|스페인어(아르헨티나)|0x2c0a|0x0c0a|Modern_Spanish_CI_AS|
|스페인어(볼리비아)|0x400a|0x0c0a|Modern_Spanish_CI_AS|
|스페인어(칠레)|0x340a|0x0c0a|Modern_Spanish_CI_AS|
|스페인어(콜롬비아)|0x240a|0x0c0a|Modern_Spanish_CI_AS|
|스페인어(코스타리카)|0x140a|0x0c0a|Modern_Spanish_CI_AS|
|스페인어(도미니카 공화국)|0x1c0a|0x0c0a|Modern_Spanish_CI_AS|
|스페인어(에콰도르)|0x300a|0x0c0a|Modern_Spanish_CI_AS|
|스페인어(엘살바도르)|0x440a|0x0c0a|Modern_Spanish_CI_AS|
|스페인어(과테말라)|0x100a|0x0c0a|Modern_Spanish_CI_AS|
|스페인어(온두라스)|0x480a|0x0c0a|Modern_Spanish_CI_AS|
|스페인어(멕시코)|0x080a|0x0c0a|Modern_Spanish_CI_AS|
|스페인어(니카라과)|0x4c0a|0x0c0a|Modern_Spanish_CI_AS|
|스페인어(파나마)|0x180a|0x0c0a|Modern_Spanish_CI_AS|
|스페인어(파라과이)|0x3c0a|0x0c0a|Modern_Spanish_CI_AS|
|스페인어(페루)|0x280a|0x0c0a|Modern_Spanish_CI_AS|
|스페인어(푸에르토리코)|0x500a|0x0c0a|Modern_Spanish_CI_AS|
|스페인어(스페인)|0x0c0a|0x0c0a|Modern_Spanish_CI_AS|
|스페인어(스페인, 전통 정렬)|0x040a|0x040a|Traditional_Spanish_CI_AS|
|스페인어(미국)|0x540a|0x0409|Latin1_General_CI_AS|
|스페인어(우루과이)|0x380a|0x0c0a|Modern_Spanish_CI_AS|
|스페인어(베네수엘라)|0x200a|0x0c0a|Modern_Spanish_CI_AS|
|스와힐리어(케냐)|0x0441|0x0409|Latin1_General_CI_AS|
|스웨덴어(핀란드)|0x081d|0x040b|Finnish_Swedish_CI_AS|
|스웨덴어(스웨덴)|0x041d|0x040b|Finnish_Swedish_CI_AS|
|시리아어(시리아)|0x045a|0x045a|서버 수준에서 사용할 수 없음|
|타지크어(타지키스탄)|0x0428|0x0419|Cyrillic_General_CI_AS|
|타마지트어(알레리, 라틴 문자)|0x085f|0x085f|Latin1_General_CI_AI|
|타밀어(인도)|0x0449|0x0439|서버 수준에서 사용할 수 없음|
|타타르어(러시아)|0x0444|0x0444|Cyrillic_General_CI_AS|
|텔루구어(인도)|0x044a|0x0439|서버 수준에서 사용할 수 없음|
|태국어(태국)|0x041e|0x041e|Thai_CI_AS|
|티베트어(중국)|0x0451|0x0451|서버 수준에서 사용할 수 없음|
|터키어(터키)|0x041f|0x041f|Turkish_CI_AS|
|투르크멘어(투르크메니스탄)|0x0442|0x0442|Latin1_General_CI_AI|
|위구르어(중국)|0x0480|0x0480|Latin1_General_CI_AI|
|우크라이나어(우크라이나)|0x0422|0x0422|Ukrainian_CI_AS|
|고지 소르비아어(독일)|0x042e|0x042e|Latin1_General_CI_AI|
|우르두어(파키스탄)|0x0420|0x0420|Latin1_General_CI_AI|
|우즈베크어(우즈베키스탄, 키릴 자모)|0x0843|0x0419|Cyrillic_General_CI_AS|
|우즈베크어(우즈베키스탄, 라틴 문자)|0x0443|0x0443|Uzbek_Latin_90_CI_AS|
|베트남어(베트남)|0x042a|0x042a|Vietnamese_CI_AS|
|웨일스어(영국)|0x0452|0x0452|Latin1_General_CI_AI|
|월로프어(세네갈)|0x0488|0x040c|French_CI_AS|
|코사어(남아프리카)|0x0434|0x0409|Latin1_General_CI_AS|
|야쿠트어(러시아)|0x0485|0x0485|Latin1_General_CI_AI|
|이 문자(중국)|0x0478|0x0409|Latin1_General_CI_AS|
|요루바어(나이지리아)|0x046a|0x0409|Latin1_General_CI_AS|
|줄루어(남아프리카)|0x0435|0x0409|Latin1_General_CI_AS|

> [!NOTE]
> 유니코드 전용 데이터 정렬은 서버 수준 데이터 정렬로 지원되지 않으므로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 중에 선택할 수 없습니다.    
    
서버에 데이터 정렬을 할당한 후에 데이터 정렬을 변경하려면 모든 데이터베이스 개체와 데이터를 내보내고 *master* 데이터베이스를 다시 빌드한 다음, 모든 데이터베이스 개체와 데이터를 다시 가져와야 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 기본 데이터 정렬을 변경하는 대신 새 데이터베이스 또는 데이터베이스 열을 만들 때 원하는 데이터 정렬을 지정할 수 있습니다.    

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대한 서버 데이터 정렬을 쿼리하려면 `SERVERPROPERTY` 함수를 사용합니다.

```sql
SELECT CONVERT(varchar, SERVERPROPERTY('collation'));
```

서버에서 사용 가능한 모든 데이터 정렬을 쿼리하려면 다음 `fn_helpcollations()` 기본 제공 함수를 사용합니다.

```sql
SELECT * FROM sys.fn_helpcollations();
```
    
#### <a name="database-level-collations"></a><a name="Database-level-collations"></a> 데이터베이스 수준 데이터 정렬    
데이터베이스를 만들거나 수정할 때 `CREATE DATABASE` 또는 `ALTER DATABASE` 문의 `COLLATE` 절을 사용하여 기본 데이터베이스 데이터 정렬을 지정할 수 있습니다. 데이터 정렬을 지정하지 않으면 데이터베이스에 서버 데이터 정렬이 할당됩니다.    
    
서버의 데이터 정렬을 변경하는 경우에만 시스템 데이터베이스의 데이터 정렬을 변경할 수 있습니다.
    
데이터베이스 데이터 정렬은 데이터베이스의 모든 메타데이터에 사용되며, 이 데이터 정렬이 데이터베이스에 사용되는 모든 문자열 열, 임시 개체, 변수 이름 및 기타 모든 문자열의 기본값이 됩니다. 사용자 데이터베이스의 데이터 정렬을 변경할 경우 데이터베이스 액세스 임시 테이블에서 쿼리할 때 데이터 정렬 충돌이 발생할 수 있습니다. 임시 테이블은 항상 *tempdb* 시스템 데이터베이스에 저장되므로, 인스턴스에 대한 데이터 정렬을 사용합니다. 사용자 데이터베이스와 *tempdb* 간의 문자 데이터를 비교하는 쿼리를 실행할 경우 문자 데이터를 평가할 때 데이터 정렬이 충돌하면 쿼리가 실패할 수 있습니다. 쿼리에 `COLLATE` 절을 지정하면 이 문제를 해결할 수 있습니다. 자세한 내용은 [COLLATE(Transact-SQL)](~/t-sql/statements/collations.md)를 참조하세요.    

> [!NOTE]
> [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]에서 데이터베이스를 만든 후에는 데이터 정렬을 변경할 수 없습니다.

사용자 데이터베이스의 데이터 정렬은 다음과 같은 `ALTER DATABASE` 문을 사용하여 변경할 수 있습니다.

```sql
ALTER DATABASE myDB COLLATE Greek_CS_AI;
```

> [!IMPORTANT]
> 데이터베이스 수준 데이터 정렬을 변경해도 열 수준 또는 식 수준 데이터 정렬은 영향을 받지 않습니다.

데이터베이스의 현재 데이터 정렬은 다음과 같은 문을 사용하여 검색할 수 있습니다.

```sql
SELECT CONVERT (VARCHAR(50), DATABASEPROPERTYEX('database_name','collation'));
```

#### <a name="column-level-collations"></a><a name="Column-level-collations"></a> 열 수준 데이터 정렬    
테이블을 만들거나 변경할 때 `COLLATE` 절을 사용하여 각 문자열 열의 데이터 정렬을 지정할 수 있습니다. 데이터 정렬을 지정하지 않으면 데이터베이스의 기본 데이터 정렬이 열에 할당됩니다.    

열의 데이터 정렬은 다음과 같은 `ALTER TABLE` 문을 사용하여 변경할 수 있습니다.

```sql
ALTER TABLE myTable ALTER COLUMN mycol NVARCHAR(10) COLLATE Greek_CS_AI;
```
    
#### <a name="expression-level-collations"></a><a name="Expression-level-collations"></a> 식 수준 데이터 정렬    
식 수준 데이터 정렬은 문이 실행될 때 설정되며 결과 집합이 반환되는 방식에 영향을 줍니다. 따라서 `ORDER BY` 정렬 결과를 로캘별로 다르게 표시할 수 있습니다. 식 수준 데이터 정렬을 구현하려면 다음과 같은 `COLLATE` 절을 사용합니다.    
    
```sql    
SELECT name FROM customer ORDER BY name COLLATE Latin1_General_CS_AI;    
```    
    
###  <a name="locale"></a><a name="Locale_Defn"></a> 로캘    
로캘은 위치나 문화권과 관련된 정보 집합입니다. 정보에는 음성 언어의 이름과 식별자, 언어를 기록하는 데 사용되는 스크립트, 문화권별 규칙 등이 포함될 수 있습니다. 데이터 정렬은 하나 이상의 로캘과 연결될 수 있습니다. 자세한 내용은 참조 [Microsoft에 의해 할당되는 로캘 ID](https://msdn.microsoft.com/goglobal/bb964664.aspx)를 참조하세요.    
    
###  <a name="code-page"></a><a name="Code_Page_Defn"></a> 코드 페이지    
코드 페이지는 지정한 스크립트의 각 문자와 연결된 숫자 인덱스 또는 코드 포인트 값을 정렬한 문자 집합입니다. Windows 코드 페이지는 일반적으로 ‘문자 집합’ 또는 *charset*이라고 합니다.  코드 페이지는 여러 다른 Windows 시스템 로캘에 사용되는 문자 집합과 자판 배열을 지원하는 데 사용됩니다.     
 
###  <a name="sort-order"></a><a name="Sort_Order_Defn"></a> 정렬 순서    
정렬 순서는 데이터 값이 정렬되는 방식을 지정합니다. 순서는 데이터 비교 결과에 영향을 줍니다. 데이터는 데이터 정렬을 사용하여 정렬되며 인덱스를 사용하여 데이터 정렬을 최적화할 수 있습니다.    
    
##  <a name="unicode-support"></a><a name="Unicode_Defn"></a> 유니코드 지원    
유니코드는 코드 포인트를 문자에 매핑하기 위한 표준입니다. 유니코드는 전 세계 모든 언어의 모든 문자를 지원하도록 설계되었으므로, 문자 집합마다 다른 코드 페이지로 처리하지 않아도 됩니다.

### <a name="unicode-basics"></a>유니코드 기본 사항
문자 데이터와 코드 페이지만 사용할 때 한 데이터베이스에 여러 언어의 데이터를 저장하면 이를 관리하기가 어렵습니다. 필요한 언어별 문자를 모두 저장할 수 있는 하나의 데이터베이스 코드 페이지를 찾기도 어렵습니다. 또한 다양한 코드 페이지를 실행하는 여러 클라이언트가 읽거나 업데이트하는 경우 특수 문자의 올바른 변환을 보장하기 어렵습니다. 여러 언어의 클라이언트를 지원하는 데이터베이스는 항상 비유니코드 데이터 형식 대신 유니코드 데이터 형식을 사용해야 합니다.

예를 들어 다음 세 가지 주요 언어를 처리해야 하는 북아메리카 고객 데이터베이스가 있다고 가정합니다.

-  멕시코에서 사용할 스페인어 이름 및 주소
-  퀘벡에서 사용할 프랑스어 이름 및 주소
-  캐나다 및 미국에서 사용할 영어 이름 및 주소

문자 열과 코드 페이지만 사용하는 경우 세 가지 언어의 문자를 모두 처리할 코드 페이지와 함께 데이터베이스를 설치해야 합니다. 또한 다른 언어의 코드 페이지를 실행하는 클라이언트에서 읽을 때 언어의 문자를 올바르게 변환해야 합니다.
   
> [!NOTE]
> 클라이언트가 사용하는 코드 페이지는 OS(운영 체제) 설정에 따라 결정됩니다. Windows 운영 체제에서 클라이언트 코드 페이지를 설정하려면 제어판의 **국가별 설정** 을 사용하세요.    

전 세계 대상 그룹이 요구하는 모든 문자를 지원할 문자 데이터 형식 코드 페이지를 선택하기란 어렵습니다. 국제 데이터베이스에서 문자 데이터를 관리하는 가장 쉬운 방법은 항상 유니코드를 지원하는 데이터 형식을 사용하는 것입니다. 

### <a name="unicode-data-types"></a>유니코드 데이터 형식
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]([!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이상)에서 여러 언어를 반영하는 문자 데이터를 저장할 경우에는 유니코드를 지원하지 않는 데이터 형식(**char**, **varchar**, and **text**) 대신 항상 유니코드 데이터 형식(**nchar**, **nvarchar** 및 **ntext**)을 사용하세요. 

> [!NOTE]
> 유니코드 데이터 형식의 경우 [!INCLUDE[ssde_md](../../includes/ssde_md.md)]에서 UCS-2를 사용하여 최대 65,535자 또는 보조 문자를 사용할 경우 전체 유니코드 범위(1,114,111자)를 나타낼 수 있습니다. 보조 문자를 사용하도록 설정하는 방법에 대한 자세한 내용은 [보조 문자](#Supplementary_Characters)를 참조하세요.

또는 [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]부터 UTF-8 지원 데이터 정렬(\_UTF8)을 사용하는 경우 유니코드를 지원하지 않는 기존 데이터 형식(**char** 및 **varchar**)이 UTF-8 인코딩을 사용하는 유니코드 데이터 형식이 됩니다. [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]에서는 기존 유니코드 데이터 형식(**nchar**, **nvarchar** 및 **ntext**)의 동작이 변경되지 않으며 계속해서 UCS-2 또는 UTF-16 인코딩을 사용합니다. 자세한 내용은 [UTF-8과 UTF-16 간의 스토리지 차이점](#storage_differences)을 참조하세요.

### <a name="unicode-considerations"></a>유니코드 고려 사항
비유니코드 데이터 형식에는 여러 가지 제한 사항이 있습니다. 유니코드를 지원하지 않는 컴퓨터는 단일 코드 페이지만 사용할 수 있기 때문입니다. 유니코드를 사용하면 코드 페이지 변환의 필요성이 줄어들기 때문에 성능이 향상될 수 있습니다. 유니코드 데이터 정렬은 서버 수준에서 지원되지 않으므로 데이터베이스, 열 또는 식 수준에서 개별적으로 선택해야 합니다.    

서버에서 클라이언트로 데이터를 이동할 때는 기존 클라이언트 드라이버에서 서버 데이터 정렬을 인식하지 못할 수 있습니다. 유니코드 서버에서 비유니코드 클라이언트로 데이터를 이동할 때 이러한 현상이 나타날 수 있습니다. 클라이언트 운영 체제를 업그레이드하여 기본 시스템 데이터 정렬을 업데이트하는 것이 가장 좋은 방법입니다. 클라이언트에 데이터베이스 클라이언트 소프트웨어가 설치되어 있는 경우에는 해당 데이터베이스 클라이언트 소프트웨어에 서비스 업데이트를 적용하는 것도 좋습니다.    
    
> [!TIP]
> 또한 서버의 데이터에 대해 다른 데이터 정렬을 사용할 수도 있습니다. 클라이언트의 코드 페이지에 매핑되는 데이터 정렬을 선택하세요.    
>
> 일부 유니코드 문자의 검색 및 정렬 성능을 향상하기 위해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상)에서 제공되는 UTF-16 데이터 정렬(Windows 데이터 정렬만 해당)을 사용하려면, 보조 문자(\_SC) 데이터 정렬 중 하나 또는 버전 140 데이터 정렬 중 하나를 선택할 수 있습니다.    
 
[!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]에서 제공되는 UTF-8 데이터 정렬을 사용하고 일부 유니코드 문자의 검색 및 정렬을 향상하려면(Windows 데이터 정렬만 해당), UTF-8 인코딩 지원 데이터 정렬(\_UTF8)을 선택해야 합니다.
 
-   UTF8 플래그는 다음에 적용할 수 있습니다.    
    -   보충 문자(\_SC) 또는 변형 선택기 구분(\_VSS) 인식을 이미 지원하는 언어적 데이터 정렬
    -   BIN2<sup>1</sup> 이진 데이터 정렬
    
-   UTF8 플래그는 다음에 적용할 수 없습니다.    
    -   보충 문자(\_SC) 또는 변형 선택기 구분(\_VSS) 인식을 지원하지 않는 언어적 데이터 정렬
    -   BIN 또는 BIN2<sup>2</sup> 이진 데이터 정렬
    -   SQL\_* 데이터 정렬  
    
<sup>1</sup>[!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] CTP 2.3부터 지원됩니다. [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] CTP 3.0에서는 **UTF8_BIN2** 데이터 정렬이 **Latin1_General_100_BIN2_UTF8**로 바뀌었습니다.        
<sup>2</sup>[!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] CTP 2.3까지 지원됩니다.    
    
유니코드 데이터 형식 또는 비유니코드 데이터 형식 사용과 관련된 문제점을 평가하려면 작업 시나리오를 테스트하여 사용자 환경에서 나타나는 성능 차이를 측정하세요. 조직 전반의 시스템에 사용되는 데이터 정렬을 표준화하고, 가능한 경우 항상 유니코드 서버와 클라이언트를 배포하는 것이 좋습니다.    
    
대부분의 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 다른 서버나 클라이언트와 상호 작용하며, 조직에서 애플리케이션과 서버 인스턴스 간에 여러 데이터 액세스 표준을 사용할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 클라이언트는 다음의 두 가지 주요 유형 중 하나에 해당됩니다.    
    
-   OLE DB 및 ODBC(Open Database Connectivity) 버전 3.7 이상을 사용하는 **유니코드 클라이언트**    
-   ODBC 버전 3.6 또는 이전 버전과 DB-Library를 사용하는 **유니코드를 지원하지 않는 클라이언트**    
    
다음 표에서는 유니코드 서버와 유니코드를 지원하지 않는 서버의 다양한 결합에서 다국어 데이터를 사용하는 방법을 설명합니다.    
    
|서버|Client|이점 또는 제한 사항|    
|------------|------------|-----------------------------|    
|Unicode|Unicode|유니코드 데이터는 시스템 전체에서 사용되므로 이 시나리오는 검색한 데이터가 손상되지 않는 등 최상의 성능을 제공합니다. ADO(ActiveX Data Objects), OLE DB 및 ODBC 버전 3.7 이상이 여기에 해당됩니다.|    
|Unicode|비유니코드|이 시나리오에서, 특히 새로운 운영 체제를 실행하는 서버와 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 이전 운영 체제를 실행하는 클라이언트 간의 연결에서는 데이터를 클라이언트 컴퓨터로 이동할 때 제한 사항 또는 오류가 발생할 수 있습니다. 서버의 유니코드 데이터는 데이터 변환을 위해 비유니코드 클라이언트의 해당 코드 페이지에 매핑을 시도합니다.|    
|비유니코드|Unicode|다국어 데이터 사용에 적합한 구성이 아닙니다. 유니코드 데이터를 유니코드를 지원하지 않는 서버에 쓸 수 없습니다. 서버의 코드 페이지를 벗어나는 서버로 데이터를 보낼 때 문제가 발생할 수 있습니다.|    
|비유니코드|비유니코드|다국어 데이터를 사용할 때 가장 제한이 많은 시나리오입니다. 단일 코드 페이지만 사용할 수 있습니다.|    
    
##  <a name="supplementary-characters"></a><a name="Supplementary_Characters"></a> 보조 문자    
유니코드 컨소시엄에서는 각 문자에 000000~10FFFF 범위의 값인 고유 코드 포인트를 할당합니다. 가장 많이 사용되는 문자의 코드 포인트 값은 000000~00FFFF(65,535자) 범위이며, 메모리 및 디스크에서 8비트 또는 16비트의 한 단어에 들어갑니다. 이 범위는 일반적으로 BMP(기본 다국어 평면)로 지정됩니다. 

그러나 유니코드 컨소시엄에서는 각각 BMP와 동일한 크기인 16개의 문자 “평면”을 추가로 설정했습니다. 이 정의에 따라 유니코드는 코드 포인트 범위 000000~10FFFF 내에서 1,114,112자(즉, 2<sup>16</sup>x17자)를 나타낼 수 있습니다. 코드 포인트 값이 00FFFF보다 큰 문자에는 2~4개의 연속 8비트 단어(UTF-8) 또는 2개의 연속 16비트 단어(UTF-16)가 필요합니다. BMP 초과 범위에 있는 이러한 문자를 *보조 문자*라고 하고, 추가적인 연속 8비트 또는 16비트 단어를 *서로게이트 쌍*이라고 합니다. 보조 문자, 서로게이트, 서로게이트 쌍에 대한 자세한 내용은 [유니코드 표준](http://www.unicode.org/standard/standard.html)을 참조하세요.    

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 [!INCLUDE[ssde_md](../../includes/ssde_md.md)]에서 UCS-2를 사용하여 인코딩하는 BMP 범위(000000~00FFFF)에 유니코드 데이터를 저장하기 위해 **nchar**, **nvarchar** 등의 데이터 형식을 제공합니다. 

[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]에서 도입된 일련의 새 보조 문자(\_SC) 데이터 정렬을 **nchar**, **nvarchar** 및 **sql_variant** 데이터 형식에 사용하여 전체 유니코드 문자 범위(000000~10FFFF)를 나타낼 수 있습니다. 다음은 그 예입니다.  **Latin1_General_100_CI_AS_SC** 또는 일본어 데이터 정렬을 사용하는 경우 **Japanese_Bushu_Kakusu_100_CI_AS_SC**가 여기에 해당합니다. 
 
[!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]에서는 새로운 UTF-8 지원 데이터 정렬([\_UTF8](#utf8))을 사용하는 **char** 및 **varchar** 데이터 형식까지 보조 문자 지원을 확장합니다. 이 데이터 형식도 전체 유니코드 문자 범위를 나타낼 수 있습니다.   

> [!NOTE]
> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]부터 새로운 모든 \_140 데이터 정렬에서 자동으로 보조 문자를 지원합니다.

보조 문자를 사용하는 경우    
    
-   데이터 정렬 버전 90 이상에서 정렬 및 비교 연산에 보조 문자를 사용할 수 있습니다.    
-   버전 100 데이터 정렬은 모두 보조 문자를 사용한 언어적 정렬을 지원합니다.    
-   데이터베이스 개체 이름 등의 메타데이터에는 보조 문자를 사용할 수 없습니다.    
-   SC 플래그는 다음에 적용할 수 있습니다.    
    -   버전 90 데이터 정렬    
    -   버전 100 데이터 정렬    
    
-   SC 플래그는 다음에 적용할 수 없습니다.    
    -   버전 80 버전이 지정되지 않은 Windows 데이터 정렬    
    -   BIN 또는 BIN2 이진 데이터 정렬    
    -   SQL\* 데이터 정렬    
    -   버전 140 데이터 정렬(이미 보조 문자를 지원하기 때문에 SC 플래그가 필요하지 않음)    
    
다음 표에서는 보조 문자를 SCA(보조 문자 인식) 데이터 정렬과 함께 사용할 경우와 그렇지 않을 때 일부 문자열 함수 및 문자열 연산자의 동작을 비교합니다.    
    
|문자열 함수 또는 연산자|SCA 데이터 정렬 사용|SCA 데이터 정렬 사용 안 함|    
|---------------------------------|--------------------------|-----------------------------|    
|[CHARINDEX](../../t-sql/functions/charindex-transact-sql.md)<br /><br /> [LEN](../../t-sql/functions/len-transact-sql.md)<br /><br /> [PATINDEX](../../t-sql/functions/patindex-transact-sql.md)|UTF-16 서로게이트 쌍이 단일 코드 포인트로 계산됩니다.|UTF-16 서로게이트 쌍이 두 개의 코드 포인트로 계산됩니다.|    
|[LEFT](../../t-sql/functions/left-transact-sql.md)<br /><br /> [REPLACE](../../t-sql/functions/replace-transact-sql.md)<br /><br /> [REVERSE](../../t-sql/functions/reverse-transact-sql.md)<br /><br /> [RIGHT](../../t-sql/functions/right-transact-sql.md)<br /><br /> [SUBSTRING](../../t-sql/functions/substring-transact-sql.md)<br /><br /> [STUFF](../../t-sql/functions/stuff-transact-sql.md)|함수가 각 서로게이트 쌍을 단일 코드 포인트로 처리하며 올바르게 작동합니다.|함수가 서로게이트 쌍을 분할하여 예기치 않은 결과가 발생할 수 있습니다.|    
|[NCHAR](../../t-sql/functions/nchar-transact-sql.md)|0~0x10FFFF 범위의 지정된 유니코드 코드 포인트 값에 해당하는 문자를 반환합니다. 지정된 값이 0~0xFFFF 범위에 있을 경우 하나의 문자가 반환됩니다. 값이 더 높을 경우 해당 서로게이트가 반환됩니다.|0xFFFF보다 큰 값은 해당 서로게이트 대신 NULL을 반환합니다.|    
|[UNICODE](../../t-sql/functions/unicode-transact-sql.md)|0~0x10FFFF 범위의 UTF-16 코드 포인트를 반환합니다.|0~0xFFFF 범위의 UCS-2 코드 포인트를 반환합니다.|    
|[와일드카드 - 문자 하나와 일치](../../t-sql/language-elements/wildcard-match-one-character-transact-sql.md)<br /><br /> [와일드카드 - 일치하지 않는 문자](../../t-sql/language-elements/wildcard-character-s-not-to-match-transact-sql.md)|모든 와일드카드 연산에 보조 문자를 사용할 수 있습니다.|이러한 와일드카드 연산에 보조 문자를 사용할 수 없습니다. 다른 와일드카드 연산자는 사용할 수 있습니다.|    
    
## <a name="gb18030-support"></a><a name="GB18030"></a> GB18030 지원    
GB18030은 중국에서 사용하는 별개의 중국어 인코딩 표준입니다. GB18030에서 문자 길이는 1바이트, 2바이트 또는 4바이트일 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 서버가 클라이언트 쪽 애플리케이션으로부터 GB18030으로 인코딩된 문자를 받을 때 해당 문자를 인식하고 유니코드 문자로 기본 변환 및 저장하는 방식으로 GB18030 문자를 지원합니다. 이렇게 변환된 문자는 서버에 저장된 후 모든 후속 작업에서 유니코드 문자로 처리됩니다. 

모든 중국어 데이터 정렬(가급적 최신 100 버전)을 사용할 수 있습니다. 모든 \_100 수준 데이터 정렬은 GB18030 문자를 사용한 언어적 정렬을 지원합니다. 데이터에 보조 문자(서로게이트 쌍)가 포함되어 있는 경우 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 제공되는 SC 데이터 정렬을 사용하여 검색 및 정렬 성능을 향상할 수 있습니다.    

> [!NOTE]
> [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 등의 클라이언트 도구가 Dengxian 글꼴을 사용하여 GB18030 인코딩된 문자를 포함하는 문자열을 올바르게 표시하는지 확인합니다.
    
## <a name="complex-script-support"></a><a name="Complex_script"></a> 복합 스크립트 지원    
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 복합 스크립트를 입력, 저장, 변경 및 표시할 수 있습니다. 복합 스크립트에는 다음 형식이 포함됩니다.    
    
-   아랍어 텍스트와 영어 텍스트의 조합과 같은 오른쪽에서 왼쪽으로 쓰는 텍스트와 왼쪽에서 오른쪽으로 쓰는 텍스트의 조합을 포함하는 양방향 텍스트    
-   아랍어, 인도어, 태국어 문자와 같이 위치에 따라 문자 모양이 바뀌거나 다른 문자와 함께 사용되면 문자 모양이 바뀌는 양방향 텍스트    
-   태국어와 같이 단어 사이를 구분하는 공백이 없어 단어 인식을 위해 내부 사전이 필요한 언어    
    
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 와 상호 작용하는 데이터베이스 애플리케이션은 복합 스크립트를 지원하는 컨트롤을 사용해야 합니다. 관리형 코드로 생성된 표준 Windows 폼 컨트롤에서는 복합 스크립트를 사용할 수 있습니다.    

## <a name="japanese-collations-added-in--sssqlv14_md"></a><a name="Japanese_Collations"></a> 일본어 데이터 정렬이 [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]에 추가됨
 
[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]부터 다양한 옵션(\_CS, \_AS, \_KS, \_WS, \_VSS)의 순열을 사용하여 새 일본어 데이터 정렬 패밀리가 지원됩니다. 

이러한 데이터 정렬을 나열하기 위해 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]을 쿼리할 수 있습니다.      

```sql 
SELECT Name, Description FROM fn_helpcollations()  
WHERE Name LIKE 'Japanese_Bushu_Kakusu_140%' OR Name LIKE 'Japanese_XJIS_140%'
``` 

새 데이터 정렬은 모두 보조 문자를 기본적으로 지원하므로 새 **\_140** 데이터 정렬에 SC 플래그가 없거나 필요하지 않습니다.

이러한 데이터 정렬은 [!INCLUDE[ssde_md](../../includes/ssde_md.md)] 인덱스, 메모리 최적화 테이블, columnstore 인덱스 및 고유하게 컴파일된 모듈에서 지원됩니다.

<a name="ctp23"></a>

## <a name="utf-8-support"></a><a name="utf8"></a> UTF-8 지원
[!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]에서는 가져오기 또는 내보내기 인코딩 및 문자열 데이터의 데이터베이스 수준 또는 열 수준 데이터 정렬로 널리 사용되는 UTF-8 문자 인코딩이 완벽하게 지원됩니다. UTF-8은 **char** 및 **varchar** 데이터 형식에서 허용되며, *UTF8* 접미사가 있는 데이터 정렬을 만들거나 개체의 데이터 정렬을 이 데이터 정렬로 변경하면 사용할 수 있습니다. 예를 들어 **LATIN1_GENERAL_100_CI_AS_SC**를 **LATIN1_GENERAL_100_CI_AS_SC_UTF8**로 변경하는 경우가 여기에 해당합니다. 

UTF-8은 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]에서 도입된 보조 문자를 지원하는 Windows 데이터 정렬에서만 사용할 수 있습니다. **nchar** 및 **nvarchar** 데이터 형식은 UCS-2 또는 UTF-16 인코딩만 허용하며 변경되지 않고 그대로 유지됩니다.

### <a name="storage-differences-between-utf-8-and-utf-16"></a><a name="storage_differences"></a> UTF-8과 UTF-16 간의 스토리지 차이점
유니코드 컨소시엄에서는 각 문자에 000000~10FFFF 범위의 값인 고유 코드 포인트를 할당합니다. [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]에서는 UTF-8 및 UTF-16 인코딩을 모두 사용해서 전체 범위를 나타낼 수 있습니다.    
-  UTF-8 인코딩에서는 ASCII 범위(000000~00007F)의 문자에 1바이트가 필요하고, 코드 포인트 000080~0007FF에 2바이트가 필요하며, 코드 포인트 000800~00FFFF에 3바이트가 필요하고, 코드 포인트 0010000~0010FFFF에 4바이트가 필요합니다. 
-  UTF-16 인코딩에서는 코드 포인트 000000~00FFFF에 2바이트가 필요하고, 코드 포인트 0010000~0010FFFF에 4바이트가 필요합니다. 

다음 표에는 각 문자 범위와 인코딩 형식의 인코딩 스토리지 크기(바이트)가 나와 있습니다.

|코드 범위(16진수)|코드 범위(10진수)|UTF-8의 스토리지 크기(바이트)<sup>1</sup>|UTF-16의 스토리지 크기(바이트)<sup>1</sup>|    
|---------------------------------|---------------------------------|--------------------------|-----------------------------|   
|000000~00007F|0~127|1|2|
|000080~00009F<br />0000A0~0003FF<br />000400~0007FF|128~159<br />160~1,023<br />1,024~2,047|2|2|
|000800~003FFF<br />004000~00FFFF|2,048~16,383<br />16,384~65,535|3|2|
|010000~03FFFF<sup>2</sup><br /><br />040000~10FFFF<sup>2</sup>|65,536~262,143<sup>2</sup><br /><br />262,144~1,114,111<sup>2</sup>|4|4|

<sup>1</sup> ‘스토리지 크기(바이트)’는 인코딩된 바이트 길이를 가리키며, 데이터 형식의 디스크 스토리지 크기가 아닙니다.  디스크 스토리지 크기에 대한 자세한 내용은 [nchar 및 nvarchar](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md) 및 [char 및 varchar](../../t-sql/data-types/char-and-varchar-transact-sql.md)를 참조하세요.

<sup>2</sup>[보조 문자](#Supplementary_Characters)의 코드 포인트 범위입니다.

> [!TIP]   
> [CHAR(*n*) 및 VARCHAR(*n*)](../../t-sql/data-types/char-and-varchar-transact-sql.md) 또는 [NCHAR(*n*) 및 NVARCHAR(*n*)](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md)에서 *n*이 문자 수를 정의한다고 잘못 생각하는 경우가 많습니다. CHAR(10) 열의 예제에서 **Latin1_General_100_CI_AI**와 같은 데이터 정렬을 사용하여 0~127 범위의 ASCII 문자 10자를 저장할 수 있기 때문입니다. 이 범위의 각 문자는 1바이트만 사용합니다.
>    
> 그러나 [CHAR(*n*) 및 VARCHAR(*n*)](../../t-sql/data-types/char-and-varchar-transact-sql.md)의 *n*은 ‘바이트’(0~8,000) 단위로 문자열 크기를 정의하고, [NCHAR(*n*) 및 NVARCHAR(*n*)](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md)의 *n*은 ‘바이트 쌍’(0~4,000)으로 문자열 크기를 정의합니다.   *n*은 저장할 수 있는 문자 수를 정의하지 않습니다.

방금 확인한 것처럼, 적절한 유니코드 인코딩과 데이터 형식을 선택하면 사용 중인 문자 집합에 따라 스토리지 비용을 훨씬 절감하거나 현재 스토리지 공간을 늘릴 수 있습니다. 예를 들어 **Latin1_General_100_CI_AI_SC_UTF8**과 같은 UTF-8 지원 라틴어 데이터 정렬을 사용하는 경우 `CHAR(10)` 열은 10바이트를 저장하며, 0~127 범위의 ASCII 문자 10자를 포함할 수 있습니다. 그러나 128~2047 범위는 5자, 2048~65535 범위는 3자만 포함할 수 있습니다. 반면, `NCHAR(10)` 열은 10바이트 쌍(20바이트)을 저장하기 때문에 0~65535 범위의 문자 10자를 포함할 수 있습니다.  

데이터베이스나 열에 UTF-8 또는 UTF-16 인코딩을 사용할지 여부를 선택하기 전에 저장되는 문자열 데이터의 분포를 고려합니다.
-  대체로 ASCII 범위 0~127을 사용하는 경우(예: 영어), UTF-8에서는 각 문자에 1바이트, UTF-16에서는 2바이트가 필요합니다. UTF-8을 사용하는 것이 스토리지 측면에서 효율적입니다. UTF-8 지원 데이터 정렬을 사용하여 0~127 범위의 ASCII 문자를 포함하는 기존 열 데이터 형식을 `NCHAR(10)`에서 `CHAR(10)`로 변경하면 스토리지 요구 사항이 50% 감소합니다. 이러한 감소는 `NCHAR(10)`는 스토리지로 20바이트가 필요하지만 `CHAR(10)`는 동일한 유니코드 문자열 표현에 10바이트만 필요하기 때문입니다.    
-  ASCII 범위를 초과하는 거의 모든 라틴어 기반 스크립트와 그리스어, 키릴 자모, 콥트어, 아르메니아어, 히브리어, 아랍어, 시리아어, 타나 문자, 은코 문자는 UTF-8과 UTF-16에서 모두, 문자당 2바이트가 필요합니다. 이러한 경우에는 비교 가능한 데이터 형식 간(예: **char** 또는 **nchar** 사용 간)에 큰 스토리지 차이가 없습니다.
-  대체로 동아시아 스크립트인 경우(예: 한국어, 중국어, 일본어), UTF-8에서는 각 문자에 3바이트, UTF-16에서는 2바이트가 필요합니다. UTF-16을 사용하는 것이 스토리지 측면에서 효율적입니다. 
-  010000~10FFFF 범위의 문자는 UTF-8과 UTF-16에서 모두, 4바이트가 필요합니다. 이러한 경우에는 비교 가능한 데이터 형식 간(예: **char** 또는 **nchar** 사용 간)에 스토리지 차이가 없습니다.

다른 고려 사항은 [국가별 Transact-SQL 문 작성](../../relational-databases/collations/write-international-transact-sql-statements.md)을 참조하세요.

### <a name="converting-to-utf-8"></a><a name="converting"></a> UTF-8로 변환
[CHAR(*n*) 및 VARCHAR(*n*)](../../t-sql/data-types/char-and-varchar-transact-sql.md)에서 또는 [NCHAR(*n*) 및 NVARCHAR(*n*)](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md)에서 *n*은 저장할 수 있는 문자 수가 아니라 스토리지 크기(바이트)를 정의하므로 데이터 잘림을 방지하기 위해 변환해야 하는 데이터 형식 크기를 결정하는 것이 중요합니다. 

예를 들어 180바이트의 일본어 문자를 저장하는 **NVARCHAR(100)** 으로 정의된 열이 있다고 가정합니다. 이 예에서 열 데이터는 현재 문자당 2바이트를 사용하는 UCS-2 또는 UTF-16을 사용하여 인코딩됩니다. 새 데이터 형식은 200바이트만 저장할 수 있지만 일본어 문자는 UTF-8로 인코딩된 경우 3바이트가 필요하기 때문에 열 유형을 **VARCHAR(200)** 으로 변환하면 데이터가 잘릴 수 있습니다. 따라서 데이터 잘림을 통한 데이터 손실을 방지하려면 열을 **VARCHAR(270)** 으로 정의해야 합니다.

따라서 기존 데이터를 UTF-8로 변환하기 전에 열 정의에 대한 예상 바이트 크기를 미리 파악하고 이에 따라 새 데이터 형식 크기를 조정해야 합니다. [DATALENGTH](../../t-sql/functions/datalength-transact-sql.md) 함수 및 [COLLATE](../../t-sql/statements/collations.md) 문을 사용하여 기존 데이터베이스에서 UTF-8 변환 작업에 대한 올바른 데이터 길이 요구 사항을 결정하는 [데이터 샘플 GitHub](https://github.com/microsoft/sql-server-samples/blob/master/samples/features/unicode)에서 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트 또는 SQL Notebook을 참조하세요.

기존 테이블에서 열 데이터 정렬 및 데이터 형식을 변경하려면 [열 데이터 정렬 설정 또는 변경](../../relational-databases/collations/set-or-change-the-column-collation.md)에 설명된 방법 중 하나를 사용합니다.

데이터베이스 데이터 정렬을 변경하여 새 개체가 기본적으로 데이터베이스 데이터 정렬을 상속하도록 허용하거나 서버 데이터 정렬을 변경하여 새 데이터베이스가 기본적으로 시스템 데이터 정렬을 상속하도록 허용하려면 이 문서의 [관련 작업](#Related_Tasks) 섹션을 참조하세요. 

##  <a name="related-tasks"></a><a name="Related_Tasks"></a> Related tasks    
    
|Task|항목|    
|----------|-----------|    
|SQL Server 인스턴스의 데이터 정렬을 설정하거나 변경하는 방법에 대해 설명합니다. 서버 데이터 정렬을 변경해도 기존 사용자 데이터베이스의 데이터 정렬은 변경되지 않습니다.|[서버 데이터 정렬 설정 또는 변경](../../relational-databases/collations/set-or-change-the-server-collation.md)|    
|사용자 데이터베이스의 데이터 정렬을 설정하거나 변경하는 방법에 대해 설명합니다. 데이터베이스 데이터 정렬을 변경해도 기존 테이블 열의 데이터 정렬은 변경되지 않습니다.|[데이터베이스 데이터 정렬 설정 또는 변경](../../relational-databases/collations/set-or-change-the-database-collation.md)|    
|데이터베이스 열의 데이터 정렬을 설정하거나 변경하는 방법을 설명합니다.|[열 데이터 정렬 설정 또는 변경](../../relational-databases/collations/set-or-change-the-column-collation.md)|    
|서버, 데이터베이스 또는 열 수준에서 데이터 정렬 정보를 반환하는 방법을 설명합니다.|[데이터 정렬 정보 보기](../../relational-databases/collations/view-collation-information.md)|    
|특정 언어에서 다른 언어로 이식성이 향상되고 여러 언어를 더욱 쉽게 지원하도록 Transact-SQL 문을 작성하는 방법을 설명합니다.|[국가별 Transact-SQL 문 작성](../../relational-databases/collations/write-international-transact-sql-statements.md)|    
|날짜, 시간, 통화 데이터가 사용 및 표시되는 방식에 대한 기본 설정과 오류 메시지 언어를 변경하는 방법을 설명합니다.|[세션 언어 설정](../../relational-databases/collations/set-a-session-language.md)|    
    
##  <a name="related-content"></a><a name="Related_Content"></a> Related content    
자세한 내용은 다음 관련 콘텐츠를 참조하세요.
* [SQL Server Best Practices Collation Change](https://go.microsoft.com/fwlink/?LinkId=113891)  
* [유니코드 문자 형식을 사용하여 데이터 가져오기 및 내보내기(SQL Server)](../../relational-databases/import-export/use-unicode-character-format-to-import-or-export-data-sql-server.md)
* [국가별 Transact-SQL 문 작성](../../relational-databases/collations/write-international-transact-sql-statements.md)  
* [SQL Server 모범 사례 유니코드로 마이그레이션](https://go.microsoft.com/fwlink/?LinkId=113890)(더 이상 유지 관리되지 않음)   
* [유니코드 컨소시엄](https://go.microsoft.com/fwlink/?LinkId=48619)  
* [유니코드 표준](http://www.unicode.org/standard/standard.html)  
* [SQL Server용 OLE DB 드라이버에서 UTF-8 지원](../../connect/oledb/features/utf-8-support-in-oledb-driver-for-sql-server.md)  
* [SQL Server 데이터 정렬 이름(Transact-SQL)](../../t-sql/statements/sql-server-collation-name-transact-sql.md)  
* [Windows 데이터 정렬 이름(Transact-SQL)](../../t-sql/statements/windows-collation-name-transact-sql.md)  
* [Introducing UTF-8 support for SQL Server](https://techcommunity.microsoft.com/t5/SQL-Server/Introducing-UTF-8-support-for-SQL-Server/ba-p/734928)(SQL Server에 UTF-8 지원 도입)       
    
## <a name="see-also"></a>참고 항목    
[포함된 데이터베이스 데이터 정렬](../../relational-databases/databases/contained-database-collations.md)     
[전체 텍스트 인덱스 생성 시 언어 선택](../../relational-databases/search/choose-a-language-when-creating-a-full-text-index.md)     
[sys.fn_helpcollations(Transact-SQL)](../../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md)       
[싱글바이트 및 멀티바이트 문자 집합](https://docs.microsoft.com/cpp/c-runtime-library/single-byte-and-multibyte-character-sets)      
 
