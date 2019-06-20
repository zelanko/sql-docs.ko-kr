---
title: 데이터 랭 글 링 작업에 대 한 코드를 생성 합니다.
titleSuffix: Azure Data Studio
description: 이 문서에서는 Azure 데이터 Studio에서 PROSE 코드 액셀러레이터 키를 사용 하 여 일반적인 데이터 랭 글 링 작업에 대 한 코드를 자동으로 생성 하는 방법을 설명 합니다.
author: rothja
ms.author: jroth
manager: jroth
ms.date: 12/06/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: f5406ce0e67322a8f7148fc83b83d0789f27e1ae
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66770781"
---
# <a name="data-wrangling-using-prose-code-accelerator"></a>PROSE 코드 Accelerator를 사용 하 여 데이터 Wrangling

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

PROSE 코드 가속기에 데이터 랭 글 링 작업에 대 한 읽을 수 있는 Python 코드를 생성합니다. Azure Data Studio 내에서 notebook에서 작업 하는 동안 원활한 방식으로 생성된 된 코드에 직접 작성 한 코드를 혼합할 수 있습니다. 이 문서에서는 코드 액셀러레이터 키를 사용 하는 방법의 개요를 제공 합니다.

 > [!NOTE]
 > 프로그램 Synthesis using Examples, 즉, PROSE에서는 AI를 사용 하 여 알기 쉬운 코드를 생성 하는 Microsoft 기술입니다. 사용자의 의도 뿐만 아니라 데이터를 분석 하 고, 여러 후보 프로그램 생성, 순위 알고리즘을 사용 하 여 가장 적합 한 프로그램을 선택 하 여 수행 합니다. PROSE 기술에 대 한 자세한 내용을 보려면, 방문 합니다 [PROSE 홈페이지](https://microsoft.github.io/prose/)합니다.

코드가 액셀러레이터 키에는 Azure Data Studio를 사용 하 여 미리 설치 합니다. Notebook에 다른 Python 패키지와 같은 데이터를 가져올 수 있습니다. 규칙에 따라 가져옵니다 줄여서 cx로 합니다.

```python
import prose.codeaccelerator as cx
```

현재 릴리스에서 코드 액셀러레이터 다음과 같은 작업에 대 한 Python 코드를 지능적으로 생성할 수 있습니다.

- Pandas 데이터 파일 읽기 또는 Pyspark 데이터 프레임입니다.
- Dataframe에 데이터 형식을 수정 합니다.
- 정규식 패턴에서 문자열의 목록 나타내는 찾기.

코드 Accelerator 방법의 일반적인 개요를 참조 합니다 [설명서](https://aka.ms/prose-codeaccelerator-overview)합니다.

## <a name="reading-data-from-a-file-to-a-dataframe"></a>데이터 프레임에 데이터 파일에서 읽기

를 데이터 프레임에 파일을 읽는 종종 파일의 내용을 확인 하 고 올바른 데이터 로딩 라이브러리에 전달할 매개 변수를 확인 합니다. 파일의 복잡성에 따라 올바른 매개 변수를 식별 합니다. 여러 번 반복 해야 합니다.

PROSE 코드 Accelerator 데이터 파일의 구조를 분석 하 고 자동으로 파일을 로드 하는 코드를 생성 하 여이 문제를 해결 합니다. 대부분의 경우 생성된 된 코드 데이터 구문을 올바르게 분석합니다. 몇 가지 경우에 요구 사항에 맞게 코드를 조정 해야 할 수 있습니다.

다음 예를 살펴 보십시오.

 ```python
import prose.codeaccelerator as cx

# Call the ReadCsvBuilder builder to analyze the file content and generate code to load it
builder = cx.ReadCsvBuilder(r'C:/911.txt')

#Set target to pyspark if generating code to use pyspark library
#builder.Target = "pyspark"

#Get the code generated to fix the data types
builder.learn().code()
 ```

이전 코드 블록 구분 기호로 분리 된 파일을 읽기 위해 다음 python 코드를 인쇄 합니다. PROSE 헤더, quotechars, 구분 기호 등 건너뛸 줄 수 자동으로 파악 하는 방법을 확인할 수 있습니다.

 ```python
import pandas as pd

def read_file(file):
    names = ["lat",
             "lng",
             "desc",
             "zip",
             "title"]

    df = pd.read_csv(file,
        skiprows = 11,
        header = None,
        names = names,
        quotechar = "\"",
        delimiter = "|",
        index_col = False,
        dtype = str,
        na_values = [],
        keep_default_na = False,
        skipinitialspace = True)
    return df
 ```

코드가 액셀러레이터 코드를 구분 하는 부하, JSON 및 데이터 프레임에 고정 폭 파일을 생성할 수 있습니다. 고정 너비 파일을 읽기 위한를 `ReadFwfBuilder` 는 필요에 따라 열 위치를 가져오려면 구문 분석할 수 있는 사용자를 읽을 수 있는 스키마 파일을 사용 합니다. 자세한 내용은 참조는 [설명서](https://aka.ms/prose-codeaccelerator-docs)합니다.

## <a name="fixing-data-types-in-a-dataframe"></a>Dataframe에 데이터 형식 수정

Pandas을 해야 일반적 또는 잘못 된 데이터 형식 사용 하 여 pyspark 데이터 프레임입니다. 몇 가지 비준수로 인해 이런 종종 열의 값입니다. 따라서 정수 Float 또는 문자열을 읽고 날짜 문자열로 읽습니다. 데이터 형식을 수동으로 수정 하는 데 필요한 노력이 열의 수에 비례 합니다.

사용할 수는 `DetectTypesBuilder` 이러한 상황에서. 데이터를 분석 하 고 블랙 박스 방식으로 데이터 형식을 수정 하는 대신 데이터 형식을 수정 하는 것에 대 한 코드를 생성 합니다. 코드를 시작 점으로 사용 됩니다. 검토를 사용 하거나 필요에 따라 수정할 수 있습니다.

```python
import prose.codeaccelerator as cx

builder = cx.DetectTypesBuilder(df)

#Set target to pyspark if working with pyspark
#builder.Target = "pyspark"

#Get the code generated to fix the data types
builder.learn().code()
```

자세한 내용은 참조는 [설명서](https://aka.ms/prose-codeaccelerator-fixtypes)합니다.

## <a name="identifying-patterns-in-strings"></a>문자열의 패턴을 식별합니다.

다른 일반적인 시나리오 정리 또는 그룹화 하기 위해 문자열 열의 패턴을 검색 하는 것입니다. 예를 들어, 다양 한 형식으로 날짜를 사용 하 여 날짜 열이 있는 될 수 있습니다. 값을 표준화 하기 위해 정규식을 사용 하는 조건문을 작성 하는 것이 좋습니다.


|   |이름                      |BirthDate      |
|---|:-------------------------|:--------------|
| 0 |Bertram du Plessis        |1995           |
| 1 |Naiara Moravcikova        |알 수 없음        |
| 2 |Jihoo Spel                |2014           |
| 3 |Viachaslau Gordan Hilario |22-년 4 월-67      |
| 4 |Maya de Villiers          |19-Mar-60      |

볼륨 및 데이터의 다양성에 따라 열에 서로 다른 패턴에 대 한 정규식을 작성은 시간이 오래 걸리는 작업을 수 있습니다. `FindPatternsBuilder` 는 문자열의 목록에 대 한 정규식을 생성 하 여 위의 문제를 해결 하는 강력한 코드 가속 도구입니다.

```python
import prose.codeaccelerator as cx

builder = cx.FindPatternsBuilder(df['BirthDate'])

#Set target to pyspark if working with pyspark
#builder.Target = "pyspark"

builder.learn().regexes
```

다음에서 생성 되는 정규식은는 `FindPatternsBuilder` 위의 데이터에 대 한 합니다.

```
^[0-9]{2}-[A-Z][a-z]+-[0-9]{2}$
^[0-9]{2}[\s][A-Z][a-z]+[\s][0-9]{4}$
^[0-9]{4}$
^Unknown$
```

Regular Expressions 생성 외에도 `FindPatternsBuilder` 생성 된 regex에 따라 값을 클러스터링에 대 한 코드를 생성할 수도 있습니다. 열의 모든 값이 생성 된 정규식을 따르는지 어설션할 수도 있습니다. 및 다른 유용한 시나리오를 참조 하세요. 자세한 내용은 참조는 [설명서](https://aka.ms/prose-codeaccelerator-findpatterns)합니다.
