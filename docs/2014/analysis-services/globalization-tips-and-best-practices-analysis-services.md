---
title: 세계화 팁과 모범 사례 (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- translations [Analysis Services], client applications
- date comparisons
- day-of-week comparisons [Analysis Services]
- time [Analysis Services]
- month comparisons [Analysis Services]
ms.assetid: 71a8c438-1370-4c69-961e-d067ee4e47c2
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 026c1bf822a6493c6605128582f7142178ad6776
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48188263"
---
# <a name="globalization-tips-and-best-practices-analysis-services"></a>세계화 팁과 모범 사례(Analysis Services)
  **[!INCLUDE[applies](../includes/applies-md.md)]**  다차원 전용  
  
 다음의 팁 및 지침은 비즈니스 인텔리전스 솔루션의 이식성을 향상시키고 언어 및 데이터 정렬 설정과 직접적으로 관련이 있는 오류를 방지하는 데 유용할 수 있습니다.  
  
-   [스택 전체에서 유사한 데이터 정렬 사용](#bkmk_sameColl)  
  
-   [일반적인 데이터 정렬 권장 사항](#bkmk_recos)  
  
-   [개체 식별자의 대/소문자 구분](#bkmk_objid)  
  
-   [Excel 및 SQL Server Profiler를 사용한 로캘 테스트](#bkmk_test)  
  
-   [번역이 들어 있는 솔루션에서 MDX 쿼리 작성](#bkmk_mdx)  
  
-   [날짜 및 시간 값이 들어 있는 MDX 쿼리 작성](#bkmk_datetime)  
  
##  <a name="bkmk_sameColl"></a> 스택 전체에서 유사한 데이터 정렬 사용  
 가능하면 데이터베이스 엔진에 사용하는 것과 동일한 데이터 정렬 설정을 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 에서 사용하여 전자/반자 구분 및 대/소문자 구분과 액세스 민감도를 일치시키도록 하세요.  
  
 각 서비스에는 데이터베이스 엔진의 기본값이 SQL_Latin1_General_CP1_CI_AS로 설정되어 있고 Analysis Services가 Latin1_General_AS로 설정되어 있는 자체 데이터 정렬 설정이 있습니다. 기본값은 대/소문자, 전자/반자 및 악센트 구분 측면에서 호환됩니다. 두 데이터 정렬 중 하나의 설정을 변경하는 경우 데이터 정렬 속성이 기본 방법에서 벗어나면 문제가 발생할 수 있습니다.  
  
 데이터 정렬 설정이 기능적으로 동일한 경우에도 문자열 내 빈 공백이 각 서비스에 의해 다르게 해석되는 특별한 경우가 발생할 수 있습니다.  
  
 공백 문자는 유니코드에서 싱글바이트(SBCS)나 더블바이트 문자 집합(DBCS)으로 표현될 수 있으므로 '특별한 경우'입니다. 관계형 엔진에서 공백으로 구분되는 두 개의 복합 문자열(SBCS를 사용하는 문자열과 DBCS 문자열)은 동일한 것으로 간주됩니다. Analysis Services에서는 처리하는 동안 동일한 두 개의 복합 문자열이 동일하지 않고 두 번째 인스턴스는 중복으로 표시됩니다.  
  
 자세한 내용과 권장 해결 방법에 대해 알려면 [유니코드 문자열의 공백에 데이터 정렬을 기반으로 한 서로 다른 처리 결과가 있는 경우](http://social.technet.microsoft.com/wiki/contents/articles/23979.ssas-processing-error-blanks-in-a-unicode-string-have-different-processing-outcomes-based-on-collation-and-character-set.aspx)(영문)를 참조하세요.  
  
##  <a name="bkmk_recos"></a> 일반적인 데이터 정렬 권장 사항  
 Analysis Services에서는 항상 모든 사용 가능한 언어 및 데이터 정렬의 전체 목록을 제공하며, 선택된 언어에 따라 데이터 정렬을 필터링하지 않습니다. 실행 가능한 조합을 선택해야 합니다.  
  
 자주 사용되는 일부 데이터 정렬이 다음 목록에 나와 있습니다.  
  
 이 목록은 다른 옵션을 제외하는 분명한 권장 사항이 아니라 추가 조사의 시작점으로 고려해야 합니다. 특별히 권장되지 않는 데이터 정렬이 데이터에 가장 적합한 데이터 정렬임을 알 수 있습니다. 철저한 테스트는 데이터 값이 적절히 정렬 및 비교되는지 확인하는 유일한 방법입니다. 항상 데이터 정렬을 테스트할 때 처리 및 쿼리 작업을 둘 다 실행해야 합니다.  
  
-   Latin1_General_100_AS는 [ISO 기본 라틴어 알파벳](http://en.wikipedia.org/wiki/ISO_basic_Latin_alphabet)의 26자를 사용하는 애플리케이션에 종종 사용됩니다.  
  
-   스칸디나비아어 문자(예: ø)를 포함하는 북부 유럽 언어에는 Finnish_Swedish_100을 사용할 수 있습니다.  
  
-   러시아어 같은 동부 유럽 언어에는 종종 Cyrillic_General_100을 사용합니다.  
  
-   중국어 언어 및 데이터 정렬은 지역에 따라 달라지지만 일반적으로 중국어 언어 또는 중국어 번체의 하나입니다.  
  
     PRC 및 싱가포르에서 Microsoft 지원은 중국어 간체를 한어병음과 함께 기본 정렬 순서로 확인하는 경향이 있습니다. 권장 데이터 정렬은 Chinese_PRC(SQL Server 2000), Chinese_PRC_90(SQL Server 2005) 또는 Chinese_Simplified_Pinyin_100(SQL Server 2008 이상)입니다.  
  
     대만에서는 획수에 따른 권장 정렬 순서 Chinese_Taiwan_Stroke(SQL Server 2000), Chinese_Taiwan_Stroke_90(SQL Server 2005) 또는 Chinese_Traditional_Stroke_Count_100(SQL Server 2008 이상)으로 중국어 번체를 확인하는 것이 더 일반적입니다.  
  
     다른 지역(예: 홍콩 특별 행정구 및 마카오 특별 행정구)에서는 중국어 번체도 사용합니다. 홍콩에서는 데이터 정렬로 Chinese_Hong_Kong_Stroke_90(SQL Server 2005)을 확인하는 것이 일반적입니다. 마카오 특별 행정구에서는 Chinese_Traditional_Stroke_Count_100(SQL Server 2008 이상)이 자주 사용됩니다.  
  
-   일본어에서 가장 자주 사용되는 데이터 정렬은 Japanese_CI_AS입니다. Japanese_XJIS_100은 [JIS2004](http://en.wikipedia.org/wiki/JIS_X_0213)를 지원하는 설치에서 사용됩니다. Japanese_BIN2는 일반적으로 Windows 이외의 플랫폼에서 또는 SQL Server 관계형 데이터베이스 엔진 이외의 데이터 원본에서 가져온 데이터를 사용한 데이터 마이그레이션 프로젝트에서 확인됩니다.  
  
     Japanese_Bushu_Kakusu_100은 Analysis Services 작업을 실행하는 서버에서 거의 확인되지 않습니다.  
  
-   Korean_100은 한국어에 대해 권장됩니다. Korean_Wansung_Unicode도 목록에 있지만 더 이상 사용되지 않습니다.  
  
##  <a name="bkmk_objid"></a> 개체 식별자의 대/소문자 구분  
 SQL Server 2012 SP2부터는 개체 ID의 대/소문자 구분이 데이터 정렬과 관계없이 적용됩니다. 하지만 동작은 언어에 따라 다릅니다.  
  
|언어 스크립트|대/소문자 구분|  
|---------------------|----------------------|  
|**기본 라틴어 알파벳**|라틴어 스크립트(26개의 영어 대문자 또는 소문자 중 사용)로 표현되는 개체 식별자는 데이터 정렬과 상관없이 대/소문자를 구분하는 것으로 처리됩니다. 예를 들어, 개체 ID 54321**abcdef**, 54321**ABCDEF**, 54321**AbCdEf**는 같다고 간주됩니다. 내부적으로 Analysis Services에서는 문자열의 문자들을 모두 대문자인 것처럼 처리한 다음 언어에 상관없는 간단한 바이트 비교를 수행합니다.<br /><br /> 26개 문자에만 적용됩니다. 서부 유럽 언어에 스칸디나비아어 문자가 사용되면 추가 문자는 대문자로 처리되지 않습니다.|  
|**키릴자모, 그리스어, 콥트어, 아르메니아어**|키릴자모와 같은 비라틴 bicameral 스크립트의 개체 식별자는 항상 대/소문자 구분입니다. 예를 들어, Измерение 및 измерение은 유일한 차이점이 첫 글자의 대소문자 여부임에도 불구하고 두 개의 서로 다른 값으로 간주됩니다.|  
  
 **개체 식별자에 대한 대/소문자 구분의 의미**  
  
 개체 이름이 아니라 개체 식별자만 표에 설명된 대/소문자 구분 동작이 적용됩니다. 솔루션 작동 방식에 변화가 있는 경우(전후 비교 -- SQL Server 2012 SP2 이상 설치 후), 처리 문제가 발생할 수 있습니다. 쿼리는 개체 식별자에 의해 영향을 받지 않습니다. 두 쿼리 언어(DAX 및 MDX)에서 수식 엔진에 개체 이름(식별자 아님)이 사용됩니다.  
  
> [!NOTE]  
>  대/소문자 구분과 관련된 코드 변경 내용은 일부 애플리케이션에 대한 주요 변경 내용이었습니다. 자세한 내용은 [SQL Server 2014에서 Analysis Services 기능의 주요 변경](breaking-changes-to-analysis-services-features-in-sql-server-2014.md)을 참조하세요.  
  
##  <a name="bkmk_test"></a> Excel, SQL Server Profiler 및 SQL Server Management Studio를 사용한 로캘 테스트  
 번역을 테스트할 때 연결에서 번역의 LCID를 지정해야 합니다. [다른 언어를 SSAS에서 Excel로 가져오기](http://extremeexperts.com/sql/Tips/ExcelDiffLocale.aspx)(영문)에 설명된 대로 Excel을 사용하여 번역을 테스트할 수 있습니다.  
  
 다음 작업은 로캘 식별자 연결 문자열 속성을 포함하도록 .odc 파일을 편집하여 손으로 수행할 수 있습니다. Adventure Works 샘플 다차원 데이터베이스에서 이렇게 해보세요.  
  
-   기존 .odc 파일을 검색합니다. Adventure Works 다차원 데이터용으로 하나를 찾았으면 이 파일을 마우스 오른쪽 단추로 클릭하여 메모장에서 엽니다.  
  
-   연결 문자열에 `Locale Identifier=1036` 를 추가합니다. 파일을 저장하고 닫습니다.  
  
-   Excel | **데이터** | **기존 연결**을 엽니다. 목록을 이 컴퓨터에 있는 연결 파일로 필터링합니다. Adventure Works용 연결을 찾습니다. 이름을 주의 깊게 살펴보세요. 두 개 이상 있을 수 있습니다. 연결을 엽니다.  
  
     Adventure Works 샘플 데이터베이스에 프랑스어 번역이 표시되어야 합니다.  
  
     ![프랑스어 번역이 있는 Excel 피벗 테이블](media/ssas-localetest-excel.png "프랑스어 번역이 있는 Excel 피벗 테이블")  
  
 후속 작업으로 SQL Server Profiler를 사용하여 로캘을 확인할 수 있습니다. `Session Initialize` 이벤트를 클릭한 다음 아래의 텍스트 영역에서 속성 목록을 보고 `<localeidentifier>1036</localeidentifier>`를 찾습니다.  
  
 Management Studio에서는 서버 연결에 있는 로캘 식별자를 지정할 수 있습니다.  
  
-   개체 탐색기 | **연결** | **Analysis Services** | **옵션**에서 **추가 연결 매개 변수** 탭을 클릭합니다.  
  
-   `Local Identifier=1036` 을 입력하고 **연결**을 클릭합니다.  
  
-   Adventure Works 데이터베이스에 대해 MDX 쿼리를 실행합니다. 쿼리 결과는 프랑스어 번역이어야 합니다.  
  
     ![SSMS에서 프랑스어 번역이 있는 MDX 쿼리](media/ssas-localetest-ssms.png "SSMS에서 프랑스어 번역이 있는 MDX 쿼리")  
  
##  <a name="bkmk_mdx"></a> 번역이 들어 있는 솔루션에서 MDX 쿼리 작성  
 번역은 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 개체의 이름에 대한 표시 정보를 제공합니다. 그러나 동일 개체의 식별자는 번역되지 않습니다. 가능하면 번역된 캡션 및 이름 대신 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 개체의 식별자 및 키를 사용하십시오. 예를 들어 여러 언어 간 이식성을 위해 MDX(Multidimensional Expressions) 문 및 스크립트에 대해 멤버 이름 대신 멤버 키를 사용할 수 있습니다.  
  
> [!NOTE]  
>  테이블 형식 개체 이름은 데이터 정렬에 관계없이 항상 대/소문자를 구분한다는 점에 유의하세요. 반면에 다차원 개체 이름은 데이터 정렬의 대/소문자 구분을 따릅니다. 다차원 개체 이름만 대/소문자를 구분하므로 다차원 개체를 참조하는 모든 MDX 쿼리에 대/소문자가 올바로 사용되었는지 확인합니다.  
  
##  <a name="bkmk_datetime"></a> 날짜 및 시간 값이 들어 있는 MDX 쿼리 작성  
 여러 언어 간에 날짜 및 시간 기반 MDX 쿼리의 이식성을 높이기 위한 제안 사항은 다음과 같습니다.  
  
1.  **비교 및 작업에 숫자 부분 사용**  
  
     월 및 요일 비교 및 작업을 수행할 때 해당 문자열 대신 숫자 형식의 날짜 및 시간 부분을 사용합니다(예를 들어 MonthName 대신 MonthNumberofYear 사용). 숫자 값은 언어 번역 간 차이의 영향을 가장 적게 받습니다.  
  
2.  **결과 집합에 해당 문자열 사용**  
  
     최종 사용자에게 표시되는 결과 집합을 만들 때 다국어 고객이 제공된 번역의 혜택을 받을 수 있도록 문자열(예: MonthName) 사용을 고려해 보세요.  
  
3.  **일반적인 날짜 및 시간 정보를 위한 ISO 날짜 형식 사용**  
  
     한 [Analysis Services 전문가](http://geekswithblogs.net/darrengosbell/Default.aspx) 는 다음과 같이 추천합니다. "저는 SQL 또는 MDX 쿼리에 전달하는 날짜 문자열에 대해 항상 ISO 날짜 형식인 yyyy-mm-dd를 사용합니다. 이 형식은 명확하고 클라이언트나 서버의 국가별 설정과 관계없이 작동하기 때문입니다. 모호한 날짜 형식을 구문 분석할 때 서버는 국가별 설정을 따라야 한다는 데 동의하겠지만 또한 선택할 수 있다면 선택에 따라 해석이 달라지지 않는 것이 좋다고 생각합니다."  
  
4.  `Use the Format function to enforce a specific format, regardless of regional language settings`  
  
     포럼 게시물에서 가져온 다음의 MDX 쿼리는 형식을 사용하여 기본 국가별 설정에 관계없이 특정 형식으로 날짜를 반환하는 방법을 보여 줍니다.  
  
     원래 게시물을 보려면 [SSAS 2012가 잘못된 날짜 생성(Network Steve의 포럼 게시물)](http://www.networksteve.com/forum/topic.php/SSAS_2012_generates_invalid_dates/?TopicId=40504&Posts=2) 을 참조하세요.  
  
    ```  
    WITH MEMBER [LinkTimeAdd11Date_Manual] as Format(dateadd("d",15,"2014-12-11"), "mm/dd/yyyy")  
    member [LinkTimeAdd15Date_Manual] as Format(dateadd("d",11,"2014-12-13"), "mm/dd/yyyy")  
    SELECT  
    { [LinkTimeAdd11Date_Manual]  
    ,[LinkTimeAdd15Date_Manual]  
    }  
    ON COLUMNS   
    FROM [Adventure Works]  
  
    ```  
  
## <a name="see-also"></a>관련 항목  
 [Analysis Services 다차원에 대 한 세계화 시나리오](globalization-scenarios-for-analysis-services-multiidimensional.md)   
 [국가별 Transact-SQL 문 작성](../relational-databases/collations/write-international-transact-sql-statements.md)  
  
  
