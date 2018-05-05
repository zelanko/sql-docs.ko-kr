---
title: (MySQLToSQL) 설정 MySQL 및 SQL Server 문자 매핑 | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-mysql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 20b3f22e-16a2-4a87-b4eb-c277be6bf5c8
caps.latest.revision: 4
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 0a0b1abc184a6c7c0031d1b8d2dacd6d05cda324
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="mapping-mysql-and-sql-server-character-set-mysqltosql"></a>(MySQLToSQL) 설정 MySQL 및 SQL Server 문자 매핑
MySQL 문자 데이터 형식, 식 및 리터럴을 대 한 문자 집합 (문자 집합)을 지정할 수 있습니다.  
  
## <a name="charset-mapping"></a>문자 집합 매핑  
문자 집합 매핑 각 MySQL 문자 집합에 대해 정의 되 고 문자 데이터 형식 변환 중에 사용 합니다. 특정 문자 집합의 문자열 데이터 형식 변환 하는 방법을 지정 합니다.  
  
-   National SQL Server 문자 형식 (NCHAR/NVARCHAR) 또는  
  
-   일반 SQL Server 문자 형식 (CHAR/VARCHAR)  
  
1.  **national** 대상 데이터베이스 문자 데이터 형식은:  
  
    1.  **nchar**  
  
    2.  **nvarchar**  
  
2.  **일반** 대상 데이터베이스 문자 데이터 형식은:  
  
    1.  **char**  
  
    2.  **varchar**  
  
3.  형식 매핑에 대 한 매핑이 허용 **national** 문자 데이터 형식입니다. MySQL 문자 데이터 형식 매핑 형식에 따라 변환 된 후에 문자 집합 매핑이 적용 됩니다.  
  
> [!NOTE]  
> 문자 집합 매핑 메타 데이터 개체 탐색기의 각 노드 수준을에 정의할 수 있습니다 및 MySQL에서 읽은 모든 문자 집합을 나타냅니다.  
  
## <a name="charset-mapping-on-different-node-levels"></a>서로 다른 노드 수준에서 문자 집합 매핑  
문자 집합 매핑 다릅니다 다른 노드 수준의 즉:  
  
1.  루트 메타 데이터 노드 수준에서  
  
2.  데이터베이스, 범주 및 개체 노드 수준에서  
  
> [!NOTE]  
> 문자 집합 매핑 편집을 위해 선택한 탭 매핑 서로 다른 노드 수준에 관계 없이 세 개의 단추가 있습니다.  
>   
> 반환할 수 있습니다.  
>   
> 1.  **적용:** charset 매핑을 편집 하 고 아직 저장 되지 경우에 사용자가 수행한 변경 내용을 적용 합니다.  
> 2.  **취소:** 사용자가 수행한 변경 내용을 취소 합니다. 문자 집합 매핑 편집 있지만 저장 되지 단추가 활성화를 가져옵니다.  
> 3.  **기본값으로 재설정:** 모든 매핑을 기본값으로 다시 설정 합니다.  
  
