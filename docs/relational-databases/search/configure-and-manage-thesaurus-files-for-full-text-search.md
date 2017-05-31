---
title: "전체 텍스트 검색에 사용할 동의어 사전 파일 구성 및 관리 | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-search
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- full-text indexes [SQL Server], thesaurus files
- thesaurus [full-text search], configuring
- thesaurus [full-text search]
ms.assetid: 3ef96a63-8a52-45be-9a1f-265bff400e54
caps.latest.revision: 84
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 40a1d0874909c787b69300821d05e22a701d657a
ms.contentlocale: ko-kr
ms.lasthandoff: 04/11/2017

---
# <a name="configure-and-manage-thesaurus-files-for-full-text-search"></a>전체 텍스트 검색에 사용할 동의어 사전 파일 구성 및 관리
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 전체 텍스트 검색 쿼리는 전체 텍스트 검색 *동의어 사전*을 사용하여 사용자 지정 용어의 동의어를 검색할 수 있습니다. 각 동의어 사전은 특정 언어에 대한 동의어 집합을 정의합니다. 전체 텍스트 데이터에 맞게 동의어 사전을 개발하면 해당 데이터에 대한 전체 텍스트 쿼리의 범위를 효과적으로 넓힐 수 있습니다.

동의어 사전 검색은 모든 [FREETEXT](../../t-sql/queries/freetext-transact-sql.md) 및 [FREETEXTABLE](../../relational-databases/system-functions/freetexttable-transact-sql.md) 쿼리와 `FORMSOF THESAURUS` 절을 지정하는 [CONTAINS](../../t-sql/queries/contains-transact-sql.md) 및 [CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md) 쿼리에 대해 수행됩니다.
  
전체 텍스트 검색 동의어 사전은 XML 텍스트 파일입니다.
  
##  <a name="tasks"></a> 동의어 사전의 기능  
 전체 텍스트 검색 쿼리가 지정된 언어에서 동의어를 찾을 수 있도록 하려면 해당 언어에 대한 동의어 사전 매핑(즉, 동의어)을 정의해야 합니다. 각 동의어 사전은 다음을 정의하도록 수동으로 구성해야 합니다.  
  
