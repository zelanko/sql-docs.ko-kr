---
title: sp_rxPredict | Microsoft Docs
ms.custom: ''
ms.date: 07/14/2017
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
author: jeannt
ms.author: jeannt
manager: craigg
ms.openlocfilehash: ede8232f36f42cc2b9758bdee8f50457ebd58dfe
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32998810"
---
# <a name="sprxpredict"></a>sp_rxPredict  
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

저장 된 모델을 기반으로 예측 된 값을 생성 합니다.

거의 실시간으로 기계 학습 모델에서 점수를 제공 합니다. `sp_rxPredict` 저장 프로시저에 대 한 래퍼도 제공 되는 `rxPredict` 함수 [RevoScaleR](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler) 및 [MicrosoftML](https://docs.microsoft.com/r-server/r-reference/microsoftml/microsoftml-package)합니다. 작성 된 C + 하 이며 작업 점수 매기기에 맞게 최적화 됩니다. Python 기계 학습 모델 또는 둘 다 R을 지원 합니다.

**이 항목에 적용 됩니다.**:  
- SQL Server 2017  
- Microsoft R Server로 업그레이드 된 SQL Server 2016 R 서비스  

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

입력된 데이터 원본의 모든 통과 열 뿐만 아니라 점수 열 반환 됩니다.
추가 점수를 신뢰 구간 등의 열, 알고리즘은 이러한 값의 생성을 지원 하는 경우 반환 될 수 있습니다.

## <a name="remarks"></a>주의

저장된 프로시저를 사용할 수 있도록, SQLCLR 인스턴스에 대해 활성화 되어야 합니다.

> [!NOTE]
> 이 옵션을 사용 하기 전에 보안 측면을 고려 합니다.

사용자가 요구 `EXECUTE` 데이터베이스에 대 한 권한이 있습니다.

### <a name="supported-platforms"></a>지원 플랫폼

다음 버전 중 하나가 필요합니다.  
- SQL Server 2017 컴퓨터 학습 서비스 (Microsoft R Server 9.1.0 포함)  
- Microsoft 기계 학습 서버  
- 9.1.0 Microsoft R Server는 R 서비스 인스턴스의 업그레이드 된 SQL Server R Services 2016 이상 버전  

### <a name="supported-algorithms"></a>지원되는 알고리즘

지원 되는 알고리즘 목록은 참조 [실시간 점수 매기기](../../advanced-analytics/real-time-scoring.md)합니다.

다음 모델 유형은 **하지** 지원:  
- 지원 되지 않는 유형의 R 변환 포함 하는 모델  
- 사용 하 여 모델의 `rxGlm` 또는 `rxNaiveBayes` RevoScaleR에서 알고리즘  
- PMML 모델  
- CRAN 또는 다른 저장소에서 다른 R 라이브러리를 사용 하 여 만든 모델  
- 다른 종류의 여기 나열 되지 않은 R 변환 포함 하는 모델  

## <a name="examples"></a>예

```sql
DECLARE @model = SELECT @model 
FROM model_table 
WHERE model_name = 'rxLogit trained';

EXEC sp_rxPredict @model = @model,
@inputData = N'SELECT * FROM data';
```

유효한 SQL 쿼리를 입력된 데이터에 사용 될 뿐만 아니라 *@inputData* 저장 된 모델의 열과 호환 되는 열을 포함 해야 합니다.

`sp_rxPredict` 다음.NET 열 유형만 지원: float, short, ushort, double, long, ulong 및 문자열입니다. 실시간 점수 매기기에 사용 하기 전에 필터링 하 여 입력된 데이터에서 지원 되지 않는 형식을 제외 해야 합니다. 

  해당 SQL 형식에 대 한 정보를 참조 하십시오. [SQL-CLR 형식 매핑](https://msdn.microsoft.com/library/bb386947.aspx) 또는 [CLR 매개 변수 데이터 매핑](../clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data.md)합니다.

