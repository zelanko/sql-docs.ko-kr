---
title: 데이터 정렬 및 유니코드 지원 | Microsoft 문서
ms.custom: ''
ms.date: 10/18/2019
ms.prod: sql-server-2014
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
- server-level collations [SQL Server]
ms.assetid: 92d34f48-fa2b-47c5-89d3-a4c39b0f39eb
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c63b7c0d1acad34bb273e4a49921d55818965e80
ms.sourcegitcommit: 82a1ad732fb31d5fa4368c6270185c3f99827c97
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/21/2019
ms.locfileid: "72688730"
---
# <a name="collation-and-unicode-support"></a>Collation and Unicode Support
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 데이터 정렬은 데이터에 대한 정렬 규칙과 대/소문자 및 악센트 구분 속성을 제공합니다. `char` 및 `varchar`과 같은 문자 데이터 형식과 함께 사용되는 데이터 정렬은 해당 데이터 형식을 나타내는 데 사용할 수 있는 코드 페이지와 해당 문자를 지정합니다. 새 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스를 설치하든 데이터베이스 백업을 복원하든 서버를 클라이언트 데이터베이스에 연결하든 사용할 데이터의 로캘 요구 사항, 정렬 순서, 대/소문자 및 악센트 구분 여부를 파악해야 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 인스턴스에서 사용 가능한 데이터 정렬을 나열하려면 [sys를 참조하세요.fn_helpcollations &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/sys-fn-helpcollations-transact-sql)를 참조하세요.  
  
 서버, 데이터베이스, 열 또는 식에 대한 데이터 정렬을 선택하면 데이터에 일정한 특성이 부여되며, 이는 여러 데이터베이스 작업의 결과에 영향을 줍니다. 예를 들어 ORDER BY를 사용하여 쿼리를 작성할 경우 결과 집합의 정렬 순서는 쿼리의 식 수준에서 COLLATE 절에 지정되거나 데이터베이스에 적용된 데이터 정렬에 따라 달라집니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 데이터 정렬 지원을 최대한 활용하려면 이 항목에 정의된 용어와 이러한 용어가 데이터의 특성과 어떻게 관련되는지를 이해해야 합니다.  
  
  