-   확장 집합  
  
     확장 집합은 전체 텍스트 쿼리에 의해 서로 대체되는 "writer", "author" 및 "journalist"와 같은 동의어 그룹을 포함합니다. 확장 집합에 동의어에 대한 일치 항목이 있는 쿼리는 확장 집합의 다른 모든 동의어를 포함하도록 확장됩니다.  
  
     자세한 내용은 이 항목의 뒷부분에 나오는 [확장 집합의 XML 구조](#expansion)를 참조하세요.  
  
-   교체 집합  
  
     교체 집합에는 대체 집합으로 바꿀 텍스트 패턴이 포함되어 있습니다. 예를 보려면 이 항목의 뒷부분에 나오는[교체 집합의 XML 구조](#replacement) 섹션을 참조하세요. 

-   분음 부호 설정  
  
     지정된 동의어 사전에 대해 모든 검색 패턴은 물결표(**~**), 양음 악센트 표시(**´**) 또는 움라우트(**¨**) 등의 분음 부호를 구분하거나 구분하지 않습니다(즉, *악센트 구분* 또는 *악센트 구분 안 함*). 예를 들어 전체 텍스트 쿼리에서 "café" 패턴을 다른 패턴으로 바꾸도록 지정한다고 가정해 보겠습니다. 동의어 사전이 악센트를 구분하지 않으면 전체 텍스트 검색 시 "café" 및 "cafe" 패턴이 바뀝니다. 동의어 사전이 악센트를 구분하면 전체 텍스트 검색 시 "café" 패턴만 바뀝니다. 기본적으로 동의어 사전은 악센트를 구분하지 않습니다.  
  
##  <a name="initial_thesaurus_files"></a> 기본 동의어 사전 파일
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 지원되는 각 언어당 하나의 XML 동의어 사전 파일을 제공합니다. 이러한 파일은 기본적으로 비어 있습니다. 파일에는 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 동의어 사전에 공통적인 최상위 XML 구조와 주석 처리된 예제 동의어 사전만 포함되어 있습니다.  
  
##  <a name="location"></a> 동의어 사전 파일의 위치  
 동의어 사전 파일의 기본 위치는 다음과 같습니다.  
  
     <SQL_Server_data_files_path>\MSSQL13.MSSQLSERVER\MSSQL\FTDATA\  
  
 이 기본 위치에는 다음 파일이 포함되어 있습니다.  
  
-   **언어별** 동의어 사전 파일  

    설치 프로그램은 위의 위치에 빈 동의어 사전 파일을 설치합니다. 지원되는 각 언어에 대해 별도의 파일이 제공됩니다. 시스템 관리자는 이러한 파일을 사용자 지정할 수 있습니다.  
  
     동의어 사전 파일의 기본 파일 이름은 다음 형식을 사용합니다.  
  
         'ts' + <three-letter language-abbreviation> + '.xml'  
  
     특정 언어에 대한 동의어 사전 파일의 이름은 레지스트리의 다음 값에 지정됩니다.
     
        HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\<instance-name>\MSSearch\<language-abbrev>  
  
-   **전역** 동의어 사전 파일  
  
     빈 전역 동의어 사전 파일인 tsGlobal.xml  

### <a name="change-the-location-of-a-thesaurus-file"></a>동의어 사전 파일의 위치 변경 
레지스트리 키를 변경하여 동의어 사전 파일의 위치와 이름을 바꿀 수 있습니다. 각 언어에 대해 동의어 사전 파일의 위치는 레지스트리의 다음 값에 지정됩니다.  
  
    HKLM\SOFTWARE\Microsoft\Microsoft SQL Server\<instance name>\MSSearch\Language\<language-abbreviation>\TsaurusFile  
  
 전역 동의어 사전 파일은 LCID 0의 중립 언어에 해당합니다. 이 값은 관리자만 변경할 수 있습니다.  

##  <a name="how_queries_use_tf"></a> 전체 텍스트 쿼리에서 동의어 사전을 사용하는 방법  
동의어 사전 쿼리는 언어별 동의어 사전과 전역 동의어 사전을 모두 사용합니다.
1.  이 쿼리는 먼저 언어별 파일을 조회한 다음 이미 로드되지 않은 경우 처리를 위해 해당 파일을 로드합니다. 이 쿼리는 동의어 사전 파일의 확장 집합 규칙과 교체 집합 규칙으로 지정된 언어별 동의어를 포함하도록 확장됩니다. 
2.  그런 다음 전역 동의어 사전에 대해 이러한 단계가 반복됩니다. 그러나 용어가 이미 언어별 동의어 사전 파일에서 일치 항목의 일부인 경우 해당 용어는 전역 동의어 사전에서 일치 항목으로 적합하지 않습니다.  

##  <a name="structure"></a> 동의어 사전 파일의 구조  
 각 동의어 사전 파일은 ID가 `Microsoft Search Thesaurus`인 XML 컨테이너와, 예제 동의어 사전을 포함하는 주석( `<!--` … `-->`)을 정의합니다. 동의어 사전은 분음 부호 설정, 확장 집합, 교체 집합을 정의하는 자식 요소의 샘플이 포함된 `<thesaurus>` 요소에 정의됩니다.

일반적인 빈 동의어 사전 파일에는 다음과 같은 XML 텍스트가 포함되어 있습니다.  
  
```xml  
<XML ID="Microsoft Search Thesaurus">  
  
<!--  Commented out  
  
    <thesaurus xmlns="x-schema:tsSchema.xml">  
<diacritics_sensitive>0</diacritics_sensitive>  
        <expansion>  
            <sub>Internet Explorer</sub>  
            <sub>IE</sub>  
            <sub>IE5</sub>  
        </expansion>  
        <replacement>  
            <pat>NT5</pat>  
            <pat>W2K</pat>  
            <sub>Windows 2012</sub>  
        </replacement>  
        <expansion>  
            <sub>run</sub>  
            <sub>jog</sub>  
        </expansion>  
    </thesaurus>  
-->  
</XML>  
```

### <a name="expansion"></a> 확장 집합의 XML 구조  
  
 각 확장 집합은 `<expansion>` 요소로 묶입니다. 이 요소 내에서 `<sub>` 요소에 하나 이상의 대체 단어를 지정합니다. 확장 집합에 서로의 동의어인 대체 그룹을 지정할 수 있습니다.  
  
 예를 들어 "writer", "author" 및 "journalist" 대체 단어를 동의어로 처리하도록 확장 섹션을 편집할 수 있습니다. 하나의 대체 집합에 일치하는 항목이 있는 전체 텍스트 검색 쿼리는 확장 집합에 지정된 다른 모든 대체 단어를 포함하도록 확장됩니다. 따라서 위 예에서 "author"라는 단어에 대해 FORMS OF THESAURUS 또는 FREETEXT 쿼리를 실행하면 전체 텍스트 검색에 "writer" 및 "journalist"라는 단어를 포함하는 검색 결과가 반환됩니다.  
  
다음은 위 예에 대한 확장 집합 섹션을 나타낸 것입니다.  
  
```xml  
<expansion>  
        <sub>writer</sub>  
        <sub>author</sub>  
        <sub>journalist</sub>  
</expansion>  
```  
  
### <a name="replacement"></a> 교체 집합의 XML 구조  
  
각 교체 집합은 `<replacement>` 요소로 묶입니다. 이 요소 내에서 동의어당 하나씩 1개 이상의 패턴을 `<pat>` 요소에 지정하고, 0개 이상의 대체 단어를 `<sub>` 요소에 지정할 수 있습니다. 대체 집합으로 바꿀 패턴을 지정할 수 있습니다. 패턴 및 대체 집합에는 단어 또는 일련의 단어를 포함할 수 있습니다. 패턴에 지정된 대체 단어가 없는 경우 사용자 쿼리에서 해당 패턴이 제거됩니다.  
  
예를 들어 'Win8' 패턴을 'Windows Server 2012' 또는 'Windows 8.0' 대체 단어로 바꾸는 쿼리를 원하는 경우 'Win8'에 대해 전체 텍스트 쿼리를 실행하면 전체 텍스트 검색에 'Server 2012' 또는 'Windows 8.0'd\을 포함하는 검색 결과만 반환됩니다. 'Win8'을 포함하는 결과는 반환되지 않습니다. 이는 'Win8' 패턴이 'Windows Server 2012' 및 'Windows 8.0' 패턴으로 '바뀌었기' 때문입니다.  
  
다음은 위 예에 대한 교체 집합 섹션을 나타낸 것입니다.  
  
```xml  
<replacement>  
        <pat>Win8</pat>  
        <sub>Windows Server 2012</sub>  
        <sub>Windows 8.0</sub>  
</replacement>  
```  
  
패턴이 유사하게 일치하는 두 개의 교체 집합이 있는 경우 두 개 중 더 긴 것이 우선적으로 적용됩니다. 예를 들어 "Internet Explorer online community"에 대해 FORMS OF THESAURUS 쿼리를 실행하고 다음과 같은 교체 집합이 있는 경우 "Internet Explorer" 교체 집합이 "Internet" 교체 집합보다 우선적으로 적용됩니다. 따라서 쿼리가 "IE online community" 또는 "IE 9 online community"로 처리됩니다.  
  
```xml  
<replacement>  
         <pat>Internet</pat>  
         <sub>intranet</sub>  
</replacement>  
```  
  
및  
  
```xml  
<replacement>  
         <pat>Internet Explorer</pat>  
         <sub>IE</sub>  
         <sub>IE 9</sub>  
</replacement>  
```

### <a name="xml-structure-of-the-diacritics-setting"></a>분음 부호 설정의 XML 구조  
  
동의어 사전의 분음 부호 설정은 단일 `<diacritics_sensitive>` 요소에 지정됩니다. 이 요소는 다음과 같이 악센트 구분 여부를 제어하는 정수 값을 포함합니다.  
  
|분음 부호 설정|값|XML|  
|------------------------|-----------|---------|  
|악센트 구분 안 함|0|`<diacritics_sensitive>0</diacritics_sensitive>`|  
|악센트 구분|1|`<diacritics_sensitive>1</diacritics_sensitive>`|  
  
> [!NOTE]  
>  이 설정은 파일에서 한 번만 적용될 수 있으며 해당 파일의 모든 검색 패턴에 적용됩니다. 개별 패턴에 대해서는 이 설정을 지정할 수 없습니다.  

##  <a name="editing"></a> 동의어 사전 파일 편집  
지정된 언어에 대한 동의어 사전은 해당 동의어 사전 파일(XML 파일)을 편집하여 구성할 수 있습니다. 설치 중에 `<xml>` 컨테이너와 주석 처리된 샘플 `<thesaurus`> 요소만 포함된 빈 동의어 사전 파일이 설치됩니다. 동의어를 검색하는 전체 텍스트 검색 쿼리가 올바르게 작동하려면 동의어 집합을 정의하는 실제 `<thesaurus` 요소를 만들어야 하는데, 확장 집합과 교체 집합의 두 형식으로 정의할 수 있습니다.  

### <a name="edit-a-thesaurus-file"></a>동의어 사전 파일 편집  
  
1.  동의어 사전 파일을 메모장이나 다른 텍스트 편집기에서 엽니다.  
  
2.  동의어 사전 파일을 처음 편집하는 경우 파일의 시작 및 끝 부분에서 각각 다음 주석 줄을 제거합니다.  
  
    ```xml  
    <!--Commented out  
    -->  
    ```  
  
3.  교체 집합이나 확장 집합을 추가, 수정 또는 삭제합니다.  
  
4.  파일을 저장하고 메모장을 닫습니다.  
  
5.  동의어 사전 파일의 언어에 해당하는 LCID(로컬 식별자)를 지정하고 [sp_fulltext_load_thesaurus_file](../../relational-databases/system-stored-procedures/sp-fulltext-load-thesaurus-file-transact-sql.md) 을 사용하여 동의어 사전 파일의 내용을 tempdb에 로드할 수 있습니다. 예를 들어 영어 동의어 사전 파일 tsenu.xml의 경우 해당하는 LCID는 1033입니다.  
  
    ```tsql  
    USE AdventureWorks;  
    EXEC sys.sp_fulltext_load_thesaurus_file 1033;  
    GO
    ```

### <a name="recommendations-for-editing-thesaurus-files"></a>동의어 사전 파일 편집 관련 권장 사항  
  
 동의어 사전 파일의 항목에는 특수 문자를 사용하지 않는 것이 좋습니다. 특수 문자와 관련하여 단어 분리기의 동작에 미묘한 부분이 있기 때문입니다. 동의어 사전 항목에 특수 문자가 포함된 경우 해당 항목과 함께 사용된 단어 분리기는 전체 텍스트 쿼리의 동작에 미묘한 영향을 미칠 수 있습니다.  
  
 중지 단어는 전체 텍스트 인덱스에서 생략되므로 `<sub>` 항목에는 중지 단어를 포함하지 않는 것이 좋습니다. 쿼리는 동의어 사전 파일의 `<sub>` 항목을 포함하도록 확장되므로 `<sub>` 항목에 중지 단어가 포함되어 있으면 쿼리 크기가 불필요하게 커지게 됩니다.  

### <a name="restrictions-for-editing-thesaurus-files"></a>동의어 사전 파일 편집 관련 제한 사항  
  
 동의어 사전 파일 편집에는 다음과 같은 제한 사항이 적용됩니다.  
  
-   동의어 사전 파일은 시스템 관리자만 업데이트, 수정 또는 삭제할 수 있습니다.  
  
-   텍스트 편집기 도구를 사용하여 동의어 사전 파일을 편집하는 경우 파일을 유니코드 형식으로 저장하고 바이트 순서 표시를 지정해야 합니다.  
  
-   동의어 사전 항목은 비어 있거나 빈 문자열로 단어 분리될 수 없습니다.  
  
-   문자 수가 512개보다 많은 구는 동의어 사전 파일에 사용할 수 없습니다.  
  
-   동의어 사전에는 확장 집합의 `<sub>` 항목과 교체 집합의 `<pat>` 요소 사이에 중복된 항목이 없어야 합니다.  

## <a name="see-also"></a>참고 항목  
 [CONTAINS&#40;Transact-SQL&#41;](../../t-sql/queries/contains-transact-sql.md)   
 [CONTAINSTABLE&#40;Transact-SQL&#41;](../../relational-databases/system-functions/containstable-transact-sql.md)   
 [FREETEXT&#40;Transact-SQL&#41;](../../t-sql/queries/freetext-transact-sql.md)   
 [FREETEXTTABLE&#40;Transact-SQL&#41;](../../relational-databases/system-functions/freetexttable-transact-sql.md)     
 [sp_fulltext_load_thesaurus_file&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-load-thesaurus-file-transact-sql.md)  
 [sys.dm_fts_parser&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-parser-transact-sql.md)
 
