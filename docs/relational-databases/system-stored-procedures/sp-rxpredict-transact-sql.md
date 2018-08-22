---
title: sp_rxPredict | Microsoft Docs
ms.custom: ''
ms.date: 08/20/2018
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_rxPredict
- sp_rxPredict_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_rxPredict procedure
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 8f46403afef0e2f6cf967561a8fd24ec6409fe93
ms.sourcegitcommit: 9528843359cc43b9c66afac363f542ae343266e9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2018
ms.locfileid: "40434863"
---
# <a name="sprxpredict"></a>sp_rxPredict  
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

SQL Server 데이터베이스에 이진 형식으로 저장 된 모델을 학습 하는 컴퓨터에 따라 지정된 된 입력에 대 한 예측된 값을 생성 합니다.

R 및 Python 기계 학습 모델에서 거의 실시간으로 점수 매기기를 제공 합니다. `sp_rxPredict` 저장 프로시저에 대 한 래퍼를 제공 합니다 `rxPredict` R 함수 [RevoScaleR](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler) 및 [MicrosoftML](https://docs.microsoft.com/r-server/r-reference/microsoftml/microsoftml-package), 및 [rx_predict](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict) 에서Python함수[revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) 하 고 [microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package)합니다. 이 C + 기록 되 고 작업을 점수 매기기에 맞게 최적화 됩니다.

**이 문서에 적용 됩니다**:  
- SQL Server 2017  
- SQL Server 2016 R Services [R 구성 요소를 업그레이드 합니다.](https://docs.microsoft.com/sql/advanced-analytics/r/use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server)

## <a name="syntax"></a>구문

```
sp_rxPredict  ( @model, @input )
```

### <a name="arguments"></a>인수

**모델**

지원 되는 형식에서 미리 학습 된 모델입니다. 

**input**

유효한 SQL 쿼리

### <a name="return-values"></a>반환 값

입력된 데이터 원본에서 통과 열 뿐만 아니라 점수 열 반환 됩니다.
추가 신뢰 구간 같은 열을 점수 매기기, 알고리즘은 이러한 값의 생성을 지원 하는 경우 반환 될 수 있습니다.

## <a name="remarks"></a>Remarks

저장된 프로시저를 사용할 수 있도록, SQLCLR 인스턴스에서 활성화 되어야 합니다.

> [!NOTE]
> 이 옵션을 사용 하기 전에 보안 문제를 고려 합니다.

사용자가 필요한 `EXECUTE` 데이터베이스에 대 한 권한이 있습니다.

### <a name="supported-platforms"></a>지원 플랫폼
 
- SQL Server 2017 Machine Learning Services (R Server 9.2 포함)  
- SQL Server 2017 Machine Learning Server (독립 실행형) 
- R Server 9.1.0에 R Services 인스턴스 업그레이드를 사용 하 여 SQL Server R Services 2016 이상  

### <a name="supported-algorithms"></a>지원되는 알고리즘

지원 되는 알고리즘 목록은 참조 하세요 [실시간 점수 매기기](../../advanced-analytics/real-time-scoring.md)합니다.

다음 모델 유형은 **되지** 지원:  
- 지원 되지 않는 유형의 R 변환 포함 하는 모델  
- 사용 하 여 모델을 `rxGlm` 또는 `rxNaiveBayes` RevoScaleR의 알고리즘  
- PMML 모델  
- CRAN 또는 다른 저장소에서 다른 R 라이브러리를 사용 하 여 만든 모델  
- 모든 다른 종류의 여기에 나열 된 것과 다른 R 변환 포함 하는 모델  

## <a name="examples"></a>예

```sql
DECLARE @model = SELECT @model 
FROM model_table 
WHERE model_name = 'rxLogit trained';

EXEC sp_rxPredict @model = @model,
@inputData = N'SELECT * FROM data';
```

유효한 SQL 쿼리를 입력된 데이터에서 사용 될 뿐 아니라 *@inputData* 저장 된 모델의 열과 호환 되는 열을 포함 해야 합니다.

`sp_rxPredict` 다음.NET 열 유형만 지원: double, float, short, ushort, long, ulong 및 문자열입니다. 실시간 점수 매기기에 사용 하기 전에 입력된 데이터에서 지원 되지 않는 형식 필터링 해야 합니다. 

  해당 SQL 형식에 대 한 자세한 내용은 [SQL-CLR 형식 매핑](/dotnet/framework/data/adonet/sql/linq/sql-clr-type-mapping) 하거나 [CLR 매개 변수 데이터 매핑](../clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data.md)합니다.

