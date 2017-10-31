---
title: "Windows 데이터 정렬 이름 (Transact SQL) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- Windows collations [SQL Server]
- names [SQL Server], collations
- collations [SQL Server], Windows collations
- Collation Designator
ms.assetid: acceef84-2c68-46e2-a021-be019b7ab14e
caps.latest.revision: 43
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7898592af503300cb1bea261d8809a81fa568155
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="windows-collation-name-transact-sql"></a>Windows 데이터 정렬 이름(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 COLLATE 절에 Windows 데이터 정렬 이름을 지정합니다. Windows 데이터 정렬 이름은 데이터 정렬 지정자와 비교 스타일로 구성됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
<Windows_collation_name> :: =   
CollationDesignator_<ComparisonStyle>  
  
<ComparisonStyle> :: =   
{ CaseSensitivity_AccentSensitivity  [ _KanatypeSensitive ] [ _WidthSensitive ]    
}  
| { _BIN | _BIN2 }  
```  
  
## <a name="arguments"></a>인수  
 *CollationDesignator*  
 Windows 데이터 정렬에 사용할 기본 데이터 정렬 규칙을 지정합니다. 기본 데이터 정렬 규칙에는 다음 사항이 포함됩니다.  
  
-   사전 정렬을 지정한 경우 적용되는 정렬 규칙. 정렬 규칙은 알파벳이나 언어를 기준으로 적용됩니다.  
  
-   비유니코드 문자 데이터를 저장하는 데 사용하는 코드 페이지  
  
 예는 다음과 같습니다.  
  
-   Latin1_General 또는 프랑스어: 둘 다 코드 페이지 1252를 사용합니다.  
  
-   터키어: 코드 페이지 1254를 사용합니다.  
  
 *CaseSensitivity*  
 **CI** 지정 대/소문자 구분, **CS** 대/소문자 구분을 지정 합니다.  
  
 *AccentSensitivity*  
 **AI** 지정 악센트 구분 안 함, **AS** 악센트 구분을 지정 합니다.  
  
 *KanatypeSensitive*  
 **생략 하면** 전자/반자 구분 안 함, 지정 **KS** 전자/반자 구분을 지정 합니다.  
  
 *WidthSensitivity*  
 **생략 하면** 너비 구분 지정 **WS** 전자/반자 구분을 지정 합니다.  
  
 **BIN**  
 이전 버전과 호환되는 이진 정렬 순서를 사용하도록 지정합니다.  
  
 **BIN2**  
 코드 포인트 비교 기능을 사용하는 이진 정렬 순서를 지정합니다.  
  
## <a name="remarks"></a>주의  
 데이터 정렬 버전에 따라 일부 코드 포인트가 정의되지 않을 수 있습니다. 예를 들어 다음을 비교해 보세요.  
  
```  
SELECT LOWER(nchar(504) COLLATE Latin1_General_CI_AS);   
SELECT LOWER (nchar(504) COLLATE Latin1_General_100_CI_AS);  
GO  
```  
  
 데이터 정렬이 Latin1_General_CI_AS인 경우 이 코드 포인트가 이 데이터 정렬에서 정의되어 있지 않으므로 첫 번째 줄은 대문자를 반환합니다.  
  
 일부 언어에서 작동하는 경우 이전 데이터 정렬을 사용하지 않는 것이 중요할 수 있습니다. 예를 들어 텔레구어의 경우 이 값은 True입니다.  
  
 일부 경우에 Windows 데이터 정렬 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 정렬은 동일한 쿼리에 대해 다른 쿼리 계획을 생성할 수 있습니다.  
  
## <a name="examples"></a>예  
 다음은 Windows 데이터 정렬 이름의 몇 가지 예입니다.  
  
-   **Latin1_General_100_**  
  
 라틴어1 일반 용어 사전 정렬 규칙, 코드 페이지 1252를 사용하는 데이터 정렬입니다. 대/소문자는 구분하지 않고 악센트를 구분합니다. 라틴어1 일반 용어 사전 정렬 규칙을 사용하고 코드 페이지 1252에 매핑되는 데이터 정렬입니다. Windows 데이터 정렬 일 경우 데이터 정렬의 버전 번호를 표시: _90 또는 _100 합니다. 대/소문자는 구분하지 않고(CI) 악센트를 구분합니다(AS).  
  
-   **Estonian_CS_AS**  
  
     에스토니아어 사전 정렬 규칙, 코드 페이지 1257을 사용하는 데이터 정렬입니다. 대/소문자를 구분하며 악센트를 구분합니다.  
  
-   **Latin1_General_BIN**  
  
     코드 페이지 1252 및 이진 정렬 규칙을 사용하는 데이터 정렬입니다. 라틴어1 일반 용어 사전 정렬 규칙은 무시됩니다.  
  
## <a name="windows-collations"></a>Windows 데이터 정렬  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 인스턴스에서 지원하는 Windows 데이터 정렬을 나열하려면 다음 쿼리를 실행합니다.  
  
```  
SELECT * FROM sys.fn_helpcollations() WHERE name NOT LIKE 'SQL%';  
```  
  
 다음 표에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 지원되는 모든 Windows 데이터 정렬을 보여 줍니다.  
  
|Windows 로캘|데이터 정렬 버전 100|데이터 정렬 버전 90|  
|--------------------|---------------------------|--------------------------|  
|알자스어(프랑스)|Latin1_General_100_|사용할 수 없음|  
|암하라어(에티오피아)|Latin1_General_100_|사용할 수 없음|  
|아르메니아어(아르메니아)|Cyrillic_General_100_|사용할 수 없음|  
|아샘어(인도)|Assamese_100_ <sup>1</sup>|사용할 수 없음|  
|바슈키르어(러시아)|Bashkir_100_|사용할 수 없음|  
|바스크어(바스크)|Latin1_General_100_|사용할 수 없음|  
|벵골어(방글라데시)|Bengali_100_<sup>1</sup>|사용할 수 없음|  
|벵골어(인도)|Bengali_100_<sup>1</sup>|사용할 수 없음|  
|보스니아어(보스니아 및 헤르체고비나, 키릴 자모)|Bosnian_Cyrillic_100_|사용할 수 없음|  
|보스니아어(보스니아 및 헤르체고비나, 라틴 문자)|Bosnian_Latin_100_|사용할 수 없음|  
|브르타뉴어(프랑스)|Breton_100_|사용할 수 없음|  
|중국어(마카오 특별 행정구)|Chinese_Traditional_Pinyin_100_|사용할 수 없음|  
|중국어(마카오 특별 행정구)|Chinese_Traditional_Stroke_Order_100_|사용할 수 없음|  
|중국어(싱가포르)|Chinese_Simplified_Stroke_Order_100_|사용할 수 없음|  
|코르시카어(프랑스)|Corsican_100_|사용할 수 없음|  
|크로아티아어(보스니아 및 헤르체고비나, 라틴 문자)|Croatian_100_|사용할 수 없음|  
|다리어(아프가니스탄)|Dari_100_|사용할 수 없음|  
|영어(인도)|Latin1_General_100_|사용할 수 없음|  
|영어(말레이시아)|Latin1_General_100_|사용할 수 없음|  
|영어(싱가포르)|Latin1_General_100_|사용할 수 없음|  
|필리핀어(필리핀)|Latin1_General_100_|사용할 수 없음|  
|프리지아어(네덜란드)|Frisian_100_|사용할 수 없음|  
|그루지야어(그루지야)|Cyrillic_General_100_|사용할 수 없음|  
|그린란드어(그린란드)|Danish_Greenlandic_100_|사용할 수 없음|  
|구자라트어(인도)|Indic_General_100_<sup>1</sup>|Indic_General_90_|  
|하우사어(나이지리아, 라틴 문자)|Latin1_General_100_|사용할 수 없음|  
|힌디어(인도)|Indic_General_100_<sup>1</sup>|Indic_General_90_|  
|이그보어(나이지리아)|Latin1_General_100_|사용할 수 없음|  
|이누크티투트어(캐나다, 라틴 문자)|Latin1_General_100_|사용할 수 없음|  
|이누크티투트어(캐나다 음절)|Latin1_General_100_|사용할 수 없음|  
|아일랜드어(아일랜드)|Latin1_General_100_|사용할 수 없음|  
|일본어(일본 XJIS)|Japanese_XJIS_100_|Japanese_90_, Japanese_|  
|일본어(일본)|Japanese_Bushu_Kakusu_100_|사용할 수 없음|  
|카나다어(인도)|Indic_General_100_<sup>1</sup>|Indic_General_90_|  
|크메르어(캄보디아)|Khmer_100_<sup>1</sup>|사용할 수 없음|  
|끼체어(과테말라)|Modern_Spanish_100_|사용할 수 없음|  
|키냐르완다어(르완다)|Latin1_General_100_|사용할 수 없음|  
|콘칸어(인도)|Indic_General_100_<sup>1</sup>|Indic_General_90_|  
|라오스어(라오스)|Lao_100_<sup>1</sup>|사용할 수 없음|  
|저소르브어(독일)|Latin1_General_100_|사용할 수 없음|  
|룩셈부르크어(룩셈부르크)|Latin1_General_100_|사용할 수 없음|  
|말라얄람어(인도)|Indic_General_100_<sup>1</sup>|사용할 수 없음|  
|몰타어(몰타)|Maltese_100_|사용할 수 없음|  
|마오리어(뉴질랜드)|Maori_100_|사용할 수 없음|  
|마푸둔군어(칠레)|Mapudungan_100_|사용할 수 없음|  
|마라티어(인도)|Indic_General_100_<sup>1</sup>|Indic_General_90_|  
|모호크어(모호크)|Mohawk_100_|사용할 수 없음|  
|몽골어(중국)|Cyrillic_General_100_|사용할 수 없음|  
|네팔어(네팔)|Nepali_100_<sup>1</sup>|사용할 수 없음|  
|노르웨이어(복말)(노르웨이)|Norwegian_100_|사용할 수 없음|  
|노르웨이어(니노르스크)(노르웨이)|Norwegian_100_|사용할 수 없음|  
|오크어(프랑스)|French_100_|사용할 수 없음|  
|오리야어(인도)|Indic_General_100_<sup>1</sup>|사용할 수 없음|  
|파슈토어(아프가니스탄)|Pashto_100_<sup>1</sup>|사용할 수 없음|  
|페르시아어(이란)|Persian_100_|사용할 수 없음|  
|펀잡어(인도)|Indic_General_100_<sup>1</sup>|Indic_General_90_|  
|케추아어(볼리비아)|Latin1_General_100_|사용할 수 없음|  
|케추아어(에콰도르)|Latin1_General_100_|사용할 수 없음|  
|케추아어(페루)|Latin1_General_100_|사용할 수 없음|  
|로망슈어(스위스)|Romansh_100_|사용할 수 없음|  
|이나리 라프어(핀란드)|Sami_Sweden_Finland_100_|사용할 수 없음|  
|룰레 라프어(노르웨이)|Sami_Norway_100_|사용할 수 없음|  
|룰레 라프어(스웨덴)|Sami_Sweden_Finland_100_|사용할 수 없음|  
|북부 라프어(핀란드)|Sami_Sweden_Finland_100_|사용할 수 없음|  
|북부 라프어(노르웨이)|Sami_Norway_100_|사용할 수 없음|  
|북부 라프어(스웨덴)|Sami_Sweden_Finland_100_|사용할 수 없음|  
|스콜트 라프어(핀란드)|Sami_Sweden_Finland_100_|사용할 수 없음|  
|남부 라프어(노르웨이)|Sami_Norway_100_|사용할 수 없음|  
|남부 라프어(스웨덴)|Sami_Sweden_Finland_100_|사용할 수 없음|  
|산스크리트어(인도)|Indic_General_100_<sup>1</sup>|Indic_General_90_|  
|세르비아어(보스니아 및 헤르체고비나, 키릴 자모)|Serbian_Cyrillic_100_|사용할 수 없음|  
|세르비아어(보스니아 및 헤르체고비나, 라틴 문자)|Serbian_Latin_100_|사용할 수 없음|  
|세르비아어(세르비아, 키릴 자모)|Serbian_Cyrillic_100_|사용할 수 없음|  
|세르비아어(세르비아, 라틴 문자)|Serbian_Latin_100_|사용할 수 없음|  
|세소토 사 레보아어/북부 소토어(남아프리카)|Latin1_General_100_|사용할 수 없음|  
|세츠와나어/츠와나어(남아프리카)|Latin1_General_100_|사용할 수 없음|  
|스리랑카어(스리랑카)|Indic_General_100_<sup>1</sup>|사용할 수 없음|  
|스와힐리어(케냐)|Latin1_General_100_|사용할 수 없음|  
|시리아어(시리아)|Syriac_100_<sup>1</sup>|Syriac_90_|  
|타지키스탄어(타지키스탄)|Cyrillic_General_100_|사용할 수 없음|  
|타마지트어(알레리, 라틴 문자)|Tamazight_100_|사용할 수 없음|  
|타밀어(인도)|Indic_General_100_<sup>1</sup>|Indic_General_90_|  
|텔루구어(인도)|Indic_General_100_<sup>1</sup>|Indic_General_90_|  
|티베트어(중국)|Tibetan_100_<sup>1</sup>|사용할 수 없음|  
|투르크멘어(투르크메니스탄)|Turkmen_100_|사용할 수 없음|  
|위구르어(중국)|Uighur_100_|사용할 수 없음|  
|고소르브어(독일)|Upper_Sorbian_100_|사용할 수 없음|  
|우르두어(파키스탄)|Urdu_100_|사용할 수 없음|  
|웨일스어(영국)|Welsh_100_|사용할 수 없음|  
|월라프어(세네갈)|French_100_|사용할 수 없음|  
|코사어(남아프리카)|Latin1_General_100_|사용할 수 없음|  
|야쿠트어(러시아)|Yakut_100_|사용할 수 없음|  
|이 문자(중국)|Latin1_General_100_|사용할 수 없음|  
|요루바어(나이지리아)|Latin1_General_100_|사용할 수 없음|  
|줄루어(남아프리카)|Latin1_General_100_|사용할 수 없음|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상의 서버 수준에서 더 이상 사용할 수 없음|힌디어|힌디어|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상의 서버 수준에서 더 이상 사용할 수 없음|Korean_Wansung_Unicode|Korean_Wansung_Unicode|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상의 서버 수준에서 더 이상 사용할 수 없음|Lithuanian_Classic|Lithuanian_Classic|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상의 서버 수준에서 더 이상 사용할 수 없음|마케도니아어|마케도니아어|  
  
 <sup>1</sup>Windows 유니코드 전용 데이터 정렬은 열 수준 또는 식 수준 데이터에만 적용 될 수 있습니다. 서버 또는 데이터베이스 데이터 정렬로 사용할 수 없습니다.  
  
 <sup>2</sup>마찬가지로 중국어 (대만) 데이터 정렬이 중국어 (마카오) 사용 하 여 중국어 간체의 규칙 않으며 중국어 (대만)와 달리 코드 페이지 950을 사용 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [데이터 정렬 및 유니코드 지원](../../relational-databases/collations/collation-and-unicode-support.md)   
 [ALTER TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [상수 &#40; Transact SQL &#41;](../../t-sql/data-types/constants-transact-sql.md)   
 [CREATE DATABASE&#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [CREATE TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [DECLARE @local_variable&#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)   
 [테이블 &#40; Transact SQL &#41;](../../t-sql/data-types/table-transact-sql.md)   
 [sys.fn_helpcollations&#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md)  
  
  