###  <a name="Collation_Defn"></a> 데이터 정렬  
 데이터 정렬은 데이터 집합의 각 문자를 나타내는 비트 패턴을 지정합니다. 또한 데이터 정렬은 데이터를 정렬하고 비교하는 규칙을 결정합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 여러 다른 데이터 정렬을 갖는 개체를 단일 데이터베이스에 저장하도록 지원합니다. 비유니코드 열의 경우 데이터 정렬 설정은 데이터에 대한 코드 페이지와 나타낼 수 있는 문자를 지정합니다. 유니코드가 아닌 열 간에 데이터를 이동하려면 원본 코드 페이지에서 대상 코드 페이지로 변환해야 합니다.  
  
 데이터 정렬 설정이 각기 다른 데이터베이스의 컨텍스트에서[!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 실행하면 그 결과가 달라질 수 있습니다. 가능한 경우 조직에서 표준화된 데이터 정렬을 사용하세요. 그러면 모든 문자나 유니코드 식에서 명시적으로 데이터 정렬을 지정할 필요가 없습니다. 데이터 정렬 및 코드 페이지 설정이 다른 개체를 사용해야 할 경우 선행 정렬 우선 순위 규칙을 고려하도록 쿼리를 코딩하세요. 자세한 내용은 [선행 정렬 우선 순위(Transact-SQL)](/sql/t-sql/statements/collation-precedence-transact-sql)를 참조하세요.  
  
 데이터 정렬 관련 옵션에는 대/소문자 구분, 악센트 구분, 일본어 가나 구분, 전자/반자 구분이 있습니다. 이러한 옵션은 데이터 정렬 이름에 추가하여 지정됩니다. 예를 들어 이 `Japanese_Bushu_Kakusu_100_CS_AS_KS_WS` 데이터 정렬은 대/소문자, 악센트, 일본어 가나 및 전자/반자를 구분합니다. 다음 표에서는 이러한 옵션과 연결된 동작에 대해 설명합니다.  
  
|옵션|Description|  
|------------|-----------------|  
|대/소문자 구분(_CS)|대/소문자를 구분합니다. 이 정렬 순서를 선택하면 소문자가 대문자보다 먼저 정렬됩니다. 이 옵션을 선택하지 않으면 데이터 정렬에서 대/소문자를 구분하지 않습니다. 즉, SQL Server에서 정렬할 때 대문자와 소문자를 동일한 것으로 간주합니다. _CI를 지정하여 대/소문자를 구분하지 않도록 명시적으로 선택할 수 있습니다.|  
|악센트 구분(_AS)|악센트가 있는 문자와 악센트가 없는 문자를 구분합니다. 예를 들어 ' a '는 '&#x1EA5;'와 같지 않습니다. 이 옵션을 선택하지 않으면 데이터 정렬에서 악센트를 구분하지 않습니다. 즉, SQL Server에서 정렬할 때 악센트가 있는 문자와 악센트가 없는 문자를 동일한 것으로 간주합니다. _AI를 지정하여 악센트를 구분하지 않도록 명시적으로 선택할 수 있습니다.|  
|일본어 가나 구분(_KS)|일본어 가나 문자의 두 가지 유형인 히라가나와 가타가나를 구분합니다. 이 옵션을 선택하지 않으면 데이터 정렬에서 가나를 구분하지 않습니다. 즉, SQL Server에서 정렬할 때 히라가나 문자와 가타카나 문자를 동일한 것으로 간주합니다. 일본어 가나를 구분하지 않도록 지정하는 유일한 방법은 이 옵션을 생략하는 것입니다.|  
|전자/반자 구분(_WS)|전자와 반자 문자를 구분합니다. 이 옵션을 선택하지 않으면 SQL Server에서는 정렬할 때 같은 문자의 전자 표시와 반자 표시를 동일한 문자로 간주합니다. 전자/반자를 구분하지 않도록 지정하는 유일한 방법은 이 옵션을 생략하는 것입니다.|  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 지원하는 데이터 정렬 집합은 다음과 같습니다.  
  
 Windows 데이터 정렬  
 Windows 데이터 정렬은 관련 Windows 시스템 로캘을 기반으로 문자 데이터 저장 규칙을 정의합니다. Windows 데이터 정렬의 경우 유니코드 데이터를 비교할 때와 동일한 알고리즘을 사용하여 비유니코드 데이터도 비교합니다. 기본 Windows 데이터 정렬 규칙은 사전 정렬이 적용될 때 사용되는 알파벳이나 언어를 지정하고 유니코드가 아닌 문자 데이터를 저장하는 데 사용되는 코드 페이지를 지정합니다. 유니코드 정렬과 비유니코드 정렬은 모두 특정 버전의 Windows에서 수행되는 문자열 비교와 호환됩니다. 따라서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 내의 데이터 형식에서 일관성이 유지되고 개발자는 애플리케이션에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 사용되는 것과 동일한 규칙을 사용하여 문자열을 정렬할 수 있습니다. 자세한 내용은 [Windows 데이터 정렬 이름&#40;Transact-SQL&#41;](/sql/t-sql/statements/windows-collation-name-transact-sql)을 참조하세요.  
  
 이진 데이터 정렬  
 이진 데이터 정렬은 로캘 및 데이터 형식으로 정의된 코딩 값 시퀀스에 따라 데이터를 정렬합니다. 이때 대/소문자가 구분됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 이진 데이터 정렬은 사용할 로캘과 ANSI 코드 페이지를 정의하며 이진 정렬 순서를 적용합니다. 이진 데이터 정렬은 비교적 간단하므로 애플리케이션의 성능을 향상시키는 데 도움이 됩니다. 비유니코드 데이터 형식의 경우 데이터 비교는 ANSI 코드 페이지에 정의된 코드 포인트를 기준으로 수행됩니다. 유니코드 데이터 형식의 경우 데이터 비교는 유니코드 코드 포인트를 기준으로 수행됩니다. 유니코드 데이터 형식에서의 이진 데이터 정렬의 경우 데이터 정렬 시 로캘은 고려되지 않습니다. 예를 들어 Latin_1_General_BIN과 Japanese_BIN은 유니코드 데이터에서 사용할 때 동일한 정렬 결과를 생성합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에는 두 가지 유형의 이진 데이터 정렬 즉, 이전 `BIN` 데이터 정렬과 최신 `BIN2` 데이터 정렬이 있습니다. `BIN2` 데이터 정렬에서 모든 문자는 코드 포인트에 따라 정렬됩니다. `BIN` 데이터 정렬에서 첫 번째 문자만 코드 포인트에 따라 정렬되며 나머지 문자는 바이트 값에 따라 정렬됩니다. Intel 플랫폼은 little endian 아키텍처이므로, 유니코드 문자는 항상 바이트 스왑 상태로 저장됩니다.  
  
 SQL Server 데이터 정렬  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 정렬(SQL_*)은 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]와 정렬 순서가 호환됩니다. 비유니코드에 대한 사전 정렬 규칙은 Windows 운영 체제에서 제공하는 정렬 루틴과 호환되지 않지만 유니코드 데이터의 정렬은 특정 버전의 Windows 정렬 규칙과 호환됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 정렬은 비유니코드 데이터와 유니코드 데이터에 대해 다른 비교 규칙을 사용하므로 기본 데이터 형식에 따라 동일한 데이터에 대한 비교 결과가 달라집니다. 자세한 내용은 [SQL Server 데이터 정렬 이름&#40;Transact-SQL&#41;](/sql/t-sql/statements/sql-server-collation-name-transact-sql)을 참조하세요.  
  
> [!NOTE]
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 영어 인스턴스를 업그레이드할 때 기존 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스와의 호환성을 위해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 정렬(SQL_*)을 지정할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 기본 데이터 정렬은 설치 중에 정의되므로 다음 사항에 해당하는 경우 데이터 정렬 설정을 신중하게 지정해야 합니다.  
> 
>  -   애플리케이션 코드가 이전 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 정렬의 동작에 의존할 경우  
> -   여러 언어를 반영하는 문자 데이터를 저장해야 하는 경우  
  
 다음 수준의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에서 데이터 정렬을 설정할 수 있습니다.  
  
 서버 수준 데이터 정렬  
 기본 서버 데이터 정렬은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 중에 설정되며 시스템 데이터베이스 및 모든 사용자 데이터베이스의 기본 데이터 정렬이 될 수도 있습니다. 유니코드 전용 데이터 정렬은 서버 수준 데이터 정렬로 지원되지 않으므로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 중에 선택할 수 없습니다.  
  
 서버에 데이터 정렬을 할당한 후에는 데이터 정렬을 변경할 수 없습니다. 단, 모든 데이터베이스 개체와 데이터를 내보내고 `master` 데이터베이스를 다시 작성한 다음 모든 데이터베이스 개체와 데이터를 다시 가져오는 경우는 예외입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스의 기본 데이터 정렬을 변경하는 대신 새 데이터베이스 또는 데이터베이스 열을 만들 때 원하는 데이터 정렬을 지정할 수 있습니다.  
  
 데이터베이스 수준 데이터 정렬  
 데이터베이스를 만들거나 수정할 때 CREATE DATABASE 또는 ALTER DATABASE 문의 COLLATE 절을 사용하여 기본 데이터베이스 데이터 정렬을 지정할 수 있습니다. 데이터 정렬을 지정하지 않으면 데이터베이스에 서버 데이터 정렬이 할당됩니다.  
  
 서버에 대한 데이터 정렬을 변경하는 경우를 제외하고는 시스템 데이터베이스의 데이터 정렬을 변경할 수 없습니다.  
  
 데이터베이스 데이터 정렬은 데이터베이스의 모든 메타데이터에 사용되며 데이터베이스에 사용되는 모든 문자열 열, 임시 개체, 변수 이름 및 기타 모든 문자열의 기본값이 됩니다. 사용자 데이터베이스의 데이터 정렬을 변경할 경우 데이터베이스 액세스 임시 테이블에서 쿼리할 때 데이터 정렬 충돌이 발생할 수 있습니다. 임시 테이블은 항상 `tempdb` 시스템 데이터베이스에 저장되므로, 인스턴스에 대한 데이터 정렬을 사용합니다. 사용자 데이터베이스와 `tempdb` 간의 문자 데이터를 비교하는 쿼리를 실행할 경우 문자 데이터를 평가할 때 데이터 정렬이 충돌하면 쿼리가 실패할 수 있습니다. 쿼리에 COLLATE 절을 지정하여 이 문제를 해결할 수 있습니다. 자세한 내용은 [COLLATE&#40;Transact-SQL&#41;](/sql/t-sql/statements/collations)를 참조하세요.  
  
 열 수준 데이터 정렬  
 테이블을 만들거나 변경할 때 COLLATE 절을 사용하여 각 문자열 열에 대한 데이터 정렬을 지정할 수 있습니다. 데이터 정렬을 지정하지 않으면 열에 데이터베이스의 기본 데이터 정렬이 할당됩니다.  
  
 식 수준 데이터 정렬  
 식 수준 데이터 정렬은 문이 실행될 때 설정되며 결과 집합이 반환되는 방식에 영향을 줍니다. 따라서 ORDER BY 정렬 결과를 특정 로캘과 관련되게 할 수 있습니다. 다음과 같이 COLLATE 절을 사용하여 식 수준 데이터 정렬을 구현할 수 있습니다.  
  
```  
SELECT name FROM customer ORDER BY name COLLATE Latin1_General_CS_AI;  
```  
  
  
###  <a name="Locale_Defn"></a> 로캘  
 로캘은 위치나 문화권과 관련된 정보의 모음입니다. 여기에는 통용 언어의 이름과 식별자, 언어를 기록하는 데 사용되는 문자 및 문화권별 표기법 등이 포함될 수 있습니다. 데이터 정렬은 하나 이상의 로캘과 연결될 수 있습니다. 자세한 내용은 참조 [Microsoft에 의해 할당되는 로캘 ID](https://msdn.microsoft.com/goglobal/bb964664.aspx)를 참조하세요.  
  
  
###  <a name="Code_Page_Defn"></a> Code Page  
 코드 페이지는 지정한 스크립트의 각 문자와 연결된 숫자 인덱스 또는 코드 포인트 값을 정렬한 문자 집합입니다. Windows 코드 페이지는 일반적으로 *문자 집합* 또는 *charset*이라고 합니다. 코드 페이지는 여러 다른 Windows 시스템 로캘에 사용되는 문자 집합과 자판 배열을 지원하는 데 사용됩니다.  
  
  
###  <a name="Sort_Order_Defn"></a> Sort Order  
 정렬 순서는 데이터 값이 정렬되는 방식을 지정합니다. 이는 데이터 비교의 결과에 영향을 줍니다. 데이터는 데이터 정렬을 사용하여 정렬되며 인덱스를 사용하여 데이터 정렬을 최적화할 수 있습니다.  
  
  
##  <a name="Unicode_Defn"></a> 유니코드 지원  
 유니코드는 코드 포인트를 문자에 매핑하기 위한 표준입니다. 유니코드는 전 세계 모든 언어의 모든 문자를 지원하기 때문에 각 문자 집합을 처리하는 데 서로 다른 코드 페이지가 필요하지 않습니다. 여러 언어를 반영하는 문자 데이터를 저장할 경우에는 비유니코드 데이터 형식(`nchar`, `nvarchar` 및 `ntext`) 대신 항상 유니코드 데이터 형식(`char`, `varchar` 및 `text`)을 사용하세요.  
  
 비유니코드 데이터 형식에는 여러 가지 제한 사항이 있습니다. 이는 비유니코드 컴퓨터에서는 단일 코드 페이지만 사용할 수 있기 때문입니다. 유니코드를 사용하면 코드 페이지 변환이 별로 필요하지 않으므로 성능이 향상될 수 있습니다. 이러한 경우 유니코드 데이터 정렬이 서버 수준에서 지원되지 않으므로 데이터베이스, 열 또는 식 수준에서 유니코드 데이터 정렬을 개별적으로 선택해야 합니다.  
  
 클라이언트가 사용하는 코드 페이지는 운영 체제 설정에 따라 결정됩니다. Windows 운영 체제에서 클라이언트 코드 페이지를 설정하려면 제어판의 **국가별 설정** 을 사용하세요.  
  
 서버에서 클라이언트로 데이터를 이동할 때는 기존 클라이언트 드라이버에서 서버 데이터 정렬을 인식하지 못할 수 있습니다. 유니코드 서버에서 비유니코드 클라이언트로 데이터를 이동할 때 이러한 현상이 나타날 수 있습니다. 클라이언트 운영 체제를 업그레이드하여 기본 시스템 데이터 정렬을 업데이트하는 것이 가장 좋은 방법입니다. 클라이언트에 데이터베이스 클라이언트 소프트웨어가 설치되어 있는 경우에는 해당 데이터베이스 클라이언트 소프트웨어에 서비스 업데이트를 적용하는 것도 좋습니다.  
  
 또한 서버의 데이터에 대해 다른 데이터 정렬을 사용할 수도 있습니다. 클라이언트의 코드 페이지에 매핑될 데이터 정렬을 선택하세요.  
  
 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]에서 제공되는 UTF-16 데이터 정렬을 사용하기 위해 보조 문자 `_SC` 데이터 정렬(Windows 데이터 정렬만) 중 하나를 선택하여 일부 유니코드 문자의 검색 및 정렬 성능을 향상시킬 수 있습니다.  
  
 유니코드 데이터 형식 또는 비유니코드 데이터 형식 사용과 관련된 문제점을 평가하려면 작업 시나리오를 테스트하여 사용자 환경에서 나타나는 성능 차이를 측정하세요. 조직 전반의 시스템에 사용되는 데이터 정렬을 표준화하고 유니코드 서버 및 클라이언트를 배포하는 것이 좋습니다.  
  
 대부분의 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 다른 서버나 클라이언트와 상호 작용하게 되며 조직에서는 애플리케이션과 서버 인스턴스 간에 여러 데이터 액세스 표준을 사용할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 클라이언트는 다음의 두 가지 주요 유형 중 하나에 해당됩니다.  
  
-   OLE DB 및 ODBC(Open Database Connectivity) 버전 3.7 이상을 사용하는**유니코드 클라이언트**  
  
-   DB-Library 및 ODBC 버전 3.6 이하를 사용하는**유니코드를 지원하지 않는 클라이언트**  
  
 다음 표에서는 유니코드 서버 및 비유니코드 서버의 다양한 조합과 함께 다국어 데이터 사용에 대한 정보를 제공합니다.  
  
|Server|클라이언트|이점 또는 제한 사항|  
|------------|------------|-----------------------------|  
|유니코드|유니코드|유니코드 데이터는 시스템 전체에서 사용되므로 이 시나리오는 검색한 데이터가 손상되지 않는 등 최상의 성능을 제공합니다. ADO(ActiveX Data Objects), OLE DB 및 ODBC 버전 3.7 이상이 여기에 해당됩니다.|  
|유니코드|비유니코드|이 시나리오에서, 특히 새로운 운영 체제를 실행하는 서버와 이전 버전의 운영 체제에 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 실행하는 클라이언트 간의 연결에서는 데이터를 클라이언트 컴퓨터로 이동할 때 제한 사항 또는 오류가 발생할 수 있습니다. 서버의 유니코드 데이터는 데이터 변환을 위해 비유니코드 클라이언트의 해당 코드 페이지에 매핑을 시도합니다.|  
|비유니코드|유니코드|다국어 데이터를 사용할 경우 이상적인 구성이 아닙니다. 유니코드 데이터를 비유니코드 서버에 쓸 수 없습니다. 서버의 코드 페이지를 벗어나는 서버로 데이터를 보낼 때 문제가 발생할 수 있습니다.|  
|비유니코드|비유니코드|다국어 데이터를 사용할 때 가장 제한이 많은 시나리오입니다. 단일 코드 페이지만 사용할 수 있습니다.|  
  
  
##  <a name="Supplementary_Characters"></a> 보조 문자  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 `nchar` 및 `nvarchar` 유니코드 데이터를 저장 하는 데이터 형식을 제공 합니다. 이러한 데이터 형식은 텍스트를 *UTF-16*이라고 하는 형식으로 인코딩합니다. 유니코드 컨소시엄에서는 각 문자에 0x0000 ~ 0x10FFFF 범위의 값인 고유한 코드 포인트를 할당합니다. 가장 자주 사용되는 문자에는 메모리 및 디스크에서 16비트 단어로 나타날 수 있는 코드 포인트 값이 할당되지만 코드 포인트 값이 0xFFFF보다 큰 문자에는 두 개의 연속적인 16비트 단어가 필요합니다. 이러한 문자를 *보조 문자*라고 하며 두 개의 연속적인 16비트 단어는 *서로게이트 쌍*이라고 합니다.  
  
 보조 문자를 사용하는 경우  
  
-   데이터 정렬 버전 90 이상에서 정렬 및 비교 연산에 보조 문자를 사용할 수 있습니다.  
  
-   _100 수준 데이터 정렬은 모두 보조 문자를 사용한 언어적 정렬을 지원합니다.  
  
-   데이터베이스 개체 이름 같은 메타데이터에는 보조 문자를 사용할 수 없습니다.  
  
-   [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]에서 도입된 일련의 새 SC(보조 문자) 데이터 정렬을 `nchar`, `nvarchar` 및 `sql_variant` 데이터 형식에 사용할 수 있습니다. 예를 들어 `Latin1_General_100_CI_AS_SC`또는 `Japanese_Bushu_Kakusu_100_CI_AS_SC`(일본어 데이터 정렬을 사용하는 경우)를 사용합니다.  
  
     SC 플래그는 다음에 적용할 수 있습니다.  
  
    -   버전 90 Windows 데이터 정렬  
  
    -   버전 100 Windows 데이터 정렬  
  
     SC 플래그는 다음에 적용할 수 없습니다.  
  
    -   버전 80 버전이 지정되지 않은 Windows 데이터 정렬  
  
    -   BIN 또는 BIN2 이진 데이터 정렬  
  
    -   SQL* 데이터 정렬  
  
 다음 표에서는 보조 문자를 SC 데이터 정렬과 함께 사용할 경우와 그렇지 않을 때 일부 문자열 함수 및 문자열 연산자의 동작을 비교합니다.  
  
|문자열 함수 또는 연산자|SC 데이터 정렬 사용|SC 데이터 정렬 사용 안 함|  
|---------------------------------|--------------------------|-----------------------------|  
|[CHARINDEX](/sql/t-sql/functions/charindex-transact-sql)<br /><br /> [LEN](/sql/t-sql/functions/len-transact-sql)<br /><br /> [PATINDEX](/sql/t-sql/functions/patindex-transact-sql)|UTF-16 서로게이트 쌍이 단일 코드 포인트로 계산됩니다.|UTF-16 서로게이트 쌍이 두 개의 코드 포인트로 계산됩니다.|  
|[LEFT](/sql/t-sql/functions/left-transact-sql)<br /><br /> [REPLACE](/sql/t-sql/functions/replace-transact-sql)<br /><br /> [REVERSE](/sql/t-sql/functions/reverse-transact-sql)<br /><br /> [RIGHT](/sql/t-sql/functions/right-transact-sql)<br /><br /> [SUBSTRING](/sql/t-sql/functions/substring-transact-sql)<br /><br /> [STUFF](/sql/t-sql/functions/stuff-transact-sql)|함수가 각 서로게이트 쌍을 단일 코드 포인트로 처리하며 올바르게 작동합니다.|함수가 서로게이트 쌍을 분할하여 예기치 않은 결과가 발생할 수 있습니다.|  
|[NCHAR](/sql/t-sql/functions/nchar-transact-sql)|0 ~ 0x10FFFF 범위의 지정된 유니코드 코드 포인트 값에 해당하는 문자를 반환합니다. 지정된 값이 0 ~ 0xFFFF 범위에 있을 경우 하나의 문자가 반환됩니다. 값이 더 높을 경우 해당 서로게이트가 반환됩니다.|0xFFFF보다 큰 값은 해당 서로게이트 대신 NULL을 반환합니다.|  
|[UNICODE](/sql/t-sql/functions/unicode-transact-sql)|0 ~ 0x10FFFF 범위의 UTF-16 코드 포인트를 반환합니다.|0 ~ 0xFFFF 범위의 UCS-2 코드 포인트를 반환합니다.|  
|[와일드카드 - 문자 하나와 일치](/sql/t-sql/language-elements/wildcard-match-one-character-transact-sql)<br /><br /> [와일드카드 - 일치하지 않는 문자](/sql/t-sql/language-elements/wildcard-character-s-not-to-match-transact-sql)|모든 와일드카드 연산에 보조 문자를 사용할 수 있습니다.|이러한 와일드카드 연산에 보조 문자를 사용할 수 없습니다. 다른 와일드카드 연산자는 사용할 수 있습니다.|  
  
  
##  <a name="GB18030"></a> GB18030 지원  
 GB18030은 중국에서 사용하는 별개의 중국어 인코딩 표준입니다. GB18030에서 문자 길이는 1바이트, 2바이트 또는 4바이트일 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 서버가 클라이언트 쪽 애플리케이션으로부터 GB18030으로 인코딩된 문자를 받을 때 해당 문자를 인식하고 유니코드 문자로 기본 변환 및 저장하는 방식으로 GB18030 문자를 지원합니다. 이렇게 변환된 문자는 서버에 저장된 후 모든 후속 작업에서 유니코드 문자로 처리됩니다. 모든 중국어 데이터 정렬(가급적 최신 100 버전)을 사용할 수 있습니다. 모든 _100 수준 데이터 정렬은 GB18030 문자를 사용한 언어적 정렬을 지원합니다. 데이터에 보조 문자(서로게이트 쌍)가 포함되어 있는 경우 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 에서 제공되는 SC 데이터 정렬을 사용하여 검색 및 정렬 성능을 향상시킬 수 있습니다.  
  
  
##  <a name="Complex_script"></a> 복합 스크립트 지원  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 복합 스크립트를 입력, 저장, 변경 및 표시할 수 있습니다. 입력, 저장, 변경 및 표시할 수 있습니다.  
  
-   아랍어 텍스트와 영어 텍스트의 조합과 같은 오른쪽에서 왼쪽으로 쓰는 텍스트와 왼쪽에서 오른쪽으로 쓰는 텍스트의 조합을 포함하는 양방향 텍스트  
  
-   아랍어, 인도어, 태국어 문자와 같이 위치에 따라 문자 모양이 바뀌거나 다른 문자와 함께 사용되면 문자 모양이 바뀌는 양방향 텍스트  
  
-   태국어와 같이 단어 사이를 구분하는 공백이 없어 단어 인식을 위해 내부 사전이 필요한 언어  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 와 상호 작용하는 데이터베이스 애플리케이션은 복합 스크립트를 지원하는 컨트롤을 사용해야 합니다. 관리 코드로 생성되는 표준 Windows 폼 컨트롤에는 복합 스크립트 기능이 설정되어 있습니다.  
  
  
##  <a name="Related_Tasks"></a> 관련 태스크  
  
|태스크|항목|  
|----------|-----------|  
|SQL Server 인스턴스의 데이터 정렬을 설정하거나 변경하는 방법에 대해 설명합니다.|[서버 데이터 정렬 설정 또는 변경](set-or-change-the-server-collation.md)|  
|사용자 데이터베이스의 데이터 정렬을 설정하거나 변경하는 방법에 대해 설명합니다.|[데이터베이스 데이터 정렬 설정 또는 변경](set-or-change-the-database-collation.md)|  
|데이터베이스 열의 데이터 정렬을 설정하거나 변경하는 방법에 대해 설명합니다.|[열 데이터 정렬 설정 또는 변경](set-or-change-the-column-collation.md)|  
|서버, 데이터베이스 또는 열 수준에서 데이터 정렬 정보를 반환하는 방법에 대해 설명합니다.|[데이터 정렬 정보 보기](view-collation-information.md)|  
|특정 언어에서 다른 언어로 이식하거나 여러 언어를 보다 쉽게 지원하도록 Transact-SQL 문을 작성하는 방법에 대해 설명합니다.|[국가별 Transact-SQL 문 작성](write-international-transact-sql-statements.md)|  
|날짜, 시간 및 통화 데이터가 사용 및 표시되는 방식에 대한 기본 설정과 오류 메시지 언어를 변경하는 방법에 대해 설명합니다.|[세션 언어 설정](set-a-session-language.md)|  
  
  
##  <a name="Related_Content"></a> 관련 내용  
 [SQL Server Best Practices Collation Change](https://go.microsoft.com/fwlink/?LinkId=113891)  
  
 ["SQL Server Best Practices Migration to Unicode"](https://go.microsoft.com/fwlink/?LinkId=113890)  
  
 [유니코드 컨소시엄 웹 사이트](https://go.microsoft.com/fwlink/?LinkId=48619)  
  
## <a name="see-also"></a>관련 항목:  
 [Contained Database Collations](../databases/contained-database-collations.md)   
 [전체 텍스트 인덱스 생성 시 언어 선택](../search/choose-a-language-when-creating-a-full-text-index.md)   
 [sys.fn_helpcollations(Transact-SQL)](https://msdn.microsoft.com/library/ms187963(SQL.130).aspx)  
  
  
