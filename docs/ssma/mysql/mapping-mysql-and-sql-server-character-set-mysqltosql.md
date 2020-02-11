---
title: MySQL 및 SQL Server 문자 집합 매핑 (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 20b3f22e-16a2-4a87-b4eb-c277be6bf5c8
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 32d5e23579b99b323da870d2608b2d197520f99f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67909019"
---
# <a name="mapping-mysql-and-sql-server-character-set-mysqltosql"></a>MySQL 및 SQL Server 문자 집합 매핑(MySQLToSQL)
문자 집합 (문자 집합)은 MySQL 문자 데이터 형식, 식 및 리터럴에 대해 지정할 수 있습니다.  
  
## <a name="charset-mapping"></a>문자 집합 매핑  
문자 집합 매핑은 각 MySQL 문자 집합에 대해 정의 되 고 문자 데이터 형식 변환 중에 사용 됩니다. 특정 문자 집합의 문자열 데이터 형식을 변환 하는 방법을 지정 합니다.  
  
-   국가 SQL Server 문자 형식 (NCHAR/NVARCHAR) 또는  
  
-   일반 SQL Server 문자 형식 (CHAR/VARCHAR)으로  
  
1.  **국가별** 대상 데이터베이스 문자 데이터 형식은 다음과 같습니다.  
  
    1.  **nchar**  
  
    2.  **nvarchar**  
  
2.  **일반** 대상 데이터베이스 문자 데이터 형식은 다음과 같습니다.  
  
    1.  **char**  
  
    2.  **varchar**  
  
3.  형식 매핑은 **국가별** 문자 데이터 형식에 대 한 매핑을 허용 합니다. 형식 매핑에 따라 MySQL 문자 데이터 형식이 변환 된 후에는 charset 매핑이 적용 됩니다.  
  
> [!NOTE]  
> Charset 매핑은 메타 데이터 개체 탐색기의 각 노드 수준에서 정의 될 수 있으며 MySQL에서 읽은 모든 문자 집합를 나타냅니다.  
  
## <a name="charset-mapping-on-different-node-levels"></a>다른 노드 수준의 문자 집합 매핑  
문자 집합 매핑은 노드 수준에 따라 다릅니다. 즉,  
  
1.  루트 메타 데이터 노드 수준에서  
  
2.  데이터베이스, 범주 및 개체 노드 수준에서  
  
> [!NOTE]  
> 문자 집합 매핑을 편집 하기 위해 선택한 탭에는 다른 노드 수준의 매핑에 관계 없이 3 개의 단추가 포함 됩니다.  
>   
> 아래에 이 계정과 키의 예제가 나와 있습니다.  
>   
> 1.  **적용:** 사용자가 변경한 내용을 적용 하며,이는 문자 집합 매핑을 편집 하 고 아직 저장 하지 않은 경우에만 사용할 수 있습니다.  
> 2.  **취소:** 사용자가 변경한 내용을 취소 합니다. 이 단추는 문자 집합 매핑을 편집할 때 사용할 수 있지만 저장 되지 않습니다.  
> 3.  **기본값으로 다시 설정:** 모든 매핑을 기본값으로 다시 설정 합니다.  
  
1.  **루트 메타 데이터 노드 수준:**  Charset 매핑 표에 각 문자 집합에 대 한 별도의 열이 있는 문자 집합 표를 포함 합니다. 표의 열은 다음과 같습니다.  
  
    1.  **Charset 이름이** 지정 된 표의 첫 번째 열에는 문자 집합 이름이 포함 됩니다.  
  
    2.  **문자 집합 설명** 이라는 두 번째 하나는 문자 집합 설명을 포함 합니다.  
  
    3.  **대상 문자 집합 형식** 이라는 세 번째 열은 특정 문자 집합에 대 한 매핑 설정을 포함 합니다. 이 열에 대 한 값은 다음과 같습니다.  
  
        -   CHAR/VARCHAR  
  
        -   NCHAR/NVARCHAR  
  
    > [!IMPORTANT]  
    > 특정 문자 집합의 기본값은 CHAR/VARCHAR 또는 NCHAR/NVARCHAR 뒤에 ' (기본값) ' 접두사가 있습니다.  
  
    MySQL 데이터베이스와 루트 메타 데이터 노드 수준의 대상 데이터베이스 간 문자 집합 매핑은 다음과 같습니다.  
  
    ||||  
    |-|-|-|  
    |**문자 집합 이름**|**문자 집합 설명**|**대상 문자 집합 형식 (기본값)**|  
    |번체|Big5 중국어 번체|NCHAR/NVARCHAR (기본값)|  
    |dec8|12 월 서유럽|CHAR/VARCHAR (기본값)|  
    |cp850은|DOS 유럽 서 부|CHAR/VARCHAR (기본값)|  
    |hp8|HP 서유럽|CHAR/VARCHAR (기본값)|  
    |koi8r|(KOI8-R Com 러시아어|CHAR/VARCHAR (기본값)|  
    |라틴어 1|cp1252 서유럽|CHAR/VARCHAR (기본값)|  
    |latin2|ISO 8859-2 중부 유럽|CHAR/VARCHAR (기본값)|  
    |swe7|7bit 스웨덴어|CHAR/VARCHAR (기본값)|  
    |ascii|US ASCII|CHAR/VARCHAR (기본값)|  
    |ujis|EUC-JP 일본어|NCHAR/NVARCHAR (기본값)|  
    |sjis|Shift-jis 일본어|NCHAR/NVARCHAR (기본값)|  
    |히브리어|ISO 8859-8 히브리어|CHAR/VARCHAR (기본값)|  
    |tis620|TIS620 태국어|CHAR/VARCHAR (기본값)|  
    |euckr|EUC-한국|NCHAR/NVARCHAR (기본값)|  
    |koi8u|(KOI8-U 우크라이나어|CHAR/VARCHAR (기본값)|  
    |gb2312|GB2312 중국어 간체|NCHAR/NVARCHAR (기본값)|  
    |그리스어|ISO 8859-7 그리스어|CHAR/VARCHAR (기본값)|  
    |cp 1250|Windows 중앙 유럽어|CHAR/VARCHAR (기본값)|  
    |간체 gbk|GBK 중국어 간체|NCHAR/NVARCHAR (기본값)|  
    |latin5|ISO 8859-9 터키어|CHAR/VARCHAR (기본값)|  
    |armscii8|ARMSCII-8 아르메니아어|CHAR/VARCHAR (기본값)|  
    |ut|UTF-8 유니코드|NCHAR/NVARCHAR (기본값)|  
    |ucs2|UCS-2 유니코드|NCHAR/NVARCHAR (기본값)|  
    |cp866|DOS 러시아어|CHAR/VARCHAR (기본값)|  
    |keybcs2|DOS Kamenicky 체코어-슬로바키아어|CHAR/VARCHAR (기본값)|  
    |macce|Mac 중앙 유럽어|CHAR/VARCHAR (기본값)|  
    |macroman|Mac 유럽 서 부|CHAR/VARCHAR (기본값)|  
    |cp852|DOS 중부 유럽|CHAR/VARCHAR (기본값)|  
    |latin7|ISO 8859-13 발트어|CHAR/VARCHAR (기본값)|  
    |cp 1251|Windows 키릴 자모|CHAR/VARCHAR (기본값)|  
    |cp 1256|Windows 아랍어|CHAR/VARCHAR (기본값)|  
    |cp 1257|Windows 발트어|CHAR/VARCHAR (기본값)|  
    |binary|이진 의사 문자 집합|CHAR/VARCHAR (기본값)|  
    |geostd8|GEOSTD8 그루지야어|CHAR/VARCHAR (기본값)|  
    |cp932|Windows 일본어 용 SJIS|NCHAR/NVARCHAR (기본값)|  
    |eucjpms|Windows 일본어 용 UJIS|NCHAR/NVARCHAR (기본값)|  
  
2.  **데이터베이스, 범주 또는 개체 노드 수준에서 다음을 수행 합니다.** 데이터베이스, 범주 또는 개체 노드 수준에서 charset 매핑 표에는 루트 메타 데이터 노드 수준 시각화에 있는 것과 동일한 행이 포함 되어 있습니다.  
  
    1.  표의 첫 번째 열인 **문자 집합 이름에는 문자 집합** 이름이 포함 됩니다.  
  
    2.  **문자 집합 설명** 이라는 두 번째 열에는 문자 집합 설명이 포함 되어 있습니다.  
  
    3.  유일한 차이점은 표의 세 번째 열에 있는 값입니다. **대상 데이터 형식** 이라는 세 번째 열은 특정 문자 집합에 대 한 매핑 설정을 포함 합니다. 열에 대 한 값은 다음과 같습니다.  
  
        -   상속 됨 (CHAR/VARCHAR 또는 NCHAR/NVARCHAR)  
  
        -   CHAR/VARCHAR  
  
        -   NCHAR/NVARCHAR  
  
> [!IMPORTANT]  
> -   데이터베이스, 범주 및 개체 노드 수준에서 MySQL 데이터베이스와 대상 데이터베이스 간의 문자 집합 매핑에서 열 **대상 데이터 형식** 에 대 한 루트 이외의 각 수준에 대 한 특정 문자 집합의 기본값은 ' 상속 됨 ' 이어야 합니다.  
> -   표에서 **상속** 된 값은이 특정 문자 집합으로 부모에서 상속 된 값에 따라 ' (CHAR/VARCHAR) ' 또는 ' (NCHAR/NVARCHAR) '로 접미사로 사용 됩니다.  
  
