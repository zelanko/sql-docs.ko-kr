---
title: 기본 쿼리 (Analysis Services)를 사용 하 여 데이터를 가져올 | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 67466abfccb03a689d5f717159e833143fcfafb4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62472059"
---
# <a name="import-data-by-using-a-native-query"></a>원시 쿼리를 사용하여 데이터 가져오기
[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]
테이블 형식 1400 모델에 대 한 Visual Studio의 Analysis Services 프로젝트에서 새로운 데이터 가져오기 환경을 제공 하면 매시업 때 엄청난 유연성 데이터 가져오는 동안 합니다. 이 문서에서는 데이터 원본에 대 한 연결을 만들고 다음 데이터 가져오기 지정할 원시 SQL 쿼리를 만들어 설명 합니다.

이 문서에 설명 된 작업을 완료 하려면 최신 버전의 SSDT 사용 하는 있는지를 확인 합니다. Visual Studio 2017을 사용 하는 경우 다운로드 하 고 2017 년 9 월에 설치 되어 있는지 확인 하거나 이후 Microsoft Analysis Services 프로젝트 VSIX 합니다.

[다운로드 하 여 SSDT를 설치 합니다.](../../ssdt/download-sql-server-data-tools-ssdt.md)

[Microsoft Analysis Services 프로젝트 VSIX를 다운로드 합니다.](https://marketplace.visualstudio.com/items?itemName=ProBITools.MicrosoftAnalysisServicesModelingProjects)

## <a name="create-a-datasource-connection"></a>데이터 원본 연결 만들기
데이터 원본에 연결을 이미 없다면 하나 만듭니다 해야 합니다.

1. Visual Studio에서 > **테이블 형식 모델 탐색기**를 마우스 오른쪽 단추로 클릭 **데이터 원본**를 클릭 하 고 **새 데이터 원본을**합니다.
2. **데이터 가져오기**에 데이터 원본 유형을 선택한 다음 클릭 **Connect**합니다. 데이터 원본에 연결 하는 데 필요한 추가 단계를 따릅니다.


## <a name="enter-a-query-as-a-named-expression"></a>명명 된 식으로 쿼리를 입력 합니다.
1. **테이블 형식 모델 탐색기**를 마우스 오른쪽 단추로 클릭 **식을** > **식 편집**합니다.
2. **쿼리 편집기**, 클릭 **쿼리의** > **새 쿼리** > **빈 쿼리**
3. 수식 입력줄에 입력
    ```
    = Value.NativeQuery(#"DATA SOURCE NAME", "SELECT * FROM ...")
    ```
4. 에 테이블을 만들려면 **쿼리에**쿼리를 마우스 오른쪽 단추로 클릭 한 다음 선택 **새 테이블 만들기**합니다. 새 테이블 쿼리와 동일한 이름을 갖습니다.


## <a name="example"></a>예제
이 네이티브 쿼리는 데이터 원본에서 Dimension.Employee 테이블의 모든 열을 포함 하는 모델에서 Employee 테이블을 만듭니다.

```
= Value.NativeQuery(#"SQL/myserver;WideWorldImportersDW", "SELECT * FROM Dimension.Employee")
```
![쿼리 편집기](media/ssas-import-query-example.png)


을 가져온 다음 Employees 라는 테이블은 모델에서 생성 됩니다.   

![쿼리 편집기](media/ssas-import-query-example-table.png)


## <a name="see-also"></a>참고자료  
 [Value.NativeQuery](https://msdn.microsoft.com/library/mt736917.aspx)   
 [가장](../../analysis-services/tabular-models/impersonation-ssas-tabular.md)   

  
