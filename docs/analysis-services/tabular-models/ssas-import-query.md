---
title: "기본 쿼리 (Analysis Services)를 사용 하 여 데이터를 가져올 | Microsoft Docs"
ms.custom: 
ms.date: 10/02/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 29b296b2ae7e04871e81a9c236cb990bdd19562b
ms.openlocfilehash: 8888951d9fca0013015105998200b3ee9364855d
ms.contentlocale: ko-kr
ms.lasthandoff: 10/11/2017

---
# <a name="import-data-by-using-a-native-query"></a>기본 쿼리를 사용 하 여 데이터 가져오기

테이블 형식 1400 모델에 대 한 Visual Studio의 Analysis Services 프로젝트의 새로운 데이터 가져오기 환경 제공 때 엄청난 유연성 매시업 하는 방법을 데이터 가져오기 중 합니다. 이 문서에서는 데이터 원본에 연결을 만들고 데이터 가져오기를 지정 하는 네이티브 SQL 쿼리가 만드는 설명 합니다.

이 문서에 설명 된 작업을 완료 하려면 최신 버전의 SSDT 사용 했는지 확인 합니다. Visual Studio 2017을 사용 하는 경우 다운로드 하 고 년 9 월 2017 설치 되어 있는지 확인 하거나 이후 Microsoft Analysis Services 프로젝트 VSIX 합니다.

[다운로드 및 SSDT를 설치 합니다.](../../ssdt/download-sql-server-data-tools-ssdt.md)

[Microsoft Analysis Services 프로젝트 VSIX를 다운로드 합니다.](https://marketplace.visualstudio.com/items?itemName=ProBITools.MicrosoftAnalysisServicesModelingProjects)

## <a name="create-a-datasource-connection"></a>데이터 원본 연결 만들기
이미 사용자 데이터 원본에 대 한 연결을 없다면 하나 만듭니다 해야 합니다.

1. Visual Studio에서 > **테이블 형식 모델 탐색기**를 마우스 오른쪽 단추로 클릭 **데이터 원본**, 클릭 하 고 **새 데이터 원본을**합니다.
2. **데이터 가져오기**사용자 데이터 원본 유형을 선택한 다음 클릭 **연결**합니다. 사용자 데이터 원본에 연결 하는 데 필요한 추가 단계를 따릅니다.


## <a name="enter-a-query-as-a-named-expression"></a>명명 된 식으로 쿼리를 입력 하십시오.
1. **테이블 형식 모델 탐색기**를 마우스 오른쪽 단추로 클릭 **식** > **식 편집**합니다.
2. **쿼리 편집기**, 클릭 **쿼리** > **새 쿼리** > **빈 쿼리**
3. 수식 입력줄에 입력
    ```
    = Value.NativeQuery(#"DATA SOURCE NAME", "SELECT * FROM …")
    ```
4. 에 테이블을 만들려면 **쿼리**를 쿼리를 마우스 오른쪽 단추로 클릭 한 다음 선택 **새 테이블 만들기**합니다. 새 테이블을 쿼리에 동일한 이름을 갖습니다.


## <a name="example"></a>예제
이 기본 쿼리는 데이터 원본에서 Dimension.Employee 테이블에서 모든 열을 포함 하는 모델의 Employee 테이블을 만듭니다.

```
= Value.NativeQuery(#"SQL/myserver;WideWorldImportersDW", "SELECT * FROM Dimension.Employee")
```
![쿼리 편집기](media/ssas-import-query-example.png)


을 가져온 다음 Employees 라는 테이블은 모델에서 생성 됩니다.   

![쿼리 편집기](media/ssas-import-query-example-table.png)


## <a name="see-also"></a>참고 항목  
 [Value.NativeQuery](https://msdn.microsoft.com/library/mt736917.aspx)   
 [가장](../../analysis-services/tabular-models/impersonation-ssas-tabular.md)   

  

