---
title: "검색에 사용된 단어 분리기를 이전 버전으로 되돌리기 | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: search
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-search
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 29b4488e-4c6a-4bf0-a64d-19e2fdafa7ae
caps.latest.revision: "13"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 932ac3a8337af5871910c9aabd7a906508b1455d
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="revert-the-word-breakers-used-by-search-to-the-previous-version"></a>검색에 사용된 단어 분리기를 이전 버전으로 되돌리기
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)] [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서는 한국어를 제외하고 전체 텍스트 검색에서 지원되는 모든 언어에 대해 단어 분리기 및 형태소 분석기의 버전을 설치하고 활성화합니다. 이 항목에서는 이러한 버전의 구성 요소에서 이전 버전으로 전환하거나 이전 버전에서 다시 새 버전으로 전환하는 방법에 대해 설명합니다.  
  
 이 항목에서는 다음 언어에 대해 다루지 않습니다.  
  
-   **영어**. 영어 구성 요소를 되돌리거나 복원하려면 [Change the Word Breaker Used for US English and UK English](../../relational-databases/search/change-the-word-breaker-used-for-us-english-and-uk-english.md)을 참조하세요.  
  
-   **덴마크어, 터키어 및 폴란드어**. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 이전 릴리스에 포함된 덴마크어, 폴란드어 및 터키어에 대한 타사 단어 분리기는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 구성 요소로 대체되었습니다.  
  
-   **그리스어와 체코어**. 체코어 및 그리스어에 대한 새로운 단어 분리기가 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 전체 텍스트 검색의 이전 릴리스에는 이 두 언어에 대한 지원이 포함되지 않았습니다.  
  
-   **한국어**. 한국어에 대한 단어 분리기 및 형태소 분석기는 이 릴리스에서 업그레이드되지 않았습니다.  
  
 단어 분리기 및 형태소 분석기에 대한 일반적인 내용은 [검색을 위해 단어 분리기와 형태소 분석기 구성 및 관리](../../relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md)를 참조하세요.  
  
##  <a name="overview"></a> 단어 분리기 및 형태소 분석기 되돌리기 및 복원 개요  
 단어 분리기 및 형태소 분석기를 되돌리고 복원하는 방법은 언어에 따라 다릅니다. 다음 표에서는 이전 버전의 구성 요소로 되돌리는 데 필요한 세 작업 집합에 대해 요약합니다.  
  
|현재 파일|이전 파일|영향 받는 언어 수|파일 작업|레지스트리 항목 작업|  
|------------------|-------------------|----------------------------------|----------------------|---------------------------------|  
|NaturalLanguage6.dll|NaturalLanguage6.dll|34|이전 버전의 NaturalLanguage6.dll을 가져와서 설치합니다. 그러면 현재 버전의 파일을 덮어씁니다.|별도의 작업이 필요 없습니다.<br /><br /> 레지스트리 키와 값은 이 릴리스에서 변경되지 않았습니다.|  
|(기타 파일 이름)|NaturalLanguage6.dll|5|이전 버전의 NaturalLanguage6.dll을 가져와서 설치합니다. 그러면 현재 버전의 파일을 덮어씁니다.|레지스트리 항목 집합을 변경하여 이전 버전의 구성 요소를 지정합니다.|  
|(기타 파일 이름)|(기타 파일 이름)|6|별도의 작업이 필요 없습니다.<br /><br /> [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 설치 프로그램이 구성 요소의 현재 버전과 이전 버전을 모두 Binn 폴더에 복사합니다.|레지스트리 항목 집합을 변경하여 이전 버전의 구성 요소를 지정합니다.|  
  
> [!WARNING]  
>  NaturalLanguage6.dll 파일의 현재 버전을 다른 버전으로 교체하면 이 파일을 사용하는 모든 언어의 동작이 영향을 받습니다.  
  
 이 항목에서 설명하는 파일은 `MSSQL\Binn` 인스턴스의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 폴더에 설치되는 DLL 파일입니다. 전체 경로는 일반적으로 다음과 같습니다.  
  
 `C:\Program Files\Microsoft SQL Server\<instance>\MSSQL\Binn`  
  
##  <a name="nl6nl6"></a> 현재 단어 분리기와 이전 단어 분리기의 파일 이름에 대한 언어는 NaturalLanguage6.dll입니다.  
 다음 표에 나오는 언어의 경우 현재 단어 분리기와 이전 단어 분리기의 파일 이름은 모두 NaturalLanguage6.dll입니다. 이 구성 요소를 되돌리거나 복원하려면 NaturalLanguage6.dll을 동일한 파일의 다른 버전으로 덮어써야 합니다. 레지스트리 항목은 이 릴리스에서 변경되지 않았으므로 레지스트리 항목을 변경할 필요는 없습니다.  
  
> [!WARNING]  
>  NaturalLanguage6.dll 파일의 현재 버전을 다른 버전으로 교체하면 이 파일을 사용하는 모든 언어의 동작이 영향을 받습니다.  
  
 **영향을 받는 언어 목록**  
  
|언어|약어<br />레지스트리에<br />사용된|LCID|  
|--------------|---------------------------------------|----------|  
|벵골어|ben|1093|  
|불가리아어|bgr|1026|  
|카탈로니아어|cat|1027|  
|스페인어|esn|3082|  
|프랑스어|fra|1036|  
|구자라트어|guj|1095|  
|히브리어|heb|1037|  
|힌디어|hin|1081|  
|크로아티아어|hrv|1050|  
|인도네시아어|ind|1057|  
|아이슬란드어|isl|1039|  
|이탈리아어|ita|1040|  
|카나다어|kan|1099|  
|리투아니아어|lth|1063|  
|라트비아어|lvi|1062|  
|말라얄람어|mal|1100|  
|마라티어|mar|1102|  
|말레이어|msl|1086|  
|중립|중립|0000|  
|노르웨이어(복말)|nor|1044|  
|펀잡어|pan|1094|  
|포르투갈어(브라질)|ptb|1046|  
|포르투갈어|ptg|2070|  
|루마니아어|rom|1048|  
|슬로바키아어|sky|1051|  
|슬로베니아어|slv|1060|  
|세르비아어 - 키릴 자모|srb|3098|  
|세르비아어 - 라틴 문자|srl|2074|  
|스웨덴어|sve|1053|  
|타밀어|tam|1097|  
|텔루구어|tel|1098|  
|우크라이나어|ukr|1058|  
|우르두어|urd|1056|  
|베트남어|vit|1066|  
  
 이전 표는 약어 열을 기준으로 사전순으로 정렬됩니다.  
  
###  <a name="nl6nl6revert"></a> 이전 구성 요소로 되돌리려면  
  
1.  위에서 설명한 Binn 폴더로 이동합니다.  
  
2.  NaturalLanguage6.dll의 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 버전을 다른 위치에 백업합니다.  
  
3.  이전 버전 NaturalLanguage6.dll을 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 또는 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 인스턴스의 Binn 폴더에서 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 인스턴스의 Binn 폴더로 복사합니다.  
  
    > [!WARNING]  
    >  이 변경 사항은 현재 버전과 이전 버전의 NaturalLanguage6.dll을 사용하는 모든 언어에 적용됩니다.  
  
4.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 다시 시작합니다.  
  
###  <a name="nl6nl6restore"></a> 현재 구성 요소를 복원하려면  
  
1.  NaturalLanguage6.dll의 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 버전을 백업한 위치로 이동합니다.  
  
2.  현재 버전의 NaturalLanguage6.dll을 백업 위치에서 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 인스턴스의 Binn 폴더로 복사합니다.  
  
    > [!WARNING]  
    >  이 변경 사항은 현재 버전과 이전 버전의 NaturalLanguage6.dll을 사용하는 모든 언어에 적용됩니다.  
  
3.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 다시 시작합니다.  
  
##  <a name="newnl6"></a> 이전 단어 분리기의 파일 이름에 대한 언어만 NaturalLanguage6.dll입니다.  
 다음 표에 나오는 언어의 경우 이전 단어 분리기의 파일 이름이 새 버전의 파일 이름과 다릅니다. 이전 파일 이름은 NaturalLanguage6.dll입니다. 이전 버전으로 되돌리려면 현재 버전의 NaturalLanguage6.dll을 동일 파일의 이전 버전으로 덮어써야 합니다. 또한 레지스트리 항목 집합을 변경하여 구성 요소의 이전 버전 또는 현재 버전을 지정해야 합니다.  
  
> [!WARNING]  
>  NaturalLanguage6.dll 파일의 현재 버전을 다른 버전으로 교체하면 이 파일을 사용하는 모든 언어의 동작이 영향을 받습니다.  
  
 **영향을 받는 언어 목록**  
  
|언어|약어<br />레지스트리에<br />사용된|LCID|  
|--------------|---------------------------------------|----------|  
|아랍어|ara|1025|  
|독일어|deu|1031|  
|일본어|jpn|1041|  
|네덜란드어|nld|1043|  
|러시아어|rus|1049|  
  
 이전 표는 약어 열을 기준으로 사전순으로 정렬됩니다.  
  
 다음 지침을 [단어 분리기 및 형태소 분석기를 되돌리고 복원하기 위한 파일 이름 및 레지스트리 값](#newnl6values)섹션의 값 목록과 함께 사용하세요.  
  
###  <a name="newnl6revert"></a> 이전 구성 요소로 되돌리려면  
  
1.  위에서 설명한 Binn 폴더로 이동합니다.  
  
2.  현재 버전의 구성 요소에 대한 파일을 Binn 폴더에서 제거하지 마세요.  
  
3.  NaturalLanguage6.dll의 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 버전을 다른 위치에 백업합니다.  
  
4.  이전 버전 NaturalLanguage6.dll을 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 또는 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 인스턴스의 Binn 폴더에서 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 인스턴스의 Binn 폴더로 복사합니다.  
  
    > [!WARNING]  
    >  이 변경 사항은 현재 버전과 이전 버전의 NaturalLanguage6.dll을 사용하는 모든 언어에 적용됩니다.  
  
5.  레지스트리에서 **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\<InstanceRoot>\MSSearch\CLSID** 노드로 이동합니다.  
  
6.  다음 단계에 따라 선택한 언어의 이전 단어 분리기 및 형태소 분석기 인터페이스에 대한 COM ClassID의 새 키를 추가합니다.  
  
    1.  이전 단어 분리기의 테이블 값을 사용하여 새 키를 추가합니다.  
  
    2.  키 값 데이터(기본값)를 표에 나오는 이전 단어 분리기의 파일 이름으로 업데이트합니다.  
  
    3.  선택한 언어가 형태소 분석기를 사용하는 경우 이전 형태소 분리기의 테이블 값을 사용하여 새 키를 추가합니다.  
  
    4.  선택한 언어가 형태소 분리기를 사용하는 경우 키 값 데이터(기본값)를 표에 나오는 이전 형태소 분석기의 파일 이름으로 업데이트합니다.  
  
7.  레지스트리에서 **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\<InstanceRoot>\MSSearch\Language\<language_key>** 노드로 이동합니다. *<language_key>*는 레지스트리에서 사용되는 언어에 대한 약어(예: 프랑스어 "fra", 스페인어 "esn")를 나타냅니다.  
  
8.  **WBreakerClass** 키 값을 현재 단어 분리기에 대한 표 값으로 업데이트합니다.  
  
9. 선택한 언어가 형태소 분석기를 사용하는 경우 **StemmerClass** 키 값을 현재 형태소 분리기의 표 값으로 업데이트합니다.  
  
10. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 다시 시작합니다.  
  
###  <a name="newnl6restore"></a> 현재 구성 요소를 복원하려면  
  
1.  NaturalLanguage6.dll의 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 버전을 백업한 위치로 이동합니다.  
  
2.  현재 버전의 NaturalLanguage6.dll을 백업 위치에서 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 인스턴스의 Binn 폴더로 복사합니다.  
  
    > [!WARNING]  
    >  이 변경 사항은 현재 버전과 이전 버전의 NaturalLanguage6.dll을 사용하는 모든 언어에 적용됩니다.  
  
3.  레지스트리에서 **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\<InstanceRoot>\MSSearch\CLSID** 노드로 이동합니다.  
  
4.  다음 키가 없으면 다음 단계에 따라 선택한 언어의 현재 단어 분리기 및 형태소 분석기 인터페이스에 대한 COM ClassID의 새 키를 추가합니다.  
  
    1.  현재 단어 분리기의 테이블 값을 사용하여 새 키를 추가합니다.  
  
    2.  키 값 데이터(기본값)를 표에 나오는 현재 단어 분리기의 파일 이름으로 업데이트합니다.  
  
    3.  선택한 언어가 형태소 분석기를 사용하는 경우 현재 형태소 분리기의 테이블 값을 사용하여 새 키를 추가합니다.  
  
    4.  선택한 언어가 형태소 분리기를 사용하는 경우 키 값 데이터(기본값)를 표에 나오는 현재 형태소 분석기의 파일 이름으로 업데이트합니다.  
  
5.  레지스트리에서 **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\<InstanceRoot>\MSSearch\Language\<language_key>** 노드로 이동합니다. *<language_key>*는 레지스트리에서 사용되는 언어에 대한 약어(예: 프랑스어 "fra", 스페인어 "esn")를 나타냅니다.  
  
6.  **WBreakerClass** 키 값을 이전 단어 분리기에 대한 표 값으로 업데이트합니다.  
  
7.  선택한 언어가 형태소 분석기를 사용하는 경우 **StemmerClass** 키 값을 이전 형태소 분리기의 표 값으로 업데이트합니다.  
  
8.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 다시 시작합니다.  
  
###  <a name="newnl6values"></a> 단어 분리기 및 형태소 분석기를 되돌리고 복원하기 위한 파일 이름 및 레지스트리 값  
 다음 파일 이름 및 레지스트리 항목 목록을 이전 섹션의 지침과 함께 사용하세요. 이전 값을 사용하여 이전 버전으로 되돌리거나, 현재 값을 사용하여 현재 버전의 구성 요소를 복원합니다.  
  
 다음 목록은 각 언어에 사용되는 약어를 기준으로 사전순으로 정렬됩니다.  
  
 **아랍어(ara), LCID 1025**  
  
|구성 요소|단어 분리기|형태소 분석기|  
|---------------|------------------|-------------|  
|이전 CLSID|7EFD3C7E-9E4B-4a93-9503-DECD74C0AC6D|483B0283-25DB-4c92-9C15-A65925CB95CE|  
|이전 파일 이름|NaturalLanguage6.dll|NaturalLanguage6.dll|  
|현재 CLSID|04b37e30-c9a9-4a7d-8f20-792fc87ddf71|없음|  
|현재 파일 이름|MSWB7.dll|없음|  
  
 **독일어(deu), LCID 1031**  
  
|구성 요소|단어 분리기|형태소 분석기|  
|---------------|------------------|-------------|  
|이전 CLSID|45EACA36-DBE9-4e4a-A26D-5C201902346D|65170AE4-0AD2-4fa5-B3BA-7CD73E2DA825|  
|이전 파일 이름|NaturalLanguage6.dll|NaturalLanguage6.dll|  
|현재 CLSID|dfa00c33-bf19-482e-a791-3c785b0149b4|8a474d89-6e2f-419c-8dd5-9b50edc8c787|  
|현재 파일 이름|MSWB7.dll|MSWB7.dll|  
  
 **일본어(jpn), LCID 1041**  
  
|구성 요소|단어 분리기|형태소 분석기|  
|---------------|------------------|-------------|  
|이전 CLSID|E1E8F15E-8BEC-45df-83BF-50FF84D0CAB5|3D5DF14F-649F-4cbc-853D-F18FEDE9CF5D|  
|이전 파일 이름|NaturalLanguage6.dll|NaturalLanguage6.dll|  
|현재 CLSID|04096682-6ece-4e9e-90c1-52d81f0422ed|없음|  
|현재 파일 이름|MsWb70011.dll|없음|  
  
 **네덜란드어(nld), LCID 1043**  
  
|구성 요소|단어 분리기|형태소 분석기|  
|---------------|------------------|-------------|  
|이전 CLSID|2C9F6BEB-C5B0-42b6-A5EE-84C24DC0D8EF|F7A465EE-13FB-409a-B878-195B420433AF|  
|이전 파일 이름|NaturalLanguage6.dll|NaturalLanguage6.dll|  
|현재 CLSID|69483c30-a9af-4552-8f84-a0796ad5285b|CF923CB5-1187-43ab-B053-3E44BED65FFA|  
|현재 파일 이름|MSWB7.dll|MSWB7.dll|  
  
 **러시아어(rus), LCID 1049**  
  
|구성 요소|단어 분리기|형태소 분석기|  
|---------------|------------------|-------------|  
|이전 CLSID|2CB6CDA4-1C14-4392-A8EC-81EEF1F2E079|E06A0DDD-E81A-4e93-8A8D-F386C3A1B670|  
|이전 파일 이름|NaturalLanguage6.dll|NaturalLanguage6.dll|  
|현재 CLSID|aaa3d3bd-6de7-4317-91a0-d25e7d3babc3|d42c8b70-adeb-4b81-a52f-c09f24f77dfa|  
|현재 파일 이름|MSWB7.dll|MSWB7.dll|  
  
##  <a name="newnew"></a> 이전 파일 이름과 현재 파일 이름에 대한 언어는 모두 NaturalLanguage6.dll이 아닙니다.  
 다음 표에 나오는 언어의 경우 이전 단어 분리기 및 형태소 분석기의 파일 이름이 새 버전의 파일 이름과 다릅니다. 이전 파일 이름과 현재 파일 이름이 모두 NaturalLanguage6.dll이 아닙니다. [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 설치 프로그램이 구성 요소의 현재 버전과 이전 버전을 모두 Binn 폴더에 복사하므로 파일을 대체할 필요는 없습니다. 하지만 레지스트리 항목 집합을 변경하여 구성 요소의 이전 버전 또는 현재 버전을 지정해야 합니다.  
  
 **영향을 받는 언어 목록**  
  
|언어|약어<br />레지스트리에<br />사용된|LCID|  
|--------------|---------------------------------------|----------|  
|중국어(간체)|chs|2052|  
|중국어(번체)|cht|1028|  
|태국어|tha|1054|  
|중국어 번체|zh-hk|3076|  
|중국어 번체|zh-mo|5124|  
|중국어 간체|zh-sg|4100|  
  
 이전 표는 약어 열을 기준으로 사전순으로 정렬됩니다.  
  
 다음 지침을 [단어 분리기 및 형태소 분석기를 되돌리고 복원하기 위한 파일 이름 및 레지스트리 값](#newnewvalues)섹션의 값 목록과 함께 사용하세요.  
  
###  <a name="newnewrevert"></a> 이전 구성 요소로 되돌리려면  
  
1.  현재 버전의 구성 요소에 대한 파일을 Binn 폴더에서 제거하지 마세요.  
  
2.  레지스트리에서 **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\<InstanceRoot>\MSSearch\CLSID** 노드로 이동합니다.  
  
3.  다음 단계에 따라 선택한 언어의 이전 단어 분리기 및 형태소 분석기 인터페이스에 대한 COM ClassID의 새 키를 추가합니다.  
  
    1.  이전 단어 분리기의 테이블 값을 사용하여 새 키를 추가합니다.  
  
    2.  키 값 데이터(기본값)를 표에 나오는 이전 단어 분리기의 파일 이름으로 업데이트합니다.  
  
    3.  선택한 언어가 형태소 분석기를 사용하는 경우 이전 형태소 분리기의 테이블 값을 사용하여 새 키를 추가합니다.  
  
    4.  선택한 언어가 형태소 분리기를 사용하는 경우 키 값 데이터(기본값)를 표에 나오는 이전 형태소 분석기의 파일 이름으로 업데이트합니다.  
  
4.  레지스트리에서 **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\<InstanceRoot>\MSSearch\Language\<language_key>** 노드로 이동합니다. *<language_key>*는 레지스트리에서 사용되는 언어에 대한 약어(예: 프랑스어 "fra", 스페인어 "esn")를 나타냅니다.  
  
5.  **WBreakerClass** 키 값을 현재 단어 분리기에 대한 표 값으로 업데이트합니다.  
  
6.  선택한 언어가 형태소 분석기를 사용하는 경우 **StemmerClass** 키 값을 현재 형태소 분리기의 표 값으로 업데이트합니다.  
  
7.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 다시 시작합니다.  
  
###  <a name="newnewrestore"></a> 이전 구성 요소를 복원하려면  
  
1.  이전 버전의 구성 요소에 대한 파일을 Binn 폴더에서 제거하지 마세요.  
  
2.  레지스트리에서 **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\<InstanceRoot>\MSSearch\CLSID** 노드로 이동합니다.  
  
3.  다음 키가 없으면 다음 단계에 따라 선택한 언어의 현재 단어 분리기 및 형태소 분석기 인터페이스에 대한 COM ClassID의 새 키를 추가합니다.  
  
    1.  현재 단어 분리기의 테이블 값을 사용하여 새 키를 추가합니다.  
  
    2.  키 값 데이터(기본값)를 표에 나오는 현재 단어 분리기의 파일 이름으로 업데이트합니다.  
  
    3.  선택한 언어가 형태소 분석기를 사용하는 경우 현재 형태소 분리기의 테이블 값을 사용하여 새 키를 추가합니다.  
  
    4.  선택한 언어가 형태소 분리기를 사용하는 경우 키 값 데이터(기본값)를 표에 나오는 현재 형태소 분석기의 파일 이름으로 업데이트합니다.  
  
4.  레지스트리에서 **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\<InstanceRoot>\MSSearch\Language\<language_key>** 노드로 이동합니다. *<language_key>*는 레지스트리에서 사용되는 언어에 대한 약어(예: 프랑스어 "fra", 스페인어 "esn")를 나타냅니다.  
  
5.  **WBreakerClass** 키 값을 이전 단어 분리기에 대한 표 값으로 업데이트합니다.  
  
6.  선택한 언어가 형태소 분석기를 사용하는 경우 **StemmerClass** 키 값을 이전 형태소 분리기의 표 값으로 업데이트합니다.  
  
7.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 다시 시작합니다.  
  
###  <a name="newnewvalues"></a> 단어 분리기 및 형태소 분석기를 되돌리고 복원하기 위한 파일 이름 및 레지스트리 값  
 다음 파일 이름 및 레지스트리 항목 목록을 이전 섹션의 지침과 함께 사용하세요. 이전 값을 사용하여 이전 버전으로 되돌리거나, 현재 값을 사용하여 현재 버전의 구성 요소를 복원합니다.  
  
 다음 목록은 각 언어에 사용되는 약어를 기준으로 사전순으로 정렬됩니다.  
  
 **중국어 간체(chs), LCID 2052**  
  
|구성 요소|단어 분리기|  
|---------------|------------------|  
|이전 CLSID|12CE94A0-DEFB-11D2-B31D-00600893A857|  
|이전 파일 이름|chsbrkr.dll|  
|현재 CLSID|E0831C90-BAB0-4ca5-B9BD-EA254B538DAC|  
|현재 파일 이름|MsWb70804.dll|  
  
 **중국어 번체(cht), LCID 1028**  
  
|구성 요소|단어 분리기|  
|---------------|------------------|  
|이전 CLSID|1680E7C3-9430-4A51-9B82-1E7E7AEE5258|  
|이전 파일 이름|chtbrkr.dll|  
|현재 CLSID|E9B1DF65-08F1-438b-8277-EF462B23A792|  
|현재 파일 이름|MsWb70404.dll|  
  
 **태국어(tha), LCID 1054**  
  
|구성 요소|단어 분리기|형태소 분석기|  
|---------------|------------------|-------------|  
|이전 CLSID|CCA22CF4-59FE-11D1-BBFF-00C04FB97FDA|CEDC01C7-59FE-11D1-BBFF-00C04FB97FDA|  
|이전 파일 이름|Thawbrkr.dll|Thawbrkr.dll|  
|현재 CLSID|F70C0935-6E9F-4ef1-9F06-7876536DB900|없음|  
|현재 파일 이름|MsWb7001e.dll|없음|  
  
 **중국어 번체(zh-hk), LCID 3076**  
  
|구성 요소|단어 분리기|  
|---------------|------------------|  
|이전 CLSID|1680E7C3-9430-4A51-9B82-1E7E7AEE5258|  
|이전 파일 이름|chtbrkr.dll|  
|현재 CLSID|E9B1DF65-08F1-438b-8277-EF462B23A792|  
|현재 파일 이름|MsWb70404.dll|  
  
 **중국어 번체(zh-mo), LCID 5124**  
  
|구성 요소|단어 분리기|  
|---------------|------------------|  
|이전 CLSID|1680E7C3-9430-4A51-9B82-1E7E7AEE5258|  
|이전 파일 이름|chtbrkr.dll|  
|현재 CLSID|E9B1DF65-08F1-438b-8277-EF462B23A792|  
|현재 파일 이름|MsWb70404.dll|  
  
 **중국어 간체(zh-sg), LCID 4100**  
  
|구성 요소|단어 분리기|  
|---------------|------------------|  
|이전 CLSID|12CE94A0-DEFB-11D2-B31D-00600893A857|  
|이전 파일 이름|chsbrkr.dll|  
|현재 CLSID|E0831C90-BAB0-4ca5-B9BD-EA254B538DAC|  
|현재 파일 이름|MsWb70804.dll|  
  
## <a name="see-also"></a>참고 항목  
 [Change the Word Breaker Used for US English and UK English](../../relational-databases/search/change-the-word-breaker-used-for-us-english-and-uk-english.md)   
 [전체 텍스트 검색의 동작 변경](http://msdn.microsoft.com/library/573444e8-51bc-4f3d-9813-0037d2e13b8f)  
  
  