1.  **On 루트 메타 데이터 노드 수준:** Charset 매핑 그리드의 각 문자 집합에 대 한 별도 열이 포함 된 문자 집합 표가 포함 됩니다. 눈금의 열이 됩니다.  
  
    1.  명명 된 눈금의 첫 번째 열 **문자 집합 이름** 문자 집합 이름을 포함 합니다.  
  
    2.  명명 된 두 번째 식 **Charset 설명** charset 설명을 포함 합니다.  
  
    3.  세 번째 열, 이라는 **대상 문자 집합 유형** 특정 문자 집합에 대 한 매핑 설정을 포함 합니다. 이 열에 대 한 값은 같습니다.  
  
        -   CHAR/VARCHAR  
  
        -   NCHAR/NVARCHAR  
  
    > [!IMPORTANT]  
    > 특정 문자 집합에 대 한 기본값 CHAR/VARCHAR 또는 NCHAR/NVARCHAR 후 접두사 (기본값)에 포함 합니다.  
  
    MySQL 데이터베이스와 루트 메타 데이터 노드 수준에서 대상 데이터베이스 간의 Charset 매핑은 다음과 같습니다.  
  
    ||||  
    |-|-|-|  
    |**문자 집합 이름**|**문자 집합 설명**|**대상 문자 집합 유형 (기본값)**|  
    |big5|중국어 번체 Big5|NCHAR/NVARCHAR (기본값)|  
    |dec8|DEC 서 부 유럽|CHAR/VARCHAR (기본값)|  
    |cp850|DOS 서 부 유럽|CHAR/VARCHAR (기본값)|  
    |hp8|HP 서 부 유럽|CHAR/VARCHAR (기본값)|  
    |koi8r|KOI8 R Relcom 러시아어|CHAR/VARCHAR (기본값)|  
    |라틴어 1|cp1252 서 부 유럽|CHAR/VARCHAR (기본값)|  
    |latin2|ISO 8859-2 중앙 유럽|CHAR/VARCHAR (기본값)|  
    |swe7|7 비트 스웨덴어|CHAR/VARCHAR (기본값)|  
    |ascii|US ASCII|CHAR/VARCHAR (기본값)|  
    |ujis|EUC-JP 일본어|NCHAR/NVARCHAR (기본값)|  
    |sjis|일본어 shift JIS|NCHAR/NVARCHAR (기본값)|  
    |히브리어|ISO 8859-8 히브리어|CHAR/VARCHAR (기본값)|  
    |tis620|TIS620 태국어|CHAR/VARCHAR (기본값)|  
    |euckr|EUC-KR 한국어|NCHAR/NVARCHAR (기본값)|  
    |koi8u|우크라이나어 KOI8-U|CHAR/VARCHAR (기본값)|  
    |gb2312|중국어 간체 GB2312|NCHAR/NVARCHAR (기본값)|  
    |그리스어|ISO 8859-7 그리스어|CHAR/VARCHAR (기본값)|  
    |cp 1250|Windows 중앙 유럽|CHAR/VARCHAR (기본값)|  
    |gbk|GBK 중국어 간체|NCHAR/NVARCHAR (기본값)|  
    |latin5|ISO 8859-9 터키어|CHAR/VARCHAR (기본값)|  
    |armscii8|ARMSCII 8 아르메니아어|CHAR/VARCHAR (기본값)|  
    |utf8|U t F-8 유니코드|NCHAR/NVARCHAR (기본값)|  
    |ucs2|Ucs-2 유니코드|NCHAR/NVARCHAR (기본값)|  
    |cp866|DOS 러시아어|CHAR/VARCHAR (기본값)|  
    |keybcs2|DOS Kamenicky 체코어 슬로바키아어|CHAR/VARCHAR (기본값)|  
    |macce|Mac 중앙 유럽|CHAR/VARCHAR (기본값)|  
    |macroman|Mac 서 부 유럽|CHAR/VARCHAR (기본값)|  
    |cp852|DOS 중앙 유럽|CHAR/VARCHAR (기본값)|  
    |latin7|ISO 8859-13 발트어|CHAR/VARCHAR (기본값)|  
    |cp 1251|Windows Cyrillic|CHAR/VARCHAR (기본값)|  
    |cp 1256|Windows 아랍어|CHAR/VARCHAR (기본값)|  
    |cp 1257|Windows Baltic|CHAR/VARCHAR (기본값)|  
    |BINARY|이진 의사 문자 집합|CHAR/VARCHAR (기본값)|  
    |geostd8|GEOSTD8 그루지야어|CHAR/VARCHAR (기본값)|  
    |cp932|Windows 일본어 SJIS|NCHAR/NVARCHAR (기본값)|  
    |eucjpms|Windows 일본어 UJIS|NCHAR/NVARCHAR (기본값)|  
  
2.  **데이터베이스, 범주 또는 개체 노드 수준에서:** charset 매핑 그리드 데이터베이스, 범주 또는 개체 노드 수준에서 루트 메타 데이터 노드 수준에 있는 것과 동일한 행 viz 포함 합니다.:  
  
    1.  첫 번째 열, 이라는 눈금의 **문자 집합 이름** 문자 집합 이름을 포함 합니다.  
  
    2.  이라는 두 번째 열 **문자 설정 설명** charset 설명을 포함 합니다.  
  
    3.  유일한 차이점은 눈금의 세 번째 열에 있는 값입니다. 세 번째 열, 이라는 **대상 데이터 형식** 특정 문자 집합에 대 한 매핑 설정을 포함 합니다. 열에 대 한 값은 같습니다.  
  
        -   상속 (CHAR/VARCHAR 또는 NCHAR/NVARCHAR)  
  
        -   CHAR/VARCHAR  
  
        -   NCHAR/NVARCHAR  
  
> [!IMPORTANT]  
> -   MySQL 데이터베이스와 대상 데이터베이스에서 데이터베이스, 범주 및 개체 노드 수준 사이의 문자 집합 매핑, 기본 열에 대 한 루트가 아닌 각 수준에 특정 문자 집합에 대 한 값 **대상 데이터 형식** '상속 되어야'.  
> -   표에서 값 **Inherited** 를 사용 하 여 접미사로 '(CHAR/VARCHAR)' 또는 '(NCHAR/NVARCHAR)' 따라 어떤 값이 특정 문자 집합으로 부모에서 상속 되었습니다.  
  
