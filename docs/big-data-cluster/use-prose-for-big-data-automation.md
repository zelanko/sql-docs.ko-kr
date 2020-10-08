---
title: 데이터 랭글링 작업에 대한 코드 생성
titleSuffix: Azure Data Studio
description: 이 문서에서는 Azure Data Studio에서 PROSE Code Accelerator를 사용하여 일반적인 데이터 랭글링 작업의 코드를 자동으로 생성하는 방법을 설명합니다.
author: dphansen
ms.author: davidph
ms.reviewer: mihaelab
ms.date: 12/06/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: machine-learning-bdc
ms.openlocfilehash: 9768c406ca94cd16e8e9075bd5247434b8359d5c
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91725764"
---
# <a name="data-wrangling-using-prose-code-accelerator"></a>PROSE Code Accelerator를 사용한 데이터 랭글링

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

PROSE Code Accelerator는 데이터 랭글링 작업에 대해 판독 가능한 Python 코드를 생성합니다. Azure Data Studio 내에서 Notebook으로 작업하면서 생성한 코드와 손으로 작성한 코드를 원활하게 혼합할 수 있습니다. 이 문서에서는 Code Accelerator를 사용하는 방법을 간략히 설명합니다.

 > [!NOTE]
 > PROSE(Program Synthesis using Examples)는 AI를 사용하여 사람이 읽을 수 있는 코드를 생성하는 Microsoft 기술입니다. 이를 위해 사용자의 의도와 데이터를 분석하고, 여러 후보 프로그램을 생성하고, 순위 알고리즘을 사용하여 최상의 프로그램을 선택합니다. PROSE 기술에 대한 자세한 내용을 보려면 [PROSE 홈 페이지](https://microsoft.github.io/prose/)를 방문하세요.

Code Accelerator는 Azure Data Studio와 함께 미리 설치됩니다. Notebook에서 다른 Python 패키지처럼 가져올 수 있습니다. 관례상, 이 기능을 간단히 cx로 가져옵니다.

```python
import prose.codeaccelerator as cx
```

현재 릴리스에서 Code Accelerator는 다음 작업에 대한 Python 코드를 지능적으로 생성할 수 있습니다.

- Pandas 또는 Pyspark 데이터 프레임으로 데이터 파일 읽기
- 데이터 프레임의 데이터 형식 수정
- 문자열 목록에서 패턴을 나타내는 정규식 찾기

Code Accelerator 메서드의 일반적인 개요를 보려면 [설명서](/python/api/overview/azure/prose/intro)를 참조하세요.

## <a name="reading-data-from-a-file-to-a-dataframe"></a>파일의 데이터를 데이터 프레임으로 읽기

종종, 데이터 프레임으로 파일을 읽어오면 파일의 내용을 보고, 데이터 로드 라이브러리에 전달할 올바른 매개 변수를 결정하게 됩니다. 파일의 복잡도에 따라 올바른 매개 변수를 식별하는 데 몇 가지 반복 작업이 필요할 수 있습니다.

PROSE Code Accelerator는 데이터 파일의 구조를 분석하고 파일을 로드하는 코드를 자동으로 생성하여 이 문제를 해결합니다. 대부분의 경우 생성된 코드는 데이터를 올바르게 구문 분석합니다. 일부 경우에는 요구 사항에 맞게 코드를 조정해야 할 수 있습니다.

다음과 같은 예제를 참조하세요.

 ```python
import prose.codeaccelerator as cx

# Call the ReadCsvBuilder builder to analyze the file content and generate code to load it
builder = cx.ReadCsvBuilder(r'C:/911.txt')

#Set target to pyspark if generating code to use pyspark library
#builder.Target = "pyspark"

#Get the code generated to fix the data types
builder.learn().code()
 ```

이전 코드 블록은 다음 python 코드를 인쇄하여 구분된 파일을 읽습니다. 어떻게 PROSE에서 건너뛸 줄 수, header, quotechar, delimiter 등을 자동으로 계산하는지 확인합니다.

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

Code Accelerator는 구분된, JSON 및 고정 너비 파일을 데이터 프레임으로 로드하는 코드를 생성할 수 있습니다. 고정 너비 파일을 읽기 위해 `ReadFwfBuilder`는 경우에 따라 열 위치를 가져오기 위해 구문 분석할 수 있는 사람이 읽을 수 있는 스키마 파일을 사용합니다. 자세히 알아보려면 [설명서](/python/api/overview/azure/prose/intro)를 참조하세요.

## <a name="fixing-data-types-in-a-dataframe"></a>데이터 프레임의 데이터 형식 수정

pandas 또는 pyspark 데이터 프레임에 잘못된 데이터 형식이 지정되는 경우가 일반적입니다. 열에 소수의 비규격 값이 포함되어 있기 때문인 경우가 많습니다. 그 결과 Integer는 Float 또는 String으로 읽고, Date는 String으로 읽습니다. 데이터 형식을 수동으로 수정할 경우 열 개수만큼 작업량이 늘어납니다.

이러한 상황에서는 `DetectTypesBuilder`를 사용할 수 있습니다. 이 기능은 데이터를 분석하고, 데이터 형식을 블랙 박스 방식으로 수정하는 대신, 데이터 형식을 수정하는 코드를 생성합니다. 이 코드는 시작 지점으로 사용됩니다. 필요에 따라 코드를 검토하거나 사용하거나 수정할 수 있습니다.

```python
import prose.codeaccelerator as cx

builder = cx.DetectTypesBuilder(df)

#Set target to pyspark if working with pyspark
#builder.Target = "pyspark"

#Get the code generated to fix the data types
builder.learn().code()
```

자세히 알아보려면 [설명서](/python/api/overview/azure/prose/fixdatatypes)를 참조하세요.

## <a name="identifying-patterns-in-strings"></a>문자열의 패턴 식별

또 다른 일반적인 시나리오는 정리 또는 그룹화의 목적으로 문자열 열의 패턴을 검색하는 것입니다. 예를 들어, 여러 다른 형식의 날짜를 포함하는 날짜 열이 있을 수 있습니다. 값을 표준화하기 위해 정규식을 사용하여 조건문을 작성할 수 있습니다.


|행|Name                      |BirthDate      |
|--:|:-------------------------|:--------------|
| 0 |Bertram du Plessis        |1995           |
| 1 |Naiara Moravcikova        |알 수 없음        |
| 2 |Jihoo Spel                |2014           |
| 3 |Viachaslau Gordan Hilario |22-Apr-67      |
| 4 |Maya de Villiers          |19-Mar-60      |

데이터의 양과 다양성에 따라 열의 다양한 패턴에 대한 정규식을 작성하는 일은 시간이 오래 걸리는 작업일 수 있습니다. `FindPatternsBuilder`는 문자열 목록에 대한 정규식을 생성하여 위의 문제를 해결하는 강력한 코드 가속 도구입니다.

```python
import prose.codeaccelerator as cx

builder = cx.FindPatternsBuilder(df['BirthDate'])

#Set target to pyspark if working with pyspark
#builder.Target = "pyspark"

builder.learn().regexes
```

위의 데이터에 대해 `FindPatternsBuilder`에서 생성한 정규식은 다음과 같습니다.

```
^[0-9]{2}-[A-Z][a-z]+-[0-9]{2}$
^[0-9]{2}[\s][A-Z][a-z]+[\s][0-9]{4}$
^[0-9]{4}$
^Unknown$
```

정규식 생성 외에, `FindPatternsBuilder`는 생성된 정규식을 기준으로 값을 클러스터링하는 코드도 생성할 수 있습니다. 또한 열의 모든 값이 생성된 정규식을 준수한다는 것도 어설션할 수 있습니다. 자세히 알아보고 기타 유용한 시나리오를 보려면 [설명서](/python/api/overview/azure/prose/findpatterns)를 참조하세요.